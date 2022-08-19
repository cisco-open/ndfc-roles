# ndfc_rest_fabric_msd_create

Create Multi-Site Domain (MSD) fabric ``msd_fabric``

### Role Variables

Variable        | Type  | Description
----------------|-------|----------------------------------------
msd_fabric      | str() | The MSD fabric to be created

MSD fabric parameters are defined in the following file under ``msd_fabrics``

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Default Variables

Defaults for the following are in ``./roles/ndfc_rest_fabric_external_create/defaults/main.yml``:

Variable              | Type   | Description
----------------------|--------|----------------------------------------
greenfield_debug_flag | str()  | Default: enable
IS_READ_ONLY          | bool() | Default: false

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_msd_create
  vars:
    msd_fabric: MSD
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
