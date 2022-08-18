# ndfc_vpc_interface_merged_all

Merge all vpc interfaces for vpc peer ``vpc_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
vpc_name        | str() | The name of the vpc peer for which interfaces will be merged

``vpc_name`` is defined in the following file within the ``vpc_peers`` dictionary:

``./roles/ndfc_common/vars/main.yml``


See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### See also

``vpc_interfaces`` list in [./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vpc_interface_merged_all
  vars:
    fabric_name: f1
    vpc_name: vpc1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
