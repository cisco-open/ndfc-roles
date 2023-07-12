# ndfc_service_route_peering_config_get

Retrieve configuration for ``service_route_peering_name`` from the Ansible inventory

### Role Variables

Variable                   | Type   | Description
---------------------------|--------|----------------------------------------
service_route_peering_name | string | The service route peering for which local configuration information is retrieved

Service route peerings are defined in the following file under ``service_route_peerings`

- [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_route_peering_config_get
  vars:
    service_route_peering_name: srp_1
  tasks:
  - block:
    - name: debug service_route_peering_config
      debug:
        var: service_route_peering_config
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
