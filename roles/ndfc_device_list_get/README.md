# ndfc_device_list_get

Retrieve device configuration from the local inventory for all devices in fabric ``fabric_name``

### Returns

A JSON list of objects containing device configurations, including seed_ip, role, password, username.

#### Example structure of returned information:

```json
[
    {
        "seed_ip": "10.1.1.1",
        "role": "leaf",
        "password": "mypassword",
        "username": "admin"
    },
    {
        "seed_ip": "10.1.1.2",
        "role": "spine",
        "password": "mypassword",
        "username": "admin"
    }
]
```

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which devices reside

Device parameters are defined in the following file:

- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_list_get
  vars:
    fabric_name: f1
  tasks:
  - block:
    - debug:
        var: device_list
    when: "device_list != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
