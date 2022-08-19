# ndfc_device_interface_config_all_get

Query the config for a specific interface across all devices in fabric ``fabric_name``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
fabric_name     | str() | The fabric in which the devices reside
interface_name  | str() | An NX-OS interface name e.g. Ethernet1/12, Port-channel11, Loopback1, etc

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_device_interface_config_all_get
  vars:
    fabric_name: f1
    interface_name: Ethernet1/11
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
