# ndfc_network_info_get

Query the NDFC controller and retrieve ``network_info`` dictionary given ``network_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
network_name    | str() | The network for which to retrieve ``network_info`` dictionary

Network names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

NOTE: ``network_name`` must match value in network entry's ``name:`` key (i.e. don't try to match on the value of the ``net_name:`` key).

## Returned Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
network_info    | dict() | information pertaining to network ``network_name``

### Example Playbooks

Retrieve ``network_info`` dictionary for ``network_name`` msd_n1111

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_info_get
  vars:
    network_name: msd_n1111
  tasks:
  - block:
    - debug:
        msg: "network_info: {{ network_info | default('unable to find network. Check network_name.', true) }}"
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
