# ndfc_network_deleted

Delete network ``network_name`` where ``network_name`` matches the ``name`` key in the local ``networks`` dictionary in [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
network_name    | string | The network to be deleted

Network parameters are defined in the following file:

- [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbooks

### Delete network_name f1_n1111

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted
  vars:
    network_name: f1_n1111
```

### Delete network_name msd_n1111, which resides in fabric MSD (an msd fabric)

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

## License

BSD

## Author Information

Allen Robel (@packetcalc)
