# ndfc_rest_interface_no_shutdown

Administratively no shutdown interface ``interface_name`` on ``device_name`` in fabric ``fabric_name``.

### Role Variables

Variable        | Type  | Description
----------------|-------|------------------------------------------------
device_name     | str() | The device on which ``interface_name`` resides
fabric_name     | str() | The fabric in which ``device_name`` resides
interface_name  | str() | The interface on ``device_name`` to no shutdown

Device and Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

Other variables used in this Role:

From ``./roles/ndfc_devices_merged/defaults/main.yml``:

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | bool() | Default: ``false`` Included in the config-deploy REST call payload.

### Dependencies

### Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_interface_no_shutdown
  vars:
    - fabric_name: f1
      device_name: spine_1
      interface_name: Ethernet1/1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
