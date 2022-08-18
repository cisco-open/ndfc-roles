# ndfc_network_deleted_external_fabric_all

Delete all networks in external fabric ``fabric_name``

NOTE: If the networks were created in an msd or switch fabric, use their corresponding roles instead

SEE ALSO: ndfc_network_deleted_msd_fabric_all
SEE ALSO: ndfc_network_deleted_switch_fabric_all

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The external fabric from which to delete all networks.

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbooks

# Delete all networks in external fabric_name f1

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_network_deleted_external_fabric_all
  vars:
    fabric_name: f1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
