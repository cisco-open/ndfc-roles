# ndfc_device_merged_all

Merge all leaf, spine, border_gateway devices into fabric ``fabric_name`` using ``cisco.dcnm.dcnm_inventory``.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which the devices reside

Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

Other variables used in this Role:

From ``./roles/ndfc_devices_merged/defaults/main.yml``:

Variable        | Type   | Description
----------------|--------|------------
auth_proto      | str()  | the protocol to use to authenticate to each device.  We assume all devices use the same protocol
max_hops        | int()  | the number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time
preserve_config | bool() | If true, preserve the existing config on the device(s).  If false, do not preserve the configs.

From ``./inventory/group_vars/ndfc``:

Variable              | Type    | Description
----------------------|---------|------------
device_password       | str()   | The password used to login to the device
device_username       | str()   | The username used to login to the device

### Example Playbook

This Role is not currently reliable since it does not issue a config-save + config-deploy between devices.  Please use ``ndfc_device_merged`` instead, for now.

### License

BSD

### Author Information

Allen Robel (@packetcalc)
