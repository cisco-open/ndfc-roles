# ndfc_policy_vrf_rt_import_loop

Import vrf ``import_vrf_name``'s route-targets into vrf ``vrf_name`` on multiple devices in fabric ``fabric_name`` using Ansible state ``state``


### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | str()  | The fabric in which ``device_name`` resides
vrf_name        | str()  | The vrf into which ``import_vrf_name``'s route-targets will be imports
import_vrf_name | str()  | The vrf whose route-targets will be imported into ``vrf_name``
state           | str()  | The Ansible state to apply for the import. e.g. ``deleted`` to delete the import, ``merged`` to merge the import, etc.
devices         | list() | An Ansible list of ``device_name`` to which ``vrf_name`` is attached

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
    fabric_name: f1
    vrf_name: v1
    import_vrf_name: v2
    devices:
      - leaf_1
      - leaf_2
      - leaf_3
      - leaf_4
  roles:
    - ndfc_policy_vrf_rt_import_loop

# Deploy
- hosts: ndfc
  name: deploy and save configs
  gather_facts: false
  roles:
    - ndfc_config_deploy_all_rest
  vars:
    fabric_name: f1

# Import vrf v1 route-targets into vrf v2 on four leaf devices
- hosts: ndfc
  name: Import vrf v1 route-targets into vrf v2
  gather_facts: false
  vars:
    state: merged
    fabric_name: f1
    vrf_name: v2
    import_vrf_name: v1
    devices:
      - leaf_1
      - leaf_2
      - leaf_3
      - leaf_4
  roles:
    - ndfc_policy_vrf_rt_import_loop

# Deploy
- hosts: ndfc
  name: deploy and save configs
  gather_facts: false
  roles:
    - ndfc_config_deploy_all_rest
  vars:
    fabric_name: f1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
