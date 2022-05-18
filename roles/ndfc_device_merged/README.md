# ndfc_device_merged

Merge device ``device_name`` into fabric ``fabric_name`` using ``cisco.dcnm.dcnm_inventory``.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be merged
fabric_name     | str() | The fabric in which ``device_name`` resides
config_deploy_for_existing_device | bool() | Default: ``true``. Determines whether to skip config-save + config-deploy if the device already exists in the topology.  If set to ``false``, the config-save and config-deploy tasks will be skipped if the device already exists.  If set to ``true``, the tasks will run unconditionally (i.e. regardless whether the device exists or not).


Device and Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

Other variables used in this Role:

From ``./roles/ndfc_devices_merged/defaults/main.yml``:

Variable        | Type   | Description
----------------|--------|------------
auth_proto      | str()  | The protocol to use to authenticate to each device.  We assume all devices use the same protocol.
max_hops        | int()  | The number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time.
preserve_config | bool() | If true, preserve the existing config on the device(s).  If false, do not preserve the configs.
forceShowRun    | bool() | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | bool() | Default: ``false`` Included in the config-deploy REST call payload.

From ``./inventory/group_vars/ndfc``:

Variable              | Type    | Description
----------------------|---------|------------
device_password       | str()   | The password used to login to the device
device_username       | str()   | The username used to login to the device

### Dependencies

### Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_merged
  vars:
    fabric_name: f1
    device_name: spine_1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
