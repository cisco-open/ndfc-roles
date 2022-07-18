# ndfc_rest_device_set_role

Set role for device ``device_name``.

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
device_name     | str() | The device to be merged
fabric_name     | str() | The fabric in which ``device_name`` resides
role            | str() | The desired role for ``device_name`` e.g. leaf, spine, border_gateway, etc

Device and Fabric names are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

Other variables used in this Role:

From ``./roles/ndfc_devices_merged/defaults/main.yml``:

Variable        | Type   | Description
----------------|--------|------------
forceShowRun    | bool() | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | bool() | Default: ``false`` Included in the config-deploy REST call payload.

### Dependencies

### Example Playbooks

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_device_set_role
  vars:
    fabric_name: f1
    device_name: spine_1
    role: spine
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
