# ndfc_network_deleted

Retrieve ``network_info`` dictionary given ``fabric_name`` and ``network_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which ``network_name`` resides.  If ``network_name`` resides in a child fabric to an msd_fabric, then ``fabric_name`` must be that of the msd_fabric.
network_name    | str() | The network for which to retrieve ``network_info`` dictionary

Network and fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbooks

# Retrieve network_info for fabric_name f1 and network_name n1111

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_info_get
  vars:
    fabric_name: f2
    network_name: n1111
  tasks:
  - block:
    - debug:
        msg: "network_info: {{ network_info | default('unable to find network. Check network_name.', true) }}"
```

# Retrieve network_info for fabric_name f1 and network_name n1111, which is a child of msd_fabric MSD.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_info_get
  vars:
    fabric_name: MSD
    network_name: n1111
  tasks:
  - block:
    - debug:
        msg: "network_info: {{ network_info | default('unable to find network. Check network_name.', true) }}"
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
