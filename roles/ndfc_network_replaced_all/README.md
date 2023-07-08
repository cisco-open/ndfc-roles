# ndfc_network_replaced_all

Replace all networks in fabric ``fabric_name`` with their current definitions in Replace all networks in fabric ``fabric_name`` with their current definitions in ``./roles/ndfc_common/vars/main.yml``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which the networks reside

Fabric and network parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_networks.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_replaced_all
  vars:
    fabric_name: MSD
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
