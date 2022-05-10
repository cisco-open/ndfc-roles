# ndfc-roles

This repo contains Ansible Roles and example playbooks that, together, implement a basic Spine/Leaf VXLAN/EVPN fabric using Cisco's DCNM/NDFC Controller.

The inventory contains two identical child fabrics with non-overlapping underlay addressing to facilitate interconnection via a multi-site domain (MSD) fabric.

The main playbooks, which create the two fabrics and the MSD fabric are located in the top-level directory:

```bash
example_ndfc_rest_fabric_create_f1.yml
example_ndfc_rest_fabric_create_f2.yml
example_ndfc_rest_fabric_create_msd_with_children.yml
```

These leverage the following included Roles:

```bash
ndfc_rest_config_deploy_all
ndfc_device_merged
ndfc_rest_fabric_create
ndfc_network_replaced_all
ndfc_policy_vrf_rt_import_loop
ndfc_rest_vpc_create
ndfc_vpc_interface_merged_all
```

The remaining Roles are provided as examples which facilitate various day2 ops.

### To clone this repo

```bash
git clone https://github.com/allenrobel/ndfc-roles.git
```

### Dependencies

#### cisco.dcnm Ansible Collection

The Ansible Roles in this repo require that the cisco.dcnm Collection be installed.  A ``requirements.yml`` file is included in the top-level directory which will install this collection.  Or you may do so explicitly.  It's recommended to use ``requirements.yml`` as this file may be updated with other dependencies later.

##### Example using ``requirements.yml``

```bash
ansible-galaxy collection install --requirements-file /path/to/this/repo/top-level/requirements.yml
```

##### Example using explicit Collection

```bash
ansible-galaxy collection install cisco.dcnm
```

#### jmespath

The Ansible Roles in this repo make extensive use of ``json_query()`` which requires that [jmespath](https://jmespath.org) be installed.  To install (preferably, you're running Ansible within a python virtual environment):

```bash
pip install jmespath
```

### Ansible Custom Configuration

DCNM/NDFC requires increasing the default timeout for persistent connections from the default of 30 seconds to >= 1000 seconds.  We have provided an ansible.cfg file with the requisite changes in this repo's top-level directory.  If you would rather edit your existing ansible.cfg file (where ever it is), the changes are shown below.

```bash
[persistent_connection]
command_timeout=1800
connect_timeout=1800
```

### Fabric Characteristics

The characteristics of the child/site fabrics are as follows (see also the included PDF for a topology).

1. 2 Spine acting as Route Reflectors for all Leaf and Border Gateway
2. 4 Leaf / VTEP (2 VPC pairs using fabric-peering for their virtual peer-link)
3. 2 Border Gateway / VTEP
4. 2 VRF: v1 and v2
5. L3 (ipv4 / ipv6) connectivity between VRF v1 and v2 (import/export of route-targets)
6. L2 connectivity within each VRF
7. OSPF underlay
8. VXLAN/EVPN Replication Mode: Ingress

Spines and Leafs can be added/removed by updating the Common Role Variables described below.

### Common Role Variables

To use these Roles, and example playbooks, you'll need to update some common variables used across all Roles.  These are maintained in ``./ndfc_common/vars/main.yml`` and include things like: IP addresses of your switches, VRF names, VLAN identifiers, port attachments for networks, VPC peering info and other basic information.

See the following for details around the modifications you'll need to make


[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Inventory

Next, you'll need to edit the following to add your NDFC username and password and the username/password for the switches comprising your fabric(s)

```bash
./inventory/group_vars/ndfc 
```

It is recommended (but not mandatory) that you encrypt these passwords.  Below is one way to do this.

#### Modify ./inventory/group_vars/ndfc

##### Edit ``ansible_password`` (password for NDFC controller) and ``device_password`` (password for NX-OS switches)

Add ``ansible_password`` and ``device_password`` in encrypted format (or non-encrypted, if you don't care about security).  These are the passwords you use to login to your DCNM/NDFC Controller, and NX-OS switches, respectively.

To add encrypted passwords for the NDFC controller and NX-OS devices, issue the following from this repo's top-level directory.

```bash
ansible-vault encrypt_string 'mySuperSecretNdfcPassword' --name 'ansible_password' >> ./inventory/group_vars/ndfc
ansible-vault encrypt_string 'mySuperSecretNxosPassword' --name 'device_password' >> ./inventory/group_vars/ndfc
```

ansible-vault will prompt you for a vault password, which you'll use to decrypt these passwords (using ``ansible-playbook --ask-vault-pass``) when running the example playbooks.

Example:

```bash
% ansible-vault encrypt_string 'mySuperSecretNdfcPassword' --name 'ansible_password' >> ./inventory/group_vars/ndfc
New Vault password: 
Confirm New Vault password: 
% cat ./inventory/group_vars/ndfc
ansible_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          35313565343034623966323832303764633165386439663133323832383336366362663431366565
          6238373030393562363831616266336464353963393566300a316564663135323263653165393330
          33353935396462663531323437336366653937326234313866623535313431366534363938633834
          6563336634653963320a376364323430316134623430636265383561663631343763646465626365
          36666366333438373537343033393939653830663061623362613439376161626439
% 
```

If you don't care about security, you can add a non-encrypted password by editing the file directly.
The following are example unencrypted passwords for the NDFC controller and NX-OS devices added to this file:

```bash
ansible_password: mySuperSecretNdfcPassword
device_password: mySuperSecretNxosPassword
```

##### Edit ``ansible_user``

Change ``ansible_user`` in the same file to the username associated with the above password that you're using on DCNM/NDFC.
Change ``device_username`` in the same file to the username used to login to your NX-OS switches.

Example:

```bash
ansible_user: voldomort
device_username: admin
```

##### Update ``./inventory/hosts/hosts`` with the IP address of your DCNM/NDFC Controller

```bash
% cat ./inventory/hosts/hosts 
---
ndfc:
  hosts:
    ndfc1:
      ansible_host: 192.168.1.1
```


##### To run a playbook if you encrypted your NDFC password

```bash
cd /top/level/directory/for/this/repo
ansible-playbook example_fabric_create_f1.yml --ask-vault-pass -i inventory
```

When prompted, enter the password you used in response to the ansible-vault command in step 1 above.

##### Or, to run a playbook if you didn't encrypt the NDFC password

```bash
cd /top/level/directory/for/this/repo
ansible-playbook example_fabric_create_f1.yml -i inventory
```

### Roles

Role naming conventions used in this repo.

1. If a Role pushes a specfic Ansible state, that state is included in the Role's name.
2. If a Role requires the user to provide the Ansible state, the Role's name does not include the state.
3. If a Role uses the NDFC/DCNM REST API, its name includes ``_rest_`` (e.g. ``ndfc_rest_rediscover``)


Role                           | Description
------------                   | -----------
ndfc_common                    | Common variables used by all other Roles
ndfc_device_deleted            | Delete a device from a fabric, given ``fabric_name``, ``device_name``
ndfc_device_deleted_all        | Delete all devices in a fabric, given ``fabric_name``
ndfc_device_merged             | Merge a device into a fabric, given ``fabric_name``, ``device_name``
ndfc_device_merged_all         | Merge all devices into a fabric, given ``fabric_name``
ndfc_device_query              | Query a device, given ``fabric_name``, ``device_name``
ndfc_device_query_all          | Query all devices in a fabric, given ``fabric_name``
ndfc_network_deleted_all       | Delete all networks within a fabric, given ``fabric_name``
ndfc_network_replaced_all      | Replace all networks within a fabric, given ``fabric_name``
ndfc_policy_query_generated_config_all* | Query and display all populated generated_configs on all devices, given ``fabric_name``
ndfc_policy_query_interface*    | Query and display interface config on all devices in a fabric, given ``fabric_name``, ``interface_name``
ndfc_policy_vrf_rt_import      | Import a vrf's route-targets into another vrf on a single device, given ``fabric_name``, ``device_name``
ndfc_policy_vrf_rt_import_loop | Import a vrf's route-targets into another vrf on a list of devices in a fabric, given ``fabric_name``, and a list of ``device_name``
ndfc_rest_config_deploy_all    | NDFC REST API POST calls to config-save and config-deploy
ndfc_rest_fabric_create        | Create a fabric, given ``fabric_name``
ndfc_rest_fabric_delete        | Delete a fabric, given ``fabric_name``
ndfc_rest_fabric_msd_create    | Create a multi-side domain fabric, given ``msd_fabric``
ndfc_rest_fabric_msd_delete    | Delete a multi-side domain fabric, given ``msd_fabric``
ndfc_rest_fabric_msd_child_add | Add a child fabric to an MSD fabric, given ``child_fabric``, and ``msd_fabric``
ndfc_rest_fabric_msd_child_remove | Remove a child fabric from an MSD fabric, given ``child_fabric``, and ``msd_fabric``
ndfc_rest_rediscover           | Rediscover a device, given ``fabric_name``, ``device_name``
ndfc_rest_vpc_create           | Create a VPC pair, given ``fabric_name``, ``vpc_name``
ndfc_vpc_interface_merged_all  | Create (merge) all vpc interfaces for a vpc pair, given ``fabric_name``, ``vpc_name``
ndfc_vrf_all                   | merge/delete all vrfs in a fabric, given ``fabric_name``
ndfc_vrf_replaced              | Update (replaced) a vrf, given ``fabric_name``, ``vrf_name``

\* The Roles marked with \* are examples showing how one can use cisco.dcnm.dcnm_query to glean various information from devices.  These are not used within any of the other Roles.