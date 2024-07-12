# ndfc_vrf_query

Query VRF ``vrf_name`` and return json object ``vrf_info`` which contains vrf information for ``vrf_name`` from the NDFC controller.

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
vrf_name        | string | The vrf to query.

VRF parameters are defined in the following files:

[./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

NOTE, ``vrf_name`` above corresponds to the ``name:`` key within the vrfs dictionary in the file noted above.  The ``name:`` key is unique across all defined vrfs, whereas the ``vrf_name:`` key is not unique and cannot be used with this role.  By way of example, in the entry below, you would use the value of ``name:`` rather than the value of ``vrf_name``.  The example playbook below shows the correct value to use.

## Example entry in the vrfs dictionary

```yaml
  f2_v1:
    name: f2_v1
    fabric: "{{ switch_fabrics.f2.name }}"
    vrf_name: v1
    vrf_id: 63031
    vlan_id: 3031
    vrf_template: Default_VRF_Universal
    vrf_extension_template: Default_VRF_Extension_Universal
    service_vrf_template: null
    attach:
    - ip_address: "{{ devices.leaf_5.ip }}"
    - ip_address: "{{ devices.leaf_6.ip }}"
    - ip_address: "{{ devices.leaf_7.ip }}"
    - ip_address: "{{ devices.leaf_8.ip }}"
```

### Example playbook to query the above vrf

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vrf_query
  vars:
    vrf_name: f2_v1
  tasks:
  - debug:
      msg: "vrf_info.parent.fabric: {{ vrf_info.parent.fabric }}"
  - debug:
      msg: "vrf_info.parent.vrfId: {{ vrf_info.parent.vrfId }}"
  - debug:
      msg: "vrf_info.parent.vrfStatus: {{ vrf_info.parent.vrfStatus }}"
```

See the following for details:

[./inventory/group_vars/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/inventory/group_vars/README.md)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
