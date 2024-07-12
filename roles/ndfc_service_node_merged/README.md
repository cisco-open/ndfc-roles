# ndfc_service_node_merged

Create service node ``service_node_name`` using ansible merge operation

NOTE 1: The ansible module ``cisco.dcnm.dcnm_service_node`` does not provide control over the attach interface's configuration, and a few other parameters.  If you require these, see ``ndfc_rest_service_node_add`` instead.

NOTE 2: ``service_node_type`` values are different between Ansible module dcnm_service_node and the REST API ``/appcenter/cisco/ndfc/api/v1/elastic-service/fabrics/{fabric-name}/service-nodes``

Since ndfc-roles offers roles based on both, you need to ensure that you're using the correct ``service_node_type`` values in [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml), per below (these are case-sensitive):

Role                        | service_node_type
----------------------------|----------------------------------------
ndfc_rest_service_node_add  | Firewall, ADC, VNF
ndfc_service_node_merged    | firewall, load_balancer, virtual_network_function

## Role Variables

Variable          | Type   | Description
------------------|--------|----------------------------------------
service_node_name | string | The service node to merge

Service node parameters are defined in the following file:

- [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)

## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_node_merged
  vars:
    service_node_name: sn_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
