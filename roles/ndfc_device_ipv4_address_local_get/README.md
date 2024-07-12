# ndfc_device_ipv4_address_local_get

Return device's ipv4 address from the local Ansible inventory, given ``device_name``.

The device's ipv4 address is returned in the variable ``device_ipv4_address``.

``device_ipv4_address`` is gleaned locally from [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml).

Since this operation is local, the result is returned faster than ``ndfc_device_ipv4_address_remote_get``

SEE ALSO: ``ndfc_device_ipv4_address_remote_get``

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
device_name     | string | The device to be queried

Fabric and device parameters are defined in the following files:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

```yaml
# Query ./inventory/group_vars/ndfc/02_devices.yml for fabric_name + device_name
# and print the device's ipv4 address
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_ipv4_address_local_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        msg: "device_ipv4_address: {{ device_ipv4_address }}"
    when: "device_ipv4_address != ''"
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
