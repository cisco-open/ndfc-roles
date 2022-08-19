# ndfc_network_replaced

Replace network ``network_name`` with its current definition in ``./roles/ndfc_common/vars/main.yml``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
network_name    | str() | The network to be replaced

Network parameters, including ``network_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_replaced
  vars:
    network_name: f1_n1111
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
