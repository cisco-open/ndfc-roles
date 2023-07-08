# ndfc_device_serial_number_get

Return ``device_serial_number`` given ``device_name``.

The device's serial number is returned in variable ``device_serial_number``.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be queried

Device parameters are defined in the following file:

- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
# Query NX-OS switch associated with fabric_name + device_name
# and print device's serial number
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_serial_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        msg: "device_serial_number: {{ device_serial_number }}"
    when: "device_serial_number != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
