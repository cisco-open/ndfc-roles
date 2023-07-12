# ndfc_rest_vpc_create

Create vpc peering ``vpc_name`` in fabric ``fabric_name``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which the vpc peering resides
vpc_name        | string | The name of the vpc peering to create

NOTE 1: ``fabric_name`` is required by ndfc_rest_config_deploy_all

Fabric and VPC parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/05_vpc.yml](/inventory/group_vars/ndfc/05_vpc.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_vpc_create
    - ndfc_rest_config_deploy_all
  vars:
    fabric_name: f2
    vpc_name: vpc2
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
