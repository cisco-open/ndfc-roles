# ndfc_device_merged

Merge an NX-OS device into the fabric using cisco.dcnm.dcnm_inventory.

### Requirements

### Role Variables

See the following device dictionary lists in ndfc_common/vars/main.yml

fabrics[0].leafs
fabrics[0].spines
fabrics[0].border_gateways

The structure of each object in the list is:

```
    - name: leaf_1
      ip: 172.22.150.102
      role: leaf
```

Where

Variable              | Type       | Description
----------------------|------------|------------
name                  | str()      | The device name
ip                    | ip address | The seed ip (device's mgmt0 interface address)
role                  | str()      | the device's role in the fabric (leaf, spine, border_gateway, etc)

See also variables whose defaults are set in ``./roles/ndfc_devices_merged/defaults/main.yml``:

Variable        | Type   | Description
----------------|--------|------------
auth_proto      | str()  | the protocol to use to authenticate to each device.  We assume all devices use the same protocol
max_hops        | int()  | the number of CDP hops to traverse when discovering devices. We set this to 0 to discover one device at a time
preserve_config | bool() | If true, preserve the existing config on the device(s).  If false, do not preserve the configs.

### Dependencies

### Example Playbook

example_ndfc_fabric_create_rest_f1.yml
example_ndfc_device_merged.yml

### License

BSD

### Author Information

Allen Robel (@packetcalc)
