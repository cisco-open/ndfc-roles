# ndfc_vrf_all

Create, update, or delete all defined VRFs for a fabric.

### Role Dependencies

ndfc_common

## Other Dependencies

Dependency  | Used By      | Install With
----------- | ------------ | ------------
jmespath    | json_query() | pip install jmespath

### Role Variables

Variable     | Description
------------ | -----------
fabric_name  | The name of the fabric in which the VRFs reside.<br>Typically defined in the playbook's vars: section.
vrfs         | A list of dict containing NDFC vrf configuration.<br>See ~/ndfc_common/vars/main.yml


### Example Playbooks

~/example_ndfc_vrf_all_deleted.yml
~/example_ndfc_vrf_all_merged.yml
~/example_ndfc_vrf_all_query.yml


## License

BSD

## Author Information

Allen Robel (@packetcalc)
