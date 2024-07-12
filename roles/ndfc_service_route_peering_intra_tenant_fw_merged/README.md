# ndfc_service_route_peering_intra_tenant_fw_merged

Create intra-tenant service route peering

NOTE 1: This role is not tested (or documented satisfactorily) yet.

## Role Variables

Variable                   | Type  | Description
---------------------------|-------|----------------------------------------
service_route_peering_name | string | The name of the service route peering

Service route peerings are defined in the following file under ``service_route_peerings`

- [./inventory/group_vars/ndfc/06_service_nodes.yml](/inventory/group_vars/ndfc/06_service_nodes.yml)

See the following for details:

[./inventory/group_vars/README.md](/inventory/group_vars/README.md)


## Example Playbook

```yaml
---
- hosts: ndfc
  gather_facts: false
  roles:
    - ndfc_service_route_peering_intra_tenant_fw_merged
  vars:
    service_route_peering_name: srp_1
```

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

## Author Information

Allen Robel (@packetcalc)
