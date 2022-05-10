# ndfc_rest_vrf_list_by_fabric

Retrieve list of VRFs in fabric ``fabric_name``

Returns JSON object ``info`` which will be a list of vrf dictionaries
if the GET request succeeded, or an empty list if the GET request failed.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric to be queried


### Example Playbook

The playbook below prints select information for every VRF in fabric_name f2.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_vrf_list_by_fabric
  vars:
    fabric_name: f2
  tasks:
    - debug:
        msg: "vrfName: {{ item.vrfName }} vrfId {{ item.vrfId }} vrfStatus {{ item.vrfStatus }}"
      loop: "{{ info | json_query(q1) }}"
      vars:
          q1: "[*].{ vrfId: vrfId, vrfName: vrfName, vrfStatus: vrfStatus }"
      loop_control:
        label: vrf_info
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
