# ndfc_rest_fabric_asn_get

Given ``fabric_name`` return fabric BGP ASN in var ``fabric_asn``

## Returned variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_asn      | string | The BGP AS of the queried fabric

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric to be queried

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbooks

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

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
