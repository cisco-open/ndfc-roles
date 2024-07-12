# ndfc_network_replaced

Replace network ``network_name`` with its current local definition in [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
network_name    | string | The network to be replaced

Network parameters are defined in the following file:

- [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_replaced
  vars:
    network_name: f1_n1111
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
