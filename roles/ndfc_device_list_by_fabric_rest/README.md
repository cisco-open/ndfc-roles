# ndfc_device_list_by_fabric_rest

Retrieve list of devices in fabric ``fabric_name``

Returns JSON object ``info`` which will be a list of switch dictionaries
if the GET request succeeded, or an empty list if the GET request failed.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric to be queried


### Example Playbook

The playbook below prints select information for every switch in fabric f2.

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_list_by_fabric_rest
  vars:
    fabric_name: f2
  tasks:
      - debug:
          msg: "ipAddress: {{ item.ipAddress }} logicalName: {{ item.logicalName }} model {{ item.model }} release {{ item.release }} serialNumber {{ item.serialNumber }}"
        loop: "{{ info | json_query(q1) }}"
        vars:
          q1: "[*].{ ipAddress: ipAddress, model: model, release: release, logicalName: logicalName serialNumber: serialNumber }"
        loop_control:
          label: device_info
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
