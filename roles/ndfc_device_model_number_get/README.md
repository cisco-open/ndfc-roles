# ndfc_device_model_number_get

Retrieve ``device_model_number`` from NDFC controller, given ``device_name``.

The device's model number is returned in variable ``device_model_number``.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be queried

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
# Query NX-OS switch associated with fabric_name + device_name
# and print device's model number
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_model_number_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        msg: "device_model_number: {{ device_model_number }}"
    when: "device_model_number != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
