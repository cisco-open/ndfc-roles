<seotitle>Automating NDFC using Ansible</seotitle>

# ndfc-roles

## Getting started

This repo contains Ansible Roles and example playbooks that, together, implement a basic Spine/Leaf VXLAN/EVPN fabric using Cisco's DCNM/NDFC Controller.

Two identical child fabrics and a multisite domain (MSD) fabric are defined in the role ``ndfc_common``.  The two child fabrics use  non-overlapping underlay addressing to facilitate interconnection via a multi-site domain (MSD) fabric, which is also defined in ``ndfc_common``; specifically, in ``ndfc_common/vars/main.yml``

The main playbooks, which create the two fabrics and the MSD fabric are located in the top-level directory:

```bash
example_ndfc_rest_fabric_switch_create_f1.yml
example_ndfc_rest_fabric_switch_create_f2.yml
example_ndfc_rest_fabric_msd_create_with_children.yml
```

Ref | Playbook | Description
--- | -------- | -----------
1 | ``example_ndfc_rest_fabric_switch_create_f1.yml`` | creates VXLAN/EVPN fabric f1 without connectivity to an MSD fabric
2 | ``example_ndfc_rest_fabric_switch_create_f2.yml`` | creates VXLAN/EVPN fabric f2 without connectivity to an MSD fabric
3 | ``example_ndfc_rest_fabric_msd_create_with_children.yml`` | creates VXLAN/EVPN fabrics f1 and f2, connecting them through an MSD fabric

Hence, you should use either (1 and 2) OR 3 (which creates 1 and 2, but with MSD connectivity).  That is, (1 and 2) are mutually exclusive to 3.

These playbooks leverage the following included Roles:

```bash
ndfc_rest_config_deploy_all
ndfc_device_merged
ndfc_rest_fabric_switch_create
ndfc_network_replaced_all
ndfc_policy_vrf_rt_import_evpn_loop
ndfc_rest_vpc_create
ndfc_vpc_interface_merged_all
```

And, in the case of MSD, the following additional Roles are used:

```bash
ndfc_rest_fabric_msd_create
msdc_rest_fabric_msd_child_add
```

The remaining Roles are provided as examples which facilitate various day2 ops.

## To clone this repo

```bash
git clone https://github.com/allenrobel/ndfc-roles.git
```

## Dependencies

### Cisco Nexus Dashboard (ND) + Nexus Dashboard Fabric Controller (NDFC)

ndfc-roles has been tested with the following ND+NDFC versions

Tested | ND       | NDFC
------ | -------- | -----------
Yes    | 2.2(1h)  | 12.1.1e
Yes    | 2.1(2d)  | 12.0.2f

### cisco.dcnm Ansible Collection Version 2.1.0

The Ansible Roles in this repo require that version 2.1.0 of the cisco.dcnm Collection be installed.  A ``requirements.yml`` file is included in the top-level directory which will install this collection.  Or you may do so explicitly.  It's recommended to use ``requirements.yml`` as this file may be updated with other dependencies later.

NOTE: Some earlier versions of the cisco.dcnm Ansible Collection are known not to work due to NDFC API changes involving VPC interfaces.

#### Example using ``requirements.yml``

```bash
ansible-galaxy collection install --requirements-file /path/to/this/repo/top-level/requirements.yml
```

#### Example using explicit Collection

```bash
ansible-galaxy collection install cisco.dcnm
```

### jmespath

The Ansible Roles in this repo make extensive use of ``json_query()`` which requires that [jmespath](https://jmespath.org) be installed.  To install (preferably, you're running Ansible within a python virtual environment):

```bash
pip install jmespath
```

## Ansible Custom Configuration

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

## Common Role Variables

To use these Roles, and example playbooks, you'll need to update some common variables used across all Roles.  These are maintained in ``./ndfc_common/vars/main.yml`` and include things like: IP addresses of your switches, VRF names, VLAN identifiers, port attachments for networks, VPC peering info and other basic information.

See the following for details around the modifications you'll need to make


[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

## Inventory

Next, you'll need to edit the following to add your NDFC username and password and the username/password for the switches comprising your fabric(s)

```bash
./inventory/group_vars/ndfc 
```

It is recommended (but not mandatory) that you encrypt these passwords.  Below is one way to do this.

### Modify ./inventory/group_vars/ndfc

#### Edit ``ansible_password`` (password for NDFC controller) and ``device_password`` (password for NX-OS switches)

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

#### Edit ``ansible_user``

Change ``ansible_user`` in the same file to the username associated with the above password that you're using on DCNM/NDFC.
Change ``device_username`` in the same file to the username used to login to your NX-OS switches.

Example:

```bash
ansible_user: voldomort
device_username: admin
```

#### Update ``./inventory/hosts/hosts`` with the IP address of your DCNM/NDFC Controller

```bash
% cat ./inventory/hosts/hosts 
---
ndfc:
  hosts:
    ndfc1:
      ansible_host: 192.168.1.1
```


#### To run a playbook if you encrypted your NDFC password

```bash
cd /top/level/directory/for/this/repo
ansible-playbook example_ndfc_rest_fabric_switch_create_f1.yml --ask-vault-pass -i inventory
```

When prompted, enter the password you used in response to the ansible-vault command in step 1 above.

#### Or, to run a playbook if you didn't encrypt the NDFC password

```bash
cd /top/level/directory/for/this/repo
ansible-playbook example_ndfc_rest_fabric_switch_create_f1.yml -i inventory
```

## Roles

Role naming conventions used in this repo.

1. If a Role pushes a specific Ansible state, that state is included in the Role's name.
2. If a Role requires the user to provide the Ansible state, the Role's name does not include the state.
3. If a Role uses the NDFC REST API, its name includes ``_rest_`` (e.g. ``ndfc_rest_rediscover``)


Role                           | Description
------------                   | -----------
[ndfc_common]       | Common variables used by all other Roles
[ndfc_device_config_get] | Retrieve local configuration for device, given ``device_name``
[ndfc_device_deleted] | Delete a device from a fabric, given ``device_name``
[ndfc_device_deleted_all] | Delete all devices in a fabric, given ``fabric_name``
[ndfc_device_generated_configs_get] | Retrieve device generated configs, given ``device_name``
[ndfc_device_info_get] | Query device on the NDFC controller, given ``device_name``
[ndfc_device_ipv4_address_local_get] | Retrieve device ipv4 address from local vars, given ``device_name``
[ndfc_device_ipv4_address_remote_get] | Retrieve device ipv4 address from NDFC controller, given ``device_name``
[ndfc_device_merged] | Merge a device into the topology, given ``device_name``
[ndfc_device_merged_all] | Merge all devices into a fabric, given ``fabric_name``
[ndfc_device_model_number_get] | Retrieve device model number ``device_model_number``, given ``device_name``
[ndfc_device_serial_number_get] | Retrieve device serial number ``device_serial_number``, given ``fabric_name``, ``device_name``
[ndfc_fabric_config_get] | Retrieve local configuration for fabric, given ``fabric_name``
[ndfc_network_deleted] | Delete a network, given ``fabric_name``, ``network_name``
[ndfc_network_deleted_all] | Delete all networks within a fabric, given ``fabric_name``
[ndfc_network_info_get] | Retrieve ``network_info`` dictionary, given ``fabric_name``, ``network_name``
[ndfc_network_replaced_all] | Replace all networks within a fabric, given ``fabric_name``
*[ndfc_policy_query_generated_config] | Query and display all populated generated_configs on device ``device_name``, given ``fabric_name``, ``device_name``
*[ndfc_policy_query_generated_config_all] | Query and display all populated generated_configs on all devices, given ``fabric_name``
*[ndfc_policy_query_interface_all] | Query and display interface config on all devices in a fabric, given ``fabric_name``, ``interface_name``
[ndfc_policy_vrf_rt_import_evpn] | Import a vrf's route-targets into another vrf on a single device, given ``fabric_name``, ``device_name``
[ndfc_policy_vrf_rt_import_evpn_loop] | Import a vrf's route-targets into another vrf on a list of devices in a fabric, given ``fabric_name``, and a list of ``device_name``
[ndfc_rest_config_deploy] | NDFC REST API POST calls to config-save and config-deploy for a device, given ``fabric_name``, ``device_name``
[ndfc_rest_config_deploy_all] | NDFC REST API POST calls to config-save and config-deploy for a fabric, given ``fabric_name``
[ndfc_rest_device_list_by_fabric] | Retrieve list of devices in fabric, given ``fabric_name``
[ndfc_rest_device_set_role] | Set a device's role, given ``fabric_name``, ``device_name``, and ``role``
[ndfc_rest_fabric_access_mode_get] | Retrieve a fabric's access mode, given ``fabric_name``
[ndfc_rest_fabric_access_mode_set] | Set a fabric's access mode, given ``fabric_name``, and ``read_only``
[ndfc_rest_fabric_active_fabrics_get] | Queries NDFC controller for list of active fabrics
[ndfc_rest_fabric_asn_get] | Retrieve a fabric's BGP ASN, given ``fabric_name``
[ndfc_rest_fabric_switch_create] | Create a switch fabric, given ``fabric_name``
[ndfc_rest_fabric_delete] | Delete a fabric, given ``fabric_name``
[ndfc_rest_fabric_external_create] | Create an external fabric, given ``fabric_name``
[ndfc_rest_fabric_msd_child_add] | Add a child fabric to an MSD fabric, given ``child_fabric``, and ``msd_fabric``
[ndfc_rest_fabric_msd_child_remove] | Remove a child fabric from an MSD fabric, given ``child_fabric``, and ``msd_fabric``
[ndfc_rest_fabric_msd_create] | Create a multi-side domain fabric, given ``msd_fabric``
[ndfc_rest_interface_no_shutdown] | Administratively no shutdown interface, given ``fabric_name``, ``device_name``, ``interface_name``
[ndfc_rest_interface_shutdown] | Administratively shutdown interface, given ``fabric_name``, ``device_name``, ``interface_name``
[ndfc_rest_rediscover] | Rediscover a device, given ``fabric_name``, ``device_name``
[ndfc_rest_service_node_add] | Add a service node, given ``service_node_name``
[ndfc_rest_vpc_create] | Create a VPC pair, given ``fabric_name``, ``vpc_name``
[ndfc_rest_vpc_delete] | Delete a VPC pair, given ``fabric_name``, ``vpc_name``
[ndfc_rest_vrf_list_by_fabric] | List VRFs in a given fabric, given ``fabric_name``
[ndfc_service_node_deleted] | Delete a service node, given ``service_node_name``
[ndfc_service_node_merged] | Create a service node, given ``service_node_name``
[ndfc_vpc_interface_merged_all] | Create (merge) all vpc interfaces for a vpc pair, given ``fabric_name``, ``vpc_name``
[ndfc_vrf_all] | merge/delete all vrfs in a fabric, given ``fabric_name``
[ndfc_vrf_query] | Query VRF and return json object ``info``, given ``fabric_name``, ``vrf_name``
[ndfc_vrf_replaced] | Update (replaced) a vrf, given ``fabric_name``, ``vrf_name``

\* The Roles marked with ``*`` are examples showing how one can use cisco.dcnm.dcnm_query to glean various information from devices.  These are not used within any of the other Roles.

[ndfc_common]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common
[ndfc_device_config_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_config_get
[ndfc_device_deleted]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_deleted
[ndfc_device_deleted_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_deleted_all
[ndfc_device_generated_configs_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_generated_configs_get
[ndfc_device_info_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_info_get
[ndfc_device_ipv4_address_local_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_ipv4_address_local_get
[ndfc_device_ipv4_address_remote_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_ipv4_address_remote_get
[ndfc_device_merged]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_merged
[ndfc_device_merged_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_merged_all
[ndfc_device_model_number_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_model_number_get
[ndfc_device_serial_number_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_device_serial_number_get
[ndfc_fabric_config_get]:  https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_fabric_config_get
[ndfc_network_deleted]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_network_deleted
[ndfc_network_deleted_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_network_deleted_all
[ndfc_network_info_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_network_info_get
[ndfc_network_replaced_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_network_replaced_all
[ndfc_policy_query_generated_config]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_policy_query_generated_config
[ndfc_policy_query_generated_config_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_policy_query_generated_config_all
[ndfc_policy_query_interface_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_policy_query_interface_all
[ndfc_policy_vrf_rt_import_evpn]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_policy_vrf_rt_import_evpn
[ndfc_policy_vrf_rt_import_evpn_loop]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_policy_vrf_rt_import_evpn_loop
[ndfc_rest_config_deploy]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_config_deploy
[ndfc_rest_config_deploy_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_config_deploy_all
[ndfc_rest_device_set_role]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_device_set_role
[ndfc_rest_device_list_by_fabric]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_device_list_by_fabric
[ndfc_rest_fabric_access_mode_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_access_mode_get
[ndfc_rest_fabric_access_mode_set]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_access_mode_set
[ndfc_rest_fabric_active_fabrics_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_active_fabrics_get
[ndfc_rest_fabric_asn_get]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_asn_get
[ndfc_rest_fabric_switch_create]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_switch_create
[ndfc_rest_fabric_delete]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_delete
[ndfc_rest_fabric_external_create]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_external_create
[ndfc_rest_fabric_msd_child_add]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_msd_child_add
[ndfc_rest_fabric_msd_child_remove]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_msd_child_remove
[ndfc_rest_fabric_msd_create]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_fabric_msd_create
[ndfc_rest_interface_no_shutdown]: https:////github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_interface_no_shutdown
[ndfc_rest_interface_shutdown]: https:////github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_interface_shutdown
[ndfc_rest_rediscover]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_rediscover
[ndfc_rest_service_node_add]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_service_node_add
[ndfc_rest_vpc_create]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_vpc_create
[ndfc_rest_vpc_delete]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_vpc_delete
[ndfc_rest_vrf_list_by_fabric]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_rest_vrf_list_by_fabric
[ndfc_service_node_deleted]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_service_node_deleted
[ndfc_service_node_merged]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_service_node_merged
[ndfc_vpc_interface_merged_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_vpc_interface_merged_all
[ndfc_vrf_all]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_vrf_all
[ndfc_vrf_query]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_vrf_query
[ndfc_vrf_replaced]: https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_vrf_replaced

### Code of Conduct

This repository follows the Contributor Covenant [Code of Conduct](https://github.com/allenrobel/ndfc-roles/blob/master/CODE_OF_CONDUCT.md). Please read and familiarize yourself with this document.

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.
