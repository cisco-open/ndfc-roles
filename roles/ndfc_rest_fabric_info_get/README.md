# ndfc_rest_fabric_info_get

Returns information for ``fabric_name`` in variable ``fabric_info``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric to be queried

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Default Variables

Defaults for the following are in [./roles/ndfc_rest_fabric_info_get/defaults/main.yml](/roles/ndfc_rest_fabric_info_get/defaults/main.yml)

Variable              | Type   | Description
----------------------|--------|----------------------------------------
greenfield_debug_flag | str()  | Default: enable
IS_READ_ONLY          | bool() | Default: false

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_info_get
  vars:
    fabric_name: MSD
  tasks:
  - block:
    - name: debug fabric_info
      debug:
        var: fabric_info
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
