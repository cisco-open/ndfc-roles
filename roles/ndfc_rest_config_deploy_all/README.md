# ndfc_rest_config_deploy_all

Issue NDFC POST REST API calls to invoke config-save and config-deploy in fabric ``fabric_name``

### Role Variables

Default values for the following variables are set in ``./roles/ndfc_config_deploy_all_rest/defaults/main.yml``:

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | default, false
inclAllMSDSwitches | bool() | default, false

### Example Playbook

```yaml
---
- hosts: ndfc
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
