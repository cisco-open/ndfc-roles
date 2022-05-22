# ndfc_vrf_query

Query VRF ``vrf_name`` in fabric ``fabric_name`` and return json object ``info``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which ``vrf_name`` resides
vrf_name        | str() | The vrf to query

Fabric and vrf parameters, including ``fabric_name`` and ``vrf_name``, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vrf_query
  vars:
    fabric_name: f1
    vrf_name: v1
  tasks:
  - block:
    - debug:
        msg: "info.parent.fabric: {{ info.parent.fabric }}"
    - debug:
        msg: "info.parent.vrfId: {{ info.parent.vrfId }}"
    - debug:
        msg: "info.parent.vrfStatus: {{ info.parent.vrfStatus }}"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
