# ndfc_network_deleted_all

Delete all networks in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which device_name resides

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted_all
  vars:
    fabric_name: f1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
