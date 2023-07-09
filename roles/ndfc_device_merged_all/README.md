# ndfc_device_merged_all

Merge all leaf, spine, border_gateway devices into fabric ``fabric_name``.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which the devices reside

Fabric and device parameters are defined in the following files:

- ./inventory/group_vars/ndfc/01_fabrics.yml
- ./inventory/group_vars/ndfc/02_devices.yml

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Other variables used in this Role:

- [./roles/ndfc_device_merged_all/defaults/main.yml](/roles/ndfc_device_merged_all/defaults/main.yml)

Variable        | Type    | Description
----------------|---------|------------
auth_proto      | string  | the protocol to use to authenticate to each device.  We assume all devices use the same protocol
max_hops        | integer | the number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time
preserve_config | boolean | If true, preserve the existing config on the device(s).  If false, do not preserve the configs.

- [./inventory/group_vars/ndfc/00_connection.yml](/inventory/group_vars/ndfc/00_connection.yml)

Variable              | Type    | Description
----------------------|---------|------------
device_password       | string   | The password used to login to the device
device_username       | string   | The username used to login to the device

### Dependencies

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_merged_all
  vars:
    fabric_name: f1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
