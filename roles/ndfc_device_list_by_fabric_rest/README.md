# ndfc_device_list_by_fabric_rest

Retrieve list of devices in fabric ``fabric_name``

Returns JSON object ``info`` which will be a list of switch dictionaries
if the GET request succeeded, or an empty list if the GET request failed.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric to be queried


### Example Playbook

The playbook below prints the model number and ip address for every switch in fabric f2.

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
          msg: "item.model: {{ item }}"
        loop: "{{ info | json_query(q1) }}"
        vars:
          q1: "[*].model"
      - debug:
          msg: "item.ipAddress: {{ item }}"
        loop: "{{ info | json_query(q2) }}"
        vars:
          q2: "[*].ipAddress"
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
