# ndfc_rest_fabric_access_mode_get

Given ``fabric_name`` return fabric access_mode in var ``read_only``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric to be queried

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_access_mode_get
  vars:
    fabric_name: f1
  tasks:
  - block:
    - debug:
        msg: "fabric {{ fabric_name }} read_only: {{ read_only }}"
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
