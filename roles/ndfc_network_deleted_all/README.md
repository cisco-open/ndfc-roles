# ndfc_network_deleted_all

Delete all networks in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric from which to delete all networks. If ``fabric_name`` is a child fabric of an msd_fabric, then ``fabric_name`` must be that of the msd_fabric.

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbooks

# Delete all networks in fabric_name f1

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted_all
  vars:
    fabric_name: f1
```

# Delete all networks in fabric_name f1, which is a child of msd_fabric MSD
# This will delete all networks in all child fabrics of msd_fabric MSD.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted_all
  vars:
    fabric_name: MSD
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
