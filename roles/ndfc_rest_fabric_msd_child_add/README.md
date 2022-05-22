# ndfc_rest_fabric_msd_child_add

Add ``child_fabric`` to Multi-Site Domain (MSD) fabric ``msd_fabric``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
msd_fabric      | str() | The MSD fabric to which ``child_fabric`` will be added
child_fabric    | str() | The fabric to be added to ``msd_fabric``

Fabric parameters are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


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
