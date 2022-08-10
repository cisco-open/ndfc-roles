# ndfc_device_serial_number_get

Return ``device_serial_number`` given ``device_name`` and fabric ``fabric_name``.

The device's serial number is returned in variable ``device_serial_number``.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be queried
fabric_name     | str() | The fabric in which device_name resides

Device and Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

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
    fabric_name: f2
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