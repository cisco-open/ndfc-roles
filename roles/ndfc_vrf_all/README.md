# ndfc_vrf_all

Create, update, or delete all defined VRFs in fabric ``fabric_name``.

### Role Variables

Variable     | Description
------------ | -----------
fabric_name  | The name of the fabric in which the VRFs reside.<br>Typically defined in the playbook's vars: section.
state        | Ansible state.  One of merged, overridden, replaced, or deleted.

### Other variables

This role reads the ``vrfs`` dictionary from:

- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

This dictionary defines VRFs and their attachment to devices.  Its property names are provided below.  See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | string       | Fabric in which vrf resides
import_vpn_rt          | 65000:50001    | string       | vpn route-target to import
import_evpn_rt         | 65000:50001    | string       | evpn route-target to import
vrf_name               | vrf_1          | string       | name of the vrf
vrf_id                 | 9003031        | integer      | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | integer      | vrf associated vlan 
vrf_template           | TemplateVrf    | string       | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | string       | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | string       | Service vrf template
attach                 | See example    | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the vrf is attached

### Example Playbooks

##### delete all vrf in fabric f2
```yaml
---
- hosts: ndfc
  name: delete all vrf in fabric f2
  gather_facts: false
  roles:
    - ndfc_vrf_all
    - ndfc_rest_config_deploy_all
  vars:
    fabric_name: f2
    state: deleted
```

##### merge all vrf in fabric f1
```yaml
---
- hosts: ndfc
  name: merge all vrf in fabric f1
  gather_facts: false
  roles:
    - ndfc_vrf_all
    - ndfc_config_rest_deploy_all
  vars:
    fabric_name: f1
    state: merged
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
