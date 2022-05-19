# ndfc_common

Contains vars required by ndfc_* roles

### Requirements

json_query (``pip install jmespath``)

### Role Variables

#### fabrics

A list of dictionaries with the following structure:

Variable              | Example       | Type       | Description
----------------------|---------------|------------|-------------------
name                  | fabric_1      | str()      | Fabric name
BGP_AS                | 65001         | str()      | Fabric BGP autonomous system number
ANYCAST_RP_IP_RANGE   | 10.254.1.0/24 | net/prefix | Fabric PIM RP. Set only if REPLICATION_MODE == Multicast
LOOPBACK0_IP_RANGE    | 10.2.0.0/22   | net/prefix | Loopback for routing protocols (OSPF/BGP)
LOOPBACK1_IP_RANGE    | 10.3.0.0/22   | net/prefix | Loopback for VTEP, associated with nve1 interface
SUBNET_RANGE          | 10.4.0.0/16   | net/prefix | Inter-device links e.g. spine-leaf
FABRIC_MTU            | 1500          | int()      | Packet Maximum Transfer Unit within the fabric
REPLICATION_MODE      | Multicast     | str()      | Replication mode of the fabric. Multicast or Ingress.

##### Example

```yaml
fabrics:
- name: f1
  BGP_AS: 65001
  #ANYCAST_RP_IP_RANGE: 10.254.1.0/24
  LOOPBACK0_IP_RANGE: 10.2.0.0/22
  LOOPBACK1_IP_RANGE: 10.3.0.0/22
  SUBNET_RANGE: 10.4.0.0/16
  FABRIC_MTU: 9216
  REPLICATION_MODE: Ingress
- name: f2
  BGP_AS: 65002
  #ANYCAST_RP_IP_RANGE: 10.254.2.0/24
  LOOPBACK0_IP_RANGE: 10.6.0.0/22
  LOOPBACK1_IP_RANGE: 10.7.0.0/22
  SUBNET_RANGE: 10.8.0.0/16
  FABRIC_MTU: 9216
  REPLICATION_MODE: Ingress
```

#### msd_fabrics

A list of dictionaries with the following structure:

Variable              | Example        | Type       | Description
----------------------|----------------|-----------|-------------------
name                  | fabric_1       | str()     | Fabric name
ANYCAST_GW_MAC        | 2020.0000.00aa | str()     | Shared mac-address for all leafs
BORDER_GWY_CONNECTIONS | Direct_To_BGWS | str()    | The type of BGP peering within the MSD fabric.  Valid options: ``Manual``, ``Direct_To_BGWS``, ``Centralized_To_Route_Server``
DCI_SUBNET_RANGE      | 10.100.1.0/24 | net/prefix | Range of IPv4 addresses to use for inter-device links within the MSD fabric
DCI_SUBNET_TARGET_MASK | 30            | int()     | Subnet mask to use for inter-device links within the MSD fabric
DELAY_RESTORE         | 300            | int()     | Multi-Site underlay and overlay control plane convergence time in seconds.  min: 30, max: 1000
L2_SEGMENT_ID_RANGE   | 30000-49000    | str()      | Range for L2 VNIs. min: 1, max: 16777214
L3_PARTITION_ID_RANGE | 50000-59000    | str()      | Range for L3 VNIs. min: 1, max: 16777214
LOOPBACK100_IP_RANGE  | 10.100.0.0/24  | net/prefix | range for BGW loopback interfaces associated with multisite
MS_LOOPBACK_ID        | 100            | int()      | loopback ID for the multisite loopback interface. min: 0, max: 1023
MS_UNDERLAY_AUTOCONFIG | true          | bool()     | Enable ``true`` or disable ``false`` the multi-site underlay autoconfiguration

##### Example

```yaml
msd_fabrics:
- name: MSD
  ANYCAST_GW_MAC: 2020.0000.00aa
  BORDER_GWY_CONNECTIONS: Direct_To_BGWS
  DELAY_RESTORE: 300
  L2_SEGMENT_ID_RANGE: 30000-49000
  L3_PARTITION_ID_RANGE: 50000-59000
  MS_LOOPBACK_ID: 100
  MS_UNDERLAY_AUTOCONFIG: true
  LOOPBACK100_IP_RANGE: 10.100.0.0/24
  DCI_SUBNET_RANGE: 10.100.1.0/24
  DCI_SUBNET_TARGET_MASK: 30
```

## Device dictionaries

Each of the following, for leaf, spine, border_gateway, are lists of dictionaries.  The dictionaries all have the same format.

For purposes of example, an explicit fabric name is given below, but it's recommended that the jinja2 template is used to reference the fabric name in the fabrics dictionary to avoid unnecessary repetition of variable names.

### leafs


Variable              | Example       | Type       | Description
----------------------|---------------|------------|-------------------
fabric                | fabric_1      | str()      | Fabric in which leaf resides
name                  | leaf_1        | str()      | leaf name
ip                    | 192.168.1.1   | IP address | leaf mgmt0 ip address
role                  | leaf          | str()      | The role of the switch. Must be "leaf"

##### Example

```yaml
leafs:
- fabric: "{{ fabrics[0].name }}" # leaf_1 in fabric f1
  name: leaf_1
  ip: 192.168.1.1
  role: leaf
- fabric: "{{ fabrics[0].name }}" # leaf_2 in fabric f1
  name: leaf_2
  ip: 192.168.1.2
  role: leaf
- fabric: "{{ fabrics[1].name }}"  # leaf_1 in fabric f2
  name: leaf_1
  ip: 192.168.1.3
  role: leaf
```

### spines


Variable              | Example       | Type       | Description
----------------------|---------------|------------|-------------------
fabric                | f2            | str()      | Fabric in which spine resides
name                  | spine_2       | str()      | spine name
ip                    | 192.168.1.5   | IP address | spine mgmt0 ip address
role                  | spine         | str()      | The role of the switch. Must be "spine"

##### Example

```yaml
spines:
- fabric: "{{ fabrics[0].name }}" # spine_1 in fabric f1
  name: spine_1
  ip: 192.168.1.5
  role: spine
- fabric: "{{ fabrics[1].name }}" # spine_1 in fabric f2
  name: spine_1
  ip: 192.168.1.7
  role: spine
```

### border_gateways


Variable              | Example        | Type       | Description
----------------------|----------------|------------|-------------------
fabric                | f1             | str()      | Fabric in which border_gateway resides
name                  | bgw_1          | str()      | border_gateway name
ip                    | 192.168.1.10   | IP address | border_gateway mgmt0 ip address
role                  | border_gateway | str()      | The role of the switch. Must be "border_gateway"

##### Example

```yaml
border_gateways:
- fabric: "{{ fabrics[0].name }}"  # border_gateway_1 in fabric f1
  name: border_gateway_1
  ip: 192.168.1.10
  role: border_gateway
- fabric: "{{ fabrics[1].name }}" # border_gateway_1 in fabric f2
  name: border_gateway_1
  ip: 192.168.1.11
  role: border_gateway
```

### port_groups

Dictionary containing lists of ports to which networks are attached.  These are referenced with the ``networks`` dictionary

##### Example

```yaml
port_groups:
  pg11:
  - Port-channel11
  pg12:
  - Port-channel12
```

### networks

List of dictionaries which define networks and their attachments (device + port_group).

Variable              | Example        | Type         | Description
----------------------|----------------|--------------|-------------------
fabric                | f1             | str()        | Fabric in which network resides
net_name              | network_1      | str()        | name of the network
vrf_name              | vrf_1          | str()        | vrf in which network resides
vlan_id               | 45             | int()        | vlan associated with the network
gw_ip_subnet          | 10.1.1.1/24    | net/prefix   | gateway IP for the network
attach                | See example    | list of dict | List of dictionaries defining the attachment
attach.ip_address     | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the network is attached
attach.ports          | See example    | list         | list of ports on the switch to which the network is attached


##### Example

Below, network n1111 (10.21.1.0/24), with gateway 10.21.1.1, in fabric f1, is connected to four leafs on port port-channel11 on each leaf, within vrf v1.

```yaml
networks:
- fabric: "{{ fabrics[0].name }}" # fabric f1
  net_name: n1111
  vrf_name: v1
  vlan_id: 1111
  gw_ip_subnet: "10.21.1.1/24"
  attach:
  - ip_address: "{{ leafs[0].ip }}" # 192.168.1.1
    ports: "{{ port_groups.pg11 }}" # [ Port-channel11 ]
  - ip_address: "{{ leafs[1].ip }}"
    ports: "{{ port_groups.pg11 }}"

- fabric: "{{ fabrics[1].name }}" # fabric f2
  net_name: n1112
  vrf_name: v2
  vlan_id: 1112
  gw_ip_subnet: "10.22.1.1/24"
  attach:
  - ip_address: "{{ leafs[4].ip }}" # 192.168.1.3
    ports: "{{ port_groups.pg12 }}" # [ Port-channel12 ]
  - ip_address: "{{ leafs[5].ip }}" 
    ports: "{{ port_groups.pg12 }}"
```

### vrfs

List of dictionaries which define VRFs and their attachments (device).
This follows the same property names and (more or less) the general structure as the corresponding Ansible [cisco.dcnm_vrf](https://github.com/CiscoDevNet/ansible-dcnm/blob/main/docs/cisco.dcnm.dcnm_vrf_module.rst) module.

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | str()        | Fabric in which vrf resides
vrf_name               | vrf_1          | str()        | name of the vrf
vrf_id                 | 9003031        | int()        | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | int()        | vrf associated vlan 
vrf_template           | TemplateVrf    | str()        | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | str()        | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | str()        | Service vrf template
attach                 | See example    | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the vrf is attached


```yaml
vrfs:
- fabric: "{{ fabrics[0].name }}"
  vrf_name: v1
  vrf_id: 9003031
  vlan_id: 3031
  vrf_template: Default_VRF_Universal
  vrf_extension_template: Default_VRF_Extension_Universal
  service_vrf_template: null
  attach:
    - ip_address: "{{ leafs[0].ip }}"
    - ip_address: "{{ leafs[1].ip }}"
    - ip_address: "{{ leafs[2].ip }}"
    - ip_address: "{{ leafs[3].ip }}"
```

### vpc_peers

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | str()        | Fabric in which network resides
vpc_name               | vpc_1          | str()        | name of the VPC peering relationship
peer_1_ip              | 192.168.1.1    | ip address   | mgmt0 ip address of the first switch
peer_2_ip              | 192.168.1.2    | ip address   | mgmt0 ip address of the second switch

##### Example

```yaml
vpc_peers:
- fabric: "{{ fabrics[0].name}}" # Fabric f1
  vpc_name: "vpc1"
  peer_1_ip: "{{ leafs[0].ip }}" # 192.168.1.1
  peer_2_ip: "{{ leafs[1].ip }}" # 192.168.1.2
- fabric: "{{ fabrics[0].name}}"
  vpc_name: "vpc2"
  peer_1_ip: "{{ leafs[2].ip }}"
  peer_2_ip: "{{ leafs[3].ip }}"
```

### vpc_interfaces

Variable               | Example          | Type   | Description
-----------------------|------------------|--------|-------------------
fabric                 | f1               | str()  | Fabric in which ``vpc_name`` resides
vpc_name               | vpc_1            | str()  | name of the VPC peering relationship
vpc_port_id            | vpi11            | str()  | User-provided name.  Can be used in playbooks to merge a specific vpc_port_id
interface_mode         | trunk            | str()  | The switchport mode of the interface e.g. trunk, access
port_channel_mode      | active           | str()  | The channel-group mode of the interface e.g. active, on, passive
member_list            | [ Ethernet1/11 ] | list() | An Ansible list of NX-OS interface names

##### Example

```yaml
vpc_interfaces:
- fabric: "{{ fabrics[0].name}}"
  vpc_name: vpc1
  vpc_port_id: vpi11
  interface_mode: trunk
  port_channel_mode: active
  member_list:
  - Ethernet1/11
- fabric: "{{ fabrics[0].name}}"
  vpc_name: vpc2
  vpc_port_id: vpi11
  interface_mode: trunk
  member_list:
  - Ethernet1/11
  port_channel_mode: active
```

### Example Playbook

This role is not called directly.  Other ndfc_* roles include this role in their meta/main.yml files.

### License

BSD

### Author Information

Allen Robel (@packetcalc)
