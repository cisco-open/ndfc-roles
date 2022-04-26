# ndfc_device_deleted

Given fabric_name and device_name, delete device device_name from fabric fabric_name using cisco.dcnm.dcnm_inventory

### Requirements

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device's name (see below)
fabric_name     | str() | The fabric in which device_name resides

Device and fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

example_ndfc_device_deleted.yml

### License

BSD

### Author Information

Allen Robel (@packetcalc)
