# ndfc_rest_fabric_create_easy_fabric_ebgp

Create Easy_Fabric_eBGP fabric ``fabric_name``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric to be created

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_create_easy_fabric_ebgp
  vars:
    fabric_name: EBGP_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
