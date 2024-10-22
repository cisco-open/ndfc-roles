# ndfc_policy_vrf_rt_import_evpn_loop

Import vrf ``import_vrf_name``'s route-targets into vrf ``vrf_name`` on multiple devices in fabric ``fabric_name`` using Ansible state ``state``

NOTE 1: This role will fail the first time it's run, but is written to retry and will succeed on the second retry.  This is offered as a hack until the DCNM Ansible Collection provides a way to configure route-target import/export within the dcnm_vrf module (or some other yet-to-be-created module).

NOTE 2: This role isn't needed when route-target imports are added to a VRF's config.  See the following.

- [./inventory/group_vars/README.md](/inventory/group_vars/README.md)
- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

## Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | string | The fabric in which ``device_name`` resides (see devices list below).  NOTE: if ``device_name`` resides in a child fabric of an MSD fabric, then ``fabric_name`` must be the name of the MSD fabric.
vrf_name        | string | The vrf into which ``import_vrf_name``'s route-targets will be imports
import_vrf_name | string | The vrf whose route-targets will be imported into ``vrf_name``
state           | string | The Ansible state to apply for the import. e.g. ``deleted`` to delete the import, ``merged`` to merge the import.  NOTE: ``replaced`` is not a valid state for this module.
device_list     | list   | An Ansible list of ``device_name`` to which ``vrf_name`` is attached

Fabric, device and VRF parameters are defined in the following files.

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)
- [./inventory/group_vars/ndfc/02_devices.yml](/inventory/group_vars/ndfc/02_devices.yml)
- [./inventory/group_vars/ndfc/04_vrfs.yml](/inventory/group_vars/ndfc/04_vrfs.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

The example below performs a bi-directional import of route-targets between vrfs v1 and v2 on four leaf devices in fabric f1.

```yaml
---
# Import vrf v2 route-targets into vrf v1 on four leaf devices
- hosts: ndfc
  name: Import vrf v2 route-targets into vrf v1
  gather_facts: false
  vars:
    state: merged
    vrf_name: v1
    import_vrf_name: v2
    device_list:
      - leaf_1
      - leaf_2
      - leaf_3
      - leaf_4
  roles:
    - ndfc_policy_vrf_rt_import_evpn_loop

# Deploy
- hosts: ndfc
  name: deploy and save configs
  gather_facts: false
  roles:
    - ndfc_rest_config_deploy_all
  vars:
    fabric_name: f1

# Import vrf v1 route-targets into vrf v2 on four leaf devices
- hosts: ndfc
  name: Import vrf v1 route-targets into vrf v2
  gather_facts: false
  vars:
    state: merged
    vrf_name: v2
    import_vrf_name: v1
    device_list:
      - leaf_1
      - leaf_2
      - leaf_3
      - leaf_4
  roles:
    - ndfc_policy_vrf_rt_import_evpn_loop

# Deploy
- hosts: ndfc
  name: deploy and save configs
  gather_facts: false
  roles:
    - ndfc_rest_config_deploy_all
  vars:
    fabric_name: f1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
