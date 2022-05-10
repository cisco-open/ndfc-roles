# ndfc_rest_fabric_msd_child_remove

Remove child fabric ``child_fabric`` from Multi-Site Domain (MSD) fabric ``msd_fabric``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
msd_fabric      | str() | The MSD fabric from which ``child_fabric`` will be removed
child_fabric    | str() | The fabric to be removed from ``msd_fabric``

Fabric parameters are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

Remove ``child_fabric`` f1 from ``msd_fabric`` MSD

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_msd_child_remove
  vars:
    child_fabric: f1
    msd_fabric: MSD
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
