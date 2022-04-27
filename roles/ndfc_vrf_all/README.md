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

##### delete all vrf in fabric f2
```yaml
---
- hosts: ndfc
  name: delete all vrf in fabric f2
  gather_facts: false
  roles:
    - ndfc_vrf_all
    - ndfc_config_deploy_all_rest
  vars:
    fabric_name: f2
    state: deleted
```

##### merge all vrf in fabric f1
```yaml
---
- hosts: ndfc
  name: merge all vrf in fabric f1
  gather_facts: false
  roles:
    - ndfc_vrf_all
    - ndfc_config_deploy_all_rest
  vars:
    fabric_name: f1
    state: merged
```


## License

BSD

## Author Information

Allen Robel (@packetcalc)
