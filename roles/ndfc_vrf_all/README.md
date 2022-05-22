# ndfc_vrf_all

Create, update, or delete all defined VRFs in fabric ``fabric_name``.

### Role Dependencies

ndfc_common

## Other Dependencies

Dependency  | Used By      | Install With
----------- | ------------ | ------------
jmespath    | json_query() | pip install jmespath

### Role Variables

Variable     | Description
------------ | -----------
fabric_name  | The name of the fabric in which the VRFs reside.<br>Typically defined in the playbook's vars: section.
state        | Ansible state.  One of merged, overridden, replaced, or deleted.

### Other variables

This role reads the ``vrfs`` list of dictionaries from ``~/ndfc_common/vars/main.yml``

This list of dictionaries define VRFs and their attachment to devices.  Its property names are provided below.  See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | str()        | Fabric in which vrf resides
vrf_name               | vrf_1          | str()        | name of the vrf
vrf_id                 | 9003031        | int()        | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | int()        | vrf associated vlan 
vrf_template           | TemplateVrf    | str()        | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | str()        | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | str()        | Service vrf template
attach                 | See example    | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the vrf is attached

Example entry in the ``vrfs`` list.

```yaml
vrfs:
- fabric: "{{ fabrics[0].name }}"
  vrf_name: v1
  vrf_id: 9003031
  vlan_id: 3031
  vrf_template: Default_VRF_Universal
  vrf_extension_template: Default_VRF_Extension_Universal
  service_vrf_template: null
  attach:
    - ip_address: "{{ leafs[0].ip }}"
    - ip_address: "{{ leafs[1].ip }}"
    - ip_address: "{{ leafs[2].ip }}"
    - ip_address: "{{ leafs[3].ip }}"
```


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
