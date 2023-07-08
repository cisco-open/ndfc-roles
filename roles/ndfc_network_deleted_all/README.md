# ndfc_network_deleted_all

Delete all networks in fabric ``fabric_name``

NOTE: If the networks were created in an MSD fabric, Ansible will throw an InvalidFabric error if you set ``fabric_name`` to that of a child/switch fabric.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric from which to delete all networks.

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbooks

# Delete all networks in external fabric_name f1

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted_all
  vars:
    fabric_name: MSD
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
