# ndfc_vpc_config_get

Retrieve configuration for ``vpc_name`` from the local inventory

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
vpc_name        | string | The vpc for which local configuration information is retrieved

VPC parameters are defined in the following file:

- [./inventory/group_vars/ndfc/05_vpc.yml](/inventory/group_vars/ndfc/05_vpc.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

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
