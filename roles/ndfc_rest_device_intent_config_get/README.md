# ndfc_rest_device_intent_config_get

Retrieve intended config for ``device_name``

### Role Variables

Variable           | Type   | Description
-------------------|--------|------------
device_name        | str()  | Device ``name`` in devices dictionary in ndfc_common/vars/main.yml

Default values for the following variables are set in ``./roles/ndfc_rest_config_deploy/defaults/main.yml``:

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | default, false
inclAllMSDSwitches | bool() | default, false

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_device_intent_config_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - name: debug device_intent_config
      debug:
        var: device_intent_config
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
