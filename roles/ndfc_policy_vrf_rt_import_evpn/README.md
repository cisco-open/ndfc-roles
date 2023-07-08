# ndfc_policy_vrf_rt_import_evpn

Import vrf ``import_vrf_name``'s route-targets into vrf ``vrf_name`` on device ``device_name`` using Ansible state ``state``

NOTE: This role isn't needed when route-target imports are added to a VRF's config.  See the following:
- [./inventory/group_vars/README.md](/inventory/group_vars/README.md)
- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which ``device_name`` resides
device_name     | string | The device to which vrf ``vrf_name`` is attached
vrf_name        | string | The vrf into which ``import_vrf_name``'s route-targets will be imports
import_vrf_name | string | The vrf whose route-targets will be imported into ``vrf_name``
state           | string | The Ansible state to apply for the import. e.g. ``deleted`` to delete the import, ``merged`` to merge the import.  NOTE: ``replaced`` is not a valid state for this module.

Fabric, device and VRF parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)
- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
# Import vrf v2's route-targets into vrf v1 on device leaf_2 in fabric f1, using Ansible state 'merged'
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_policy_vrf_rt_import_evpn
  vars:
    fabric_name: f1
    device_name: leaf_2
    vrf_name: v1
    import_vrf_name: v2
    state: merged
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
