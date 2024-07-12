# ndfc_device_generated_configs_get

Retrieve populated generated configs from ``device_name`` in fabric ``fabric_name``

Store in variable ``device_generated_configs``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to query

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_generated_configs_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        var: device_generated_configs
    when: "device_generated_configs != ''"
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
