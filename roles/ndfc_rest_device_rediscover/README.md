# ndfc_rest_device_rediscover

Rediscover device ``device_name`` in fabric ``fabric_name``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be rediscovered
fabric_name     | string | The fabric in which ``device_name`` resides

Device and Fabric names are defined in the following files:

- ./inventory/group_vars/ndfc/01_fabrics.yml
- ./inventory/group_vars/ndfc/02_devices.yml

See the following for details:

[./inventory/group_vars/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_device_rediscover
  vars:
    fabric_name: f1
    device_name: spine_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
