# ndfc_vpc_config_get

Retrieve local configuration for ``vpc_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
vpc_name        | str() | The vpc for which local configuration information is retrieved

VPC names are defined in the following file under ``vpc_peers`` section:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vpc_config_get
  vars:
    vpc_name: vpc1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
