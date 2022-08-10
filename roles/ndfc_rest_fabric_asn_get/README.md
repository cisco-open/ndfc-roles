# ndfc_rest_fabric_asn_get

Given ``fabric_name`` return fabric BGP ASN in var ``fabric_asn``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric to be queried

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_asn_get
  vars:
    fabric_name: f1
  tasks:
  - block:
    - debug:
        msg: "fabric_name {{ fabric_name }} fabric_asn: {{ fabric_asn }}"
    when: "fabric_asn != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
