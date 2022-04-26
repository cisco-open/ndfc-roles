# ndfc_policy_vrf_rt_import

Import vrf ``import_vrf_name``'s route-targets into vrf ``vrf_name`` on device ``device_name`` in fabric ``fabric_name`` using Ansible state ``state``


### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to which vrf ``vrf_name`` is attached
fabric_name     | str() | The fabric in which device_name resides
vrf_name        | str() | The vrf into which ``import_vrf_name``'s route-targets will be imports
import_vrf_name | str() | The vrf whose route-targets will be imported into ``vrf_name``
state           | str() | The Ansible state to apply for the import. e.g. ``deleted`` to delete the import, ``merged`` to merge the import, etc.

Fabric, device, and vrf names are are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
# Import vrf v2's route-targets into vrf v1 on device leaf_2 in fabric f1, using Ansible state 'merged'
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_policy_vrf_rt_import
  vars:
    fabric_name: f1
    device_name: leaf_2
    vrf_name: v1
    import_vrf_name: v2
    state: merged
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
