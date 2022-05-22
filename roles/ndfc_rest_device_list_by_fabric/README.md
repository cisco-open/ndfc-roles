# ndfc_rest_device_list_by_fabric

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
    - ndfc_rest_device_list_by_fabric
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

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
