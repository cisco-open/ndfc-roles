# ndfc_rest_fabric_lan_classic_create

Create LAN_Classic fabric ``fabric_name``

### Role Variables

Variable        | Type   | Description
----------------|--------|----------------------------------------
fabric_name     | str()  | The fabric to be created
IS_READ_ONLY    | bool() | If ``true`` the fabric will be created in monitor mode and no edits can be made to it.  If ``false``, the fabric will be created in read/write mode.

Fabric parameters, including ``fabric_name`, are defined in the following file:

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_fabric_lan_classic_create
  vars:
    fabric_name: my_lan_classic_fabric
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
