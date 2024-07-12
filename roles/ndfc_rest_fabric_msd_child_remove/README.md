# ndfc_rest_fabric_msd_child_remove

Remove child fabric ``child_fabric`` from Multi-Site Domain (MSD) fabric ``msd_fabric``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
child_fabric    | string | The fabric to be removed from ``msd_fabric``
msd_fabric      | string | The MSD fabric from which ``child_fabric`` will be removed

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

Remove ``child_fabric`` f1 from ``msd_fabric`` MSD

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_msd_child_remove
  vars:
    child_fabric: f1
    msd_fabric: MSD
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
