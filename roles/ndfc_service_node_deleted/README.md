# ndfc_service_node_deleted

Delete service node ``service_node_name`` using ansible deleted operation

### Role Variables

Variable          | Type  | Description
------------------|-------|----------------------------------------
service_node_name | str() | The service node to merge

Service node parameters are defined in the following file under ``service_nodes`

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_node_deleted
  vars:
    service_node_name: sn_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
