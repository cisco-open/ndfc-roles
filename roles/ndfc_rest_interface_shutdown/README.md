# ndfc_rest_interface_shutdown

Administratively shutdown interface ``interface_name`` on ``device_name``.

## Role Variables

Variable        | Type   | Description
----------------|--------|------------------------------------------------
device_name     | string | The device on which ``interface_name`` resides
interface_name  | string | The interface on ``device_name`` to shutdown

Device and interface parameters are defined in the following files:

- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)
- [./inventory/group_vars/ndfc/03_networks.yml](/inventory/group_vars/ndfc/03_networks.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Other variables used in this Role:

From [./roles/ndfc_rest_interface_shutdown/defaults/main.yml](/roles/ndfc_rest_interface_shutdown/defaults/main.yml)

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | Default: ``false`` Included in the config-deploy REST call payload.
inclAllMSDSwitches | bool() | Default: ``false`` Included in the config-deploy REST call payload.

## Dependencies

## Example Playbooks

```yaml
# example_ndfc_rest_interface_shutdown.yml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_interface_shutdown
  vars:
    device_name: spine_1
    interface_name: Ethernet1/32
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
