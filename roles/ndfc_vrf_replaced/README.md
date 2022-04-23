# ndfc_vrf_replaced

Update VRF using Ansible state: replaced

### Requirements

None

### Role Variables

fabric_name: The name of the fabric in which the VRF resides.  This will typically be defined in the playbook's vars: section.
vrfs: A list of dict containing NDFC vrf configuration. See vrfs list of dict in ~/ndfc_common/vars/main.yml


### Dependencies

## Example Playbook

example_ndfc_vrf_replaced.yml

### License

BSD

### Author Information

Allen Robel (@packetcalc)
