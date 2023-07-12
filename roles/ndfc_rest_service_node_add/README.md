# ndfc_rest_service_node_add

Create servie node ``service_node_name``

NOTE, service_node_type values are different between Ansible module dcnm_service_node and the REST API ``/appcenter/cisco/ndfc/api/v1/elastic-service/fabrics/{fabric-name}/service-nodes``

Since ndfc-roles offers roles based on both, you need to ensure that you're using the correct service_node_type values in [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml), per below (these are case-sensitive):

Role                        | service_node_type
----------------------------|----------------------------------------
ndfc_rest_service_node_add  | Firewall, ADC, VNF
ndfc_service_node_create    | firewall, load_balancer, virtual_network_function

### Role Variables

Variable          | Type   | Description
------------------|--------|----------------------------------------
service_node_name | string | The service node to add

Service node parameters are defined in the following file:

- [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

### Default Variables

Defaults for the following are in ``./roles/ndfc_rest_service_node_add/defaults/main.yml``:

Variable                        | Type    | Description
--------------------------------|---------|----------------------------------------
link_template_name              | string  | Default: service_link_trunk
vpc_switches_attached           | boolean | Default: false
interface_speed                 | string  | Default: Auto
interface_mtu                   | string  | Default: jumbo
interface_allowed_vlans         | string  | Default: all
interface_bpduguard_enabled     | boolean | Default: true
interface_porttype_fast_enabled | boolean | Default: true
interface_admin_state           | boolean | true

### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_rest_service_node_add
  vars:
    service_node_name: sn_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
