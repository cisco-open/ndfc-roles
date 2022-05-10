# ndfc_rest_vpc_create

Create vpc peering ``vpc_name`` in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which ``vpc_name`` resides
vpc_name        | str() | The name of the vpc peering to create

``fabric_name`` and ``vpc_name`` are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

Specifically:

``fabric_name`` is defined in the ``fabrics`` list

``vpc_name`` is defined in the ``vpc_peers`` list

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_vpc_create
    - ndfc_rest_config_deploy_all
  vars:
    fabric_name: f2
    vpc_name: vpc2
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
