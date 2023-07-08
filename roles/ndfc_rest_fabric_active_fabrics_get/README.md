# ndfc_rest_fabric_active_fabrics_get

Returns the list of active fabrics on the Nexus Dashboard Fabric Controller.

### Returned Variables

Variable        | Type         | Description
----------------|--------------|----------------------------------------
active_fabrics  | list of dict | a list of active fabrics

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_active_fabrics_get
  tasks:
  - block:
    - debug:
        var: active_fabrics
    when: "active_fabrics != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
