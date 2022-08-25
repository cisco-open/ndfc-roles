# ndfc_service_node_config_get

Retrieve local configuration for ``service_node_name``

### Role Variables

Variable          | Type  | Description
------------------|-------|----------------------------------------
service_node_name | str() | The service node for which local configuration information is retrieved

Service node names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_node_config_get
  vars:
    service_node_name: sn_1
  tasks:
  - block:
    - name: debug service_node_config
      debug:
        var: service_node_config
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
