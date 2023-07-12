# ndfc_device_deleted

Delete device ``device_name``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be deleted

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_deleted
  vars:
    device_name: spine_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
