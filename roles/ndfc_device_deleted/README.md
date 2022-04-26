# ndfc_device_deleted

Delete device ``device_name`` from fabric ``fabric_name`` using ``cisco.dcnm.dcnm_inventory``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be deleted
fabric_name     | str() | The fabric in which device_name resides

Device and fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_deleted
  vars:
    fabric_name: f1
    device_name: spine_1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
