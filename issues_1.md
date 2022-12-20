The following example playbook fails (as do similar tasks in other playbooks).

```yaml
- hosts: ndfc
gather_facts: false
roles:
- ndfc_network_replaced_all
vars:
    fabric_name: MSD
```

The error returned is, variously:

```bash
 "Invalid: Fabric mode is not multicast and Multicast Address: 239.1.1.0 is present",

 or 

 "Invalid: Ingress Replication is true and Multicast Address is 239.1.1.0"
```

A workaround is to set ``multicast_group_address: ""`` in roles/ndfc_network_replaced_all/tasks/worker.yml, like so:

```yaml
# ndfc_network_replaced_all/tasks/worker.yml
- name: worker replaced FABRIC {{ network.value.fabric }} NETWORK {{ network.value.net_name }} VRF {{ network.value.vrf_name }} VLAN {{ network.value.vlan_id }} SUBNET {{ network.value.gw_ip_subnet }}"
  cisco.dcnm.dcnm_network:
    fabric: "{{ fabric_name }}"
    state: replaced
    config:
    - net_name: "{{ network.value.net_name }}"
      multicast_group_address: ""
      vrf_name: "{{ network.value.vrf_name }}"
      vlan_id: "{{ network.value.vlan_id }}"
      gw_ip_subnet: "{{ network.value.gw_ip_subnet }}"
      attach: "{{ network.value.attach }}"
  vars:
    ansible_connection: httpapi
```
