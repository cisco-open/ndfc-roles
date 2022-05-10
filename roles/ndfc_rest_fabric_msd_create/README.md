# ndfc_rest_fabric_create_msd

Create Multi-Site Domain (MSD) fabric ``msd_fabric``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
msd_fabric      | str() | The MSD fabric to be created

MSD fabric parameters are defined in the following file under ``msd_fabrics``

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_create_msd
  vars:
    msd_fabric: MSD
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
