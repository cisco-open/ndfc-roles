# ndfc_policy_vrf_rt_import_evpn_loop

Import vrf ``import_vrf_name``'s route-targets into vrf ``vrf_name`` on multiple devices in fabric ``fabric_name`` using Ansible state ``state``

NOTE: This role will fail the first time it's run, but is written to retry and will succeed on the second retry.  This is offered as a hack until the DCNM Ansible Collection provides a way to configure route-target import/export within the dcnm_vrf module (or some other yet-to-be-created module).

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | str()  | The fabric in which ``device_name`` resides (see devices list below).  NOTE: if ``device_name`` resides in a child fabric of an MSD fabric, then ``fabric_name`` must be the name of the MSD fabric. 
vrf_name        | str()  | The vrf into which ``import_vrf_name``'s route-targets will be imports
import_vrf_name | str()  | The vrf whose route-targets will be imported into ``vrf_name``
state           | str() | The Ansible state to apply for the import. e.g. ``deleted`` to delete the import, ``merged`` to merge the import.  NOTE: ``replaced`` is not a valid state for this module.
device_list     | list() | An Ansible list of ``device_name`` to which ``vrf_name`` is attached

Fabric, device, and vrf names are are defined in the following file:

``./roles/ndfc_common/vars/main.yml``

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Example Playbook

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

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
