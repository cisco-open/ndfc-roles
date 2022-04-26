# ndfc_device_deleted_all

Delete all devices from fabric fabric_name

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric from which the devices will be deleted

Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbooks

```
example_ndfc_device_deleted_all.yml
example_ndfc_fabric_delete_rest_f1.yml
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
