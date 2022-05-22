# ndfc_rest_config_deploy

Issue NDFC POST REST API calls to invoke config-save on ``fabric_name`` and config-deploy on fabric ``fabric_name`` device ``device_name``.

### Role Variables

Default values for the following variables are set in ``./roles/ndfc_config_deploy_all_rest/defaults/main.yml``:

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | default, false
inclAllMSDSwitches | bool() | default, false
device_name        | str()  | Device ``name`` in ndfc_common/vars/main.yml

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_config_deploy
  vars:
    fabric_name: f1
    device_name: leaf_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
