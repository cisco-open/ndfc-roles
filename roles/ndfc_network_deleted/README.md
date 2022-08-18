# ndfc_network_deleted

Delete network ``network_name`` where ``network_name`` matches the ``name`` key in the ``networks`` dictionary in ``roles/ndfc_common/vars/main.yml``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
network_name    | str() | The network to be deleted

Network names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbooks

# Delete network_name f1_n1111

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted
  vars:
    network_name: f1_n1111
```

# Delete network_name msd_n1111, which resides in fabric MSD (an msd fabric)

This will delete network_name msd_n1111 from all child fabrics of fabric MSD.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted
  vars:
    network_name: msd_n1111
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
