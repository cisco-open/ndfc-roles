# ndfc_network_config_get

Retrieve local configuration for ``network_name`` from the ``networks`` portion of ``./roles/ndfc_common/vars/main.yml``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
network_name    | str() | The network to be retrieved

network names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_config_get
  vars:
    network_name: f1_n1111
  tasks:
  - block:
    - name: debug network_config
      debug:
        var: network_config
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
