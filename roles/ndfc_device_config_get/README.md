# ndfc_device_config_get

Retrieve local configuration for ``device_name``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device for which local configuration information is retrieved

Device parameters are defined in the following file:

- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_config_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - name: debug device_config
      debug:
        var: device_config
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
