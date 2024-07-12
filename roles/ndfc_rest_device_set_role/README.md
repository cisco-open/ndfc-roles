# ndfc_rest_device_set_role

Set role for device ``device_name``.

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be merged
role            | string | The desired role for ``device_name`` e.g. leaf, spine, border_gateway, etc

Device parameters are defined in the following file:

- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Other variables used in this Role:

Defaults for the following are in [./roles/ndfc_rest_device_set_role/defaults/main.yml](/roles/ndfc_rest_device_set_role/defaults/main.yml)

Variable           | Type    | Description
-------------------|---------|------------
forceShowRun       | boolean | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | boolean | Default: ``false`` Included in the config-deploy REST call payload.

## Dependencies

## Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_device_set_role
  vars:
    - fabric_name: f1
      device_name: spine_1
      role: spine
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
