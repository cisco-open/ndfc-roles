# ndfc_network_deleted

Delete network ``network_name`` from fabric ``fabric_name`` using ``cisco.dcnm.dcnm_network``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
network_name    | str() | The network to be deleted
fabric_name     | str() | The fabric in which ``network_name`` resides.  If ``network_name`` resides in a child fabric to an msd_fabric, then ``fabric_name`` must be that of the msd_fabric.

Network and fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbooks

# Delete network_name n1111 from fabric_name f1.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted
  vars:
    fabric_name: f1
    network_name: n1111
```

# Delete network_name n1111 from fabric_name f1, which is a child of msd_fabric MSD.
# This will delete network_name n1111 from ALL child fabrics of msd_fabric MSD.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted
  vars:
    fabric_name: MSD
    network_name: n1111
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
