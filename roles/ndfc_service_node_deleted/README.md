# ndfc_service_node_deleted

Delete service node ``service_node_name`` using ansible deleted operation

NOTE: The ansible module ``cisco.dcnm.dcnm_service_node`` does not provide control over the attach interface's configuration, and a few other parameters.  If you require these, see ``ndfc_rest_service_node_add`` instead.

NOTE, ``service_node_type`` values are different between Ansible module
dcnm_service_node and the REST API ``/appcenter/cisco/ndfc/api/v1/elastic-service/fabrics/{fabric-name}/service-nodes``

Since ndfc-roles offers roles based on both, you need to ensure
that you're using the correct ``service_node_type`` values in ``ndfc_common/vars/main.yml``,
per below (these are case-sensitive):

Role                        | service_node_type
----------------------------|----------------------------------------
ndfc_rest_service_node_add  | Firewall, ADC, VNF
ndfc_service_node_deleted   | firewall, load_balancer, virtual_network_function

### Role Variables

Variable          | Type  | Description
------------------|-------|----------------------------------------
service_node_name | str() | The service node to merge

Service node parameters are defined in the following file under ``service_nodes`

``./roles/ndfc_common/vars/main.yml``)

See the following for details:

[./roles/ndfc_common/README.md](https://github.com/allenrobel/ndfc-roles/tree/master/roles/ndfc_common/README.md)


### Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_node_deleted
  vars:
    service_node_name: sn_1
```

### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
