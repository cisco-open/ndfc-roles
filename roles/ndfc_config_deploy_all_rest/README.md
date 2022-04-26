# ndfc_config_deploy_all_reset

Issue NDFC POST REST API calls to invoke config-save and config-deploy

### Role Variables

Default values for the following variables are set in ``./roles/ndfc_config_deploy_all_rest/defaults/main.yml``:

Variable           | Type   | Description
-------------------|--------|------------
forceShowRun       | bool() | default, false
inclAllMSDSwitches | bool() | default, false

### Example Playbooks

```
example_ndfc_fabric_create_rest_f1.yml
example_ndfc_config_deploy_all_rest.yml
```

### License

BSD

### Author Information

Allen Robel (@packetcalc)
