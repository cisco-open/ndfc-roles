# ndfc_fabric_config_get

Retrieve config for ``fabric_name`` from the following sections of ``./inventory/group_vars/ndfc/01_fabrics.yml``

- lan_classic_fabrics
- msd_fabrics
- switch_fabrics
- external_fabrics

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric configuration to retrieve

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_networks.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_fabric_config_get
  vars:
    fabric_name: f1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
