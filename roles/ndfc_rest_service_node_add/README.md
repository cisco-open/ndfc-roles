# ndfc_rest_service_node_add

Create servie node ``service_node_name``

NOTE, service_node_type values are different between Ansible module
dcnm_service_node and the REST API ``/appcenter/cisco/ndfc/api/v1/elastic-service/fabrics/{fabric-name}/service-nodes``

Since ndfc-roles offers roles based on both, you need to ensure
that you're using the correct service_node_type values in ``ndfc_common/vars/main.yml``,
per below (these are case-sensitive):

Role                        | service_node_type
----------------------------|----------------------------------------
ndfc_rest_service_node_add  | Firewall, ADC, VNF
ndfc_service_node_create    | firewall, load_balancer, virtual_network_function

### Role Variables

Variable          | Type  | Description
------------------|-------|----------------------------------------
service_node_name | str() | The service node to add

Service node parameters are defined in the following file under ``service_nodes`

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)

### Default Variables

Defaults for the following are in ``./roles/ndfc_rest_service_node_add/defaults/main.yml``:

Variable                        | Type   | Description
--------------------------------|--------|----------------------------------------
link_template_name              | str()  | Default: service_link_trunk
vpc_switches_attached           | bool() | Default: false
interface_speed                 | str()  | Default: Auto
interface_mtu                   | str()  | Default: jumbo
interface_allowed_vlans         | str()  | Default: all
interface_bpduguard_enabled     | bool() | Default: true
interface_porttype_fast_enabled | bool() | Default: true
interface_admin_state           | bool() | true

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
