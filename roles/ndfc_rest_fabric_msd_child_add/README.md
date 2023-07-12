# ndfc_rest_fabric_msd_child_add

Add ``child_fabric`` to Multi-Site Domain (MSD) fabric ``msd_fabric``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
child_fabric    | string | The fabric to be added to ``msd_fabric``
msd_fabric      | string | The MSD fabric to which ``child_fabric`` will be added

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

Add ``child_fabric`` f1 to ``msd_fabric`` MSD

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_msd_child_add
  vars:
    child_fabric: f1
    msd_fabric: MSD
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
