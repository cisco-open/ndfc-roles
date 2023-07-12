# ndfc_vrf_replaced

Replace vrf ``vrf_name`` in fabric ``fabric_name`` with the current user-defined parameters.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
vrf_name        | string | The vrf to update

NOTE, ``vrf_name`` above corresponds to the ``name:`` key within the vrfs dictionary in the file noted below.  The ``name:`` key is unique across all defined vrfs, whereas the ``vrf_name:`` key is not unique and cannot be used with this role. See the example vrf entry and playbook below which demonstrate the value to use in your playbook.

VRF parameters are defined in the following file:

- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

User parameters in the the ``vrfs`` dictionary include:

Variable               | Example               | Type         | Description
-----------------------|-----------------------|--------------|-------------------
fabric                 | f1                    | string       | Fabric in which vrf resides
vrf_name               | vrf_1                 | string       | name of the vrf
vrf_id                 | 9003031               | integer      | vrf Layer3 VNI / vn-segment
vlan_id                | 3031                  | integer      | vrf associated vlan
import_vpn_rt          | 65001:3031,65002,3031 | string       | vpn route-targets to import
import_evpn_rt         | 65001:3031,65002,3031 | string       | evpn route-targets to import
vrf_template           | TemplateVrf           | string       | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf         | string       | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf            | string       | Service vrf template
attach                 | See example           | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1           | IP address   | mgmt0 address of the switch to which the vrf is attached

#### Example entry in vrfs dictionary

```yaml
vrfs:
  f2_v1:
    name: f2_v1
    fabric: "{{ switch_fabrics.f2.name }}"
    vrf_name: v1
    vrf_id: 63031
    vlan_id: 3031
    import_vpn_rt: 65001:63031,65002:63032
    import_evpn_rt: 65001:63031,65002:63032
    vrf_template: Default_VRF_Universal
    vrf_extension_template: Default_VRF_Extension_Universal
    service_vrf_template: null
    attach:
    - ip_address: "{{ devices.leaf_5.ip }}"
    - ip_address: "{{ devices.leaf_6.ip }}"
    - ip_address: "{{ devices.leaf_7.ip }}"
    - ip_address: "{{ devices.leaf_8.ip }}"
```

## Example Playbook (referencing the above example vrf entry)

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vrf_replaced
  vars:
    vrf_name: f2_v1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
