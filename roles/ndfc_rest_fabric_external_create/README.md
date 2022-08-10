# ndfc_rest_fabric_external_create

Create External fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The External fabric to be created

External fabric parameters are defined in the following file under ``external_fabrics``

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_external_create
  vars:
    fabric_name: ext_fabric_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
