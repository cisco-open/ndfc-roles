# ndfc_rest_config_deploy

Issue NDFC POST REST API calls to invoke config-save on ``fabric_name`` and config-deploy on fabric ``fabric_name`` device ``device_name``.

## Role Variables

Variable           | Type    | Description
-------------------|---------|------------
device_name        | string  | Device ``name`` in devices dictionary [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

Default values for the following variables are set in [./roles/ndfc_rest_config_deploy/defaults/main.yml](/roles/ndfc_rest_config_deploy/defaults/main.yml):

Variable           | Type    | Description
-------------------|---------|------------
forceShowRun       | boolean | default, false
inclAllMSDSwitches | boolean | default, false

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_config_deploy
  vars:
    device_name: leaf_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
