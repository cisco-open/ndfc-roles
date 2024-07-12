# ndfc_rest_fabric_create_msd

Create Multi-Site Domain (MSD) fabric ``fabric_name``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The MSD fabric to be created

Fabric parameters, including ``fabric_name`, are defined in the following file:

- ./inventory/group_vars/ndfc/01_fabrics.yml

See the following for details:

[./inventory/group_vars/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/inventory/group_vars/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_create_msd
  vars:
    fabric_name: MSD
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
