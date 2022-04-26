# ndfc_device_rediscover_rest

Rediscover device ``device_name`` in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be rediscovered
fabric_name     | str() | The fabric in which ``device_name`` resides

Device and Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_rediscover_rest
  vars:
    fabric_name: f1
    device_name: spine_1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
