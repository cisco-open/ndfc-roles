# ndfc_vrf_replaced

Replace vrf ``vrf_name`` in fabric ``fabric_name`` with the current user-defined parameters.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which ``vrf_name`` resides
vrf_name        | str() | The vrf to update

Fabric and vrf parameters, including ``fabric_name`` and ``vrf_name``, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

Specifically, vrfs are defined in the ``vrfs`` list in the above file.  User-defined parameters include:

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | str()        | Fabric in which network resides
vrf_name               | vrf_1          | str()        | vrf in which network resides
vrf_id                 | 9003031        | int()        | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | int()        | vrf associated vlan 
vrf_template           | TemplateVrf    | str()        | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | str()        | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | str()        | Service vrf template
attach                 | See example    | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the vrf is attached

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_vrf_replaced
  vars:
    fabric_name: f1
    vrf_name: v2
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
