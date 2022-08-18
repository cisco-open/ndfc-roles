# ndfc_device_ipv4_address_remote_get

Query the NDFC controller for device's ipv4 address, given ``device_name``.

The device's ipv4 address is returned in the variable ``device_ipv4_address``.

``device_ipv4_address`` is gleaned from the device itself.

Since this operation involves a query of the NDFC controller, the result is returned slower than ``ndfc_device_ipv4_address_local_get``

SEE ALSO: ``ndfc_device_ipv4_address_local_get``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be queried

Device names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

```yaml
# Query NX-OS switch associated with fabric_name + device_name
# and print device's ipv4 address
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_ipv4_address_remote_get
  vars:
    device_name: leaf_1
  tasks:
  - block:
    - debug:
        msg: "device_ipv4_address: {{ device_ipv4_address }}"
    when: "device_ipv4_address != ''"
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)