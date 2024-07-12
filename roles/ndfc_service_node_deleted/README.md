# ndfc_service_node_deleted

Delete service node ``service_node_name``

## Role Variables

Variable          | Type   | Description
------------------|--------|----------------------------------------
service_node_name | string | The service node to merge

Service node parameters are defined in the following file:

- [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_node_deleted
  vars:
    service_node_name: sn_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
