# ndfc_network_config_get

Retrieve local configuration for ``network_name``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
network_name    | string | The network to be retrieved

Network parameters are defined in the following file:

- [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

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
