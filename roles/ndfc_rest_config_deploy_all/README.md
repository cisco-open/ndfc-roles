# ndfc_rest_config_deploy_all

Issue NDFC POST REST API calls to invoke config-save and config-deploy in fabric ``fabric_name``

### Role Variables

Variable           | Type    | Description
-------------------|---------|------------
fabric_name        | string  | The fabric to config-save and config-deploy

Fabric parameters are defined in the following file:

- [./inventory/group_vars/ndfc/01_fabrics.yml](/inventory/group_vars/ndfc/01_fabrics.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

Default values for the following variables are set in [./roles/ndfc_rest_config_deploy_all/defaults/main.yml](/roles/ndfc_rest_config_deploy_all/defaults/main.yml):

Variable           | Type    | Description
-------------------|---------|------------
forceShowRun       | boolean | default, false
inclAllMSDSwitches | boolean | default, false

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
