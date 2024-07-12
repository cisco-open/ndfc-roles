# ndfc_device_names_get

Use ``set_fact`` to set a list (``device_names``) of device names matching devices in fabric ``fabric_name`` with role ``role``.

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric name to match
role            | string | The device role to match e.g. leaf, spine, border_gateway

Fabric and device parameters are defined in the following files:

- ./inventory/group_vars/ndfc/01_fabrics.yml
- ./inventory/group_vars/ndfc/02_devices.yml

See the following for details:

[./inventory/group_vars/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_names_get
  vars:
    fabric_name: f1
    role: leaf
  tasks:
  - block:
    - debug:
        msg: "device_names: {{ device_names }}"
    when: "device_names != ''"
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
