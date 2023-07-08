# ndfc_device_merged

Merge device ``device_name`` into the topology.

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be merged

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Other variables used in this Role:

- [./roles/ndfc_devices_merged/defaults/main.yml](/roles/ndfc_devices_merged/defaults/main.yml)

Variable           | Type       | Description
-------------------|------------|------------
auth_proto         | string     | The protocol to use to authenticate to each device.  We assume all devices use the same protocol.
max_hops           | integer    | The number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time.
preserve_config    | boolean    | If true, preserve the existing config on the device(s).  If false, do not preserve the configs.
forceShowRun       | boolean    | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | boolean    | Default: ``false`` Included in the config-deploy REST call payload.

- [./inventory/group_vars/ndfc/00_connection.yml](/inventory/group_vars/ndfc/00_connection.yml)

Variable              | Type    | Description
----------------------|---------|------------
device_password       | string  | The password used to login to the device
device_username       | string  | The username used to login to the device

### Dependencies

### Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_merged
  vars:
    device_name: spine_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
