# ndfc_config_deploy_all_rest

Issue NDFC POST REST API calls to invoke config-save and config-deploy

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
    - ndfc_config_deploy_all_rest
  vars:
    fabric_name: f1
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
