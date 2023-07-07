# group_vars

Contains vars required by ndfc_* roles

### Requirements

json_query (``pip install jmespath``)

### 01_fabrics.yml

#### lan_classic_fabrics

A list of dictionaries with the following structure:

Variable               | Example        | Type       | Description
-----------------------|----------------|------------|-------------------
name                   | my_lan_fabric  | string     | Fabric name
LOOPBACK0_IP_RANGE     | 10.201.0.0/22  | string     | prefix/mask defining DCI loopback address range
IS_READ_ONLY           | false          | boolean    | If ``true`` the fabric will be created in monitor mode and no edits can be made to it.  If ``false``, the fabric will be created in read/write mode.

##### Example

```yaml
lan_classic_fabrics:
  my_lan_classic_fabric:
    name: my_lan_classic_fabric
    LOOPBACK0_IP_RANGE: 10.37.0.0/22
    IS_READ_ONLY: false
```

#### switch_fabrics

A dictionary of dictionaries with the following structure:

Variable              | Example       | Type        | Description
----------------------|---------------|-------------|-------------------
name                  | fabric_1      | string      | Fabric name
type                  | switch        | string      | the type of fabric
BGP_AS                | 65001         | string      | Fabric BGP autonomous system number
ANYCAST_RP_IP_RANGE   | 10.254.1.0/24 | net/prefix  | Fabric PIM RP. Set only if REPLICATION_MODE == Multicast
LOOPBACK0_IP_RANGE    | 10.2.0.0/22   | net/prefix  | Loopback for routing protocols (OSPF/BGP)
LOOPBACK1_IP_RANGE    | 10.3.0.0/22   | net/prefix  | Loopback for VTEP, associated with nve1 interface
SUBNET_RANGE          | 10.4.0.0/16   | net/prefix  | Inter-device links e.g. spine-leaf
FABRIC_MTU            | 1500          | integer     | Packet Maximum Transfer Unit within the fabric
REPLICATION_MODE      | Multicast     | string      | Replication mode of the fabric. Multicast or Ingress.
ENABLE_PVLAN          | false         | boolean     | Mandatory. enable/disable PVLAN
ENABLE_PVLAN_PREV     | false         | boolean     | Mandatory. enable/disable PVLAN

##### Example

```yaml
switch_fabrics:
  f1:
    name: f1
    type: switch
    BGP_AS: 65001
    #ANYCAST_RP_IP_RANGE: 10.254.1.0/24
    LOOPBACK0_IP_RANGE: 10.2.0.0/22
    LOOPBACK1_IP_RANGE: 10.3.0.0/22
    SUBNET_RANGE: 10.4.0.0/16
    FABRIC_MTU: 9216
    REPLICATION_MODE: Ingress
    ENABLE_PVLAN: false
    ENABLE_PVLAN_PREV: false
  f2:
    name: f2
    type: switch
    BGP_AS: 65002
    #ANYCAST_RP_IP_RANGE: 10.254.1.0/24
    LOOPBACK0_IP_RANGE: 10.6.0.0/22
    LOOPBACK1_IP_RANGE: 10.7.0.0/22
    SUBNET_RANGE: 10.8.0.0/16
    FABRIC_MTU: 9216
    REPLICATION_MODE: Ingress
    ENABLE_PVLAN: false
    ENABLE_PVLAN_PREV: false
```

#### msd_fabrics

A list of dictionaries with the following structure:

Variable              | Example        | Type       | Description
----------------------|----------------|-----------|-------------------
name                  | fabric_1       | string     | Fabric name
ANYCAST_GW_MAC        | 2020.0000.00aa | string     | Shared mac-address for all leafs
BORDER_GWY_CONNECTIONS | Direct_To_BGWS | string    | The type of BGP peering within the MSD fabric.  Valid options: ``Manual``, ``Direct_To_BGWS``, ``Centralized_To_Route_Server``
DCI_SUBNET_RANGE      | 10.100.1.0/24 | net/prefix | Range of IPv4 addresses to use for inter-device links within the MSD fabric
DCI_SUBNET_TARGET_MASK | 30            | integer     | Subnet mask to use for inter-device links within the MSD fabric. min: 8, max: 31
DELAY_RESTORE         | 300            | integer     | Multi-Site underlay and overlay control plane convergence time in seconds.  min: 30, max: 1000
L2_SEGMENT_ID_RANGE   | 30000-49000    | string      | Range for L2 VNIs. min: 1, max: 16777214
L3_PARTITION_ID_RANGE | 50000-59000    | string      | Range for L3 VNIs. min: 1, max: 16777214
LOOPBACK100_IP_RANGE  | 10.100.0.0/24  | net/prefix | range for BGW loopback interfaces associated with multisite
MS_LOOPBACK_ID        | 100            | integer      | loopback ID for the multisite loopback interface. min: 0, max: 1023
MS_UNDERLAY_AUTOCONFIG | true          | boolean     | Enable ``true`` or disable ``false`` the multi-site underlay autoconfiguration

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


#### external_fabrics

A list of dictionaries with the following structure:

Variable               | Example        | Type      | Description
-----------------------|----------------|-----------|-------------------
name                   | ext_fabric_1   | string    | Fabric name
BGP_AS                 | 65201          | string    | Fabric BGP ASN
DCI_SUBNET_RANGE       | 10.101.1.0/24  | string    | prefix/mask defining DCI subnet address range
DCI_SUBNET_TARGET_MASK | 30             | integer   | subnet mask for DCI subnets
LOOPBACK0_IP_RANGE     | 10.201.0.0/22  | string    | prefix/mask defining DCI loopback address range
POWER_REDUNDANCY_MODE  | ps-redundant   | string    | ps-redundant,combined,insrc-redundant
SUBINTERFACE_RANGE     | 2-512          | string    | Per Border Dot1q Range For VRF Lite Connectivity (Min:2, Max:4093)

##### Example

```yaml
external_fabrics:
- name: sn_fabric_1
  BGP_AS: 65201
  DCI_SUBNET_RANGE: 10.101.1.0/24
  DCI_SUBNET_TARGET_MASK: 30
  LOOPBACK0_IP_RANGE: 10.201.0.0/22
  POWER_REDUNDANCY_MODE: ps-redundant
  SUBINTERFACE_RANGE: 2-511
```

### 02_devices.yml

#### devices
A dictionary of dictionaries
The dictionaries all have the same format.

For purposes of example, an explicit fabric name is given below, but it's recommended that the jinja2 template is used to reference the fabric name in the fabrics dictionary to avoid unnecessary repetition of variable names.

Variable              | Example       | Type       | Description
----------------------|---------------|------------|-------------------
ip                    | 192.168.1.1   | string     | switch mgmt0 ip address
msd_fabric            | MSD_1         | string     | MSD fabric in which the switch resides
name                  | leaf_1        | string     | switch name
preserve_config       | false         | boolean    | If false, write erase the config during device discovery
role                  | leaf          | string     | The role of the switch.
switch_fabric         | fabric_1      | string     | Fabric in which the switch resides

##### Example

```yaml
devices:
  # lan_classic fabric LC_1
  # preserve_config must be set to True for LAN Classic fabrics
  leaf_1_LC_1:
    name: leaf_1_LC_1
    switch_fabric: "{{ lan_classic_fabrics.LC_1.name }}"
    ip: 172.22.150.99
    role: leaf
    preserve_config: true
  # switch_fabric f1
  leaf_1:
    name: leaf_1
    switch_fabric: "{{ switch_fabrics.f1.name }}"
    msd_fabric: "{{ msd_fabrics.MSD.name }}"
    ip: 172.22.150.102
    role: leaf
    preserve_config: false
  leaf_2:
    name: leaf_2
    switch_fabric: "{{ switch_fabrics.f1.name }}"
    msd_fabric: "{{ msd_fabrics.MSD.name }}"
    ip: 172.22.150.103
    role: leaf
    preserve_config: false
```


### 03_networks.yaml

#### port_groups

Dictionary containing lists of ports to which networks are attached.  These are referenced with the ``networks`` dictionary

##### Example

```yaml
port_groups:
  pg11:
  - Port-channel11
  pg12:
  - Port-channel12
```

#### networks

Dictionary of dictionaries which define networks and their attachments (device + port_group).

Variable              | Example        | Type         | Description
----------------------|----------------|--------------|-------------------
fabric                | f1             | string       | Fabric in which network resides
net_name              | network_1      | string       | name of the network
vrf_name              | vrf_1          | string       | vrf in which network resides
vlan_id               | 45             | integer      | vlan associated with the network
gw_ip_subnet          | 10.1.1.1/24    | net/prefix   | gateway IP for the network
attach                | See example    | list of dict | List of dictionaries defining the attachment
attach.ip_address     | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the network is attached
attach.ports          | See example    | list         | list of ports on the switch to which the network is attached


##### Example

Below, network n1111 (10.21.1.0/24), with gateway 10.21.1.1, in fabric f1, is connected to four leafs on port port-channel11 on each leaf, within vrf v1.

```yaml
networks:
  f1_n1111:
    name: f1_n1111 # name must be unique across all fabrics
    fabric: "{{ switch_fabrics.f1.name }}"
    net_name: n1111 # can be the same across fabrics
    vrf_name: v1
    vlan_id: 1111
    gw_ip_subnet: "10.21.1.1/24"
    tag: 12345 # used in service_route_peerings
    attach:
      - ip_address: "{{ devices.leaf_1.ip }}"
        ports: "{{ port_groups.pg11 }}"
      - ip_address: "{{ devices.leaf_2.ip }}"
        ports: "{{ port_groups.pg11 }}"
      - ip_address: "{{ devices.leaf_3.ip }}"
        ports: "{{ port_groups.pg11 }}"
      - ip_address: "{{ devices.leaf_4.ip }}"
        ports: "{{ port_groups.pg11 }}"

  f1_n1112:
    name: f1_n1112
    fabric: "{{ switch_fabrics.f1.name }}"
    net_name: n1112
    vrf_name: v2
    vlan_id: 1112
    gw_ip_subnet: "10.22.1.1/24"
    tag: 12345
    attach:
      - ip_address: "{{ devices.leaf_1.ip }}"
        ports: "{{ port_groups.pg12 }}"
      - ip_address: "{{ devices.leaf_2.ip }}"
        ports: "{{ port_groups.pg12 }}"
      - ip_address: "{{ devices.leaf_3.ip }}"
        ports: "{{ port_groups.pg12 }}"
      - ip_address: "{{ devices.leaf_4.ip }}"
        ports: "{{ port_groups.pg12 }}"
```

### 04_vrfs.yml

#### vrfs

Dictionary of dictionaries which define VRFs and their attachments (device).
This follows the same property names and (more or less) the general structure as the corresponding Ansible [cisco.dcnm_vrf](https://github.com/CiscoDevNet/ansible-dcnm/blob/main/docs/cisco.dcnm.dcnm_vrf_module.rst) module.

Variable               | Example        | Type          | Description
-----------------------|----------------|---------------|-------------------
fabric                 | f1             | string        | Fabric in which vrf resides
vrf_name               | vrf_1          | string        | name of the vrf
vrf_id                 | 9003031        | integer       | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | integer       | vrf associated vlan 
vrf_template           | TemplateVrf    | string        | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | string        | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | string        | Service vrf template
attach                 | See example    | list of dict  | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address    | mgmt0 address of the switch to which the vrf is attached

##### Example
```yaml
vrfs:
  f1_v1:
    name: f1_v1
    fabric: "{{ switch_fabrics.f1.name }}"
    vrf_name: v1
    vrf_id: 63031
    vlan_id: 3031
    # You could explicitely list these as well...
    # import_vpn_rt: 65001:63031,65002:63032
    # import_evpn_rt: 65001:63031,65002:63032
    import_vpn_rt: "{{ switch_fabrics.f1.BGP_AS }}:63031,{{ switch_fabrics.f2.BGP_AS }}:63032"
    import_evpn_rt: "{{ switch_fabrics.f1.BGP_AS }}:63031,{{ switch_fabrics.f2.BGP_AS }}:63032"
    vrf_template: Default_VRF_Universal
    vrf_extension_template: Default_VRF_Extension_Universal
    service_vrf_template: null
    attach:
    - ip_address: "{{ devices.leaf_1.ip }}"
    - ip_address: "{{ devices.leaf_2.ip }}"
    - ip_address: "{{ devices.leaf_3.ip }}"
    - ip_address: "{{ devices.leaf_4.ip }}"

  f1_v2:
    name: f1_v2
    fabric: "{{ switch_fabrics.f1.name }}"
    vrf_name: v2
    vrf_id: 63032
    vlan_id: 3032
    import_vpn_rt: "{{ switch_fabrics.f1.BGP_AS }}:63031,{{ switch_fabrics.f2.BGP_AS }}:63032"
    import_evpn_rt: "{{ switch_fabrics.f1.BGP_AS }}:63031,{{ switch_fabrics.f2.BGP_AS }}:63032"
    vrf_template: Default_VRF_Universal
    vrf_extension_template: Default_VRF_Extension_Universal
    service_vrf_template: null
    attach:
    - ip_address: "{{ devices.leaf_1.ip }}"
    - ip_address: "{{ devices.leaf_2.ip }}"
    - ip_address: "{{ devices.leaf_3.ip }}"
    - ip_address: "{{ devices.leaf_4.ip }}"
```

### 05_vpc.yml

#### vpc_peers

Variable            | Example        | Type         | Description
--------------------|----------------|--------------|-------------------
vpc_name            | vpc_1          | string       | name of the VPC peering relationship
peer_1              | leaf_1         | string       | Name of vpc peer 1 (from devices dictionary)
peer_2              | leaf_2         | string       | Name of vpc peer 2 (from devices dictionary)

##### Example

```yaml
vpc_peers:
  vpc_1:
    vpc_name: vpc_1
    peer_1: leaf_1
    peer_2: leaf_2
  vpc_2:
    vpc_name: vpc_2
    peer_1: leaf_3
    peer_2: leaf_4
```

#### vpc_interfaces

Variable               | Example          | Type    | Description
-----------------------|------------------|---------|-------------------
bpdu_guard             | true             | boolean | Enable (true) or disable (false) BPDU guard
interface_mode         | trunk            | string  | The switchport mode of the interface e.g. trunk, access
member_list            | [ Ethernet1/11 ] | list    | An Ansible list of NX-OS interface names
mtu                    | 1500             | string  | The MTU of the interface. Valid values: "jumbo" or integer e.g. 1500
port_channel_mode      | active           | string  | The channel-group mode of the interface e.g. active, on, passive
vpc_name               | vpc_1            | string  | name of the VPC peering relationship
vpc_port_id            | vpi11            | string  | User-provided name.  Can be used in playbooks to merge a specific vpc_port_id
peer1_allowed_vlans    | 1111             | string  | Valid values: none, all, or comma-separated list of allowed vlans e.g. 2-11,12,45-50
peer2_allowed_vlans    | 1111             | string  | Valid values: none, all, or comma-separated list of allowed vlans e.g. 2-11,12,45-50

##### Example

```yaml
vpc_interfaces:
  vpci_1111:
    vpc_name: vpc_1
    vpc_port_id: vpi11
    interface_mode: trunk
    mtu: jumbo
    port_type_fast: true
    bpdu_guard: true 
    port_channel_mode: active 
    peer1_allowed_vlans: 1111
    peer2_allowed_vlans: 1111
    member_list:
    - Ethernet1/11

  vpci_1112:
    vpc_name: vpc_1
    vpc_port_id: vpi12
    interface_mode: trunk
    mtu: jumbo
    port_type_fast: true
    bpdu_guard: true
    port_channel_mode: active
    peer1_allowed_vlans: 1112
    peer2_allowed_vlans: 1112
    member_list:
    - Ethernet1/12
```

### 06_service_nodes.yml

List of dictionaries which define Service Nodes

Variable              | Example            | Type   | Description
----------------------|--------------------|--------------|-------------------
external_fabric_name  | ext_fabric_1       | string  | External Fabric in which service node resides
service_node_type     | Firewall           | string  | Valid values: Firewall, ADC, VNF
service_node_form_factor | Virtual         | string  | Valid values: Physical, Virtual
service_node_peer_name | foo               | string  | Name of the service node peer
service_node_interface_name | Eth1/1       | string  | interface on the service node used for peering
attached_fabric_name   | f1                | string  | fabric in which ``attached_switch_name`` resides
attached_switch_name   | leaf_1            | string  | name of the switch attached to service node
attached_switch_interface_name | Eth1/5    | string  | name of the interface on ``attached_switch_name`` connecting to service node
vpc_switches_attached | false              | boolean | Is service node attached to VPC switches?
link_template_name    | service_link_trunk | string  | Template used to configure ``attached_switch_interface_name`` 
interface_speed       | Auto               | string  | Speed of ``attached_switch_interface_name``
interface_mtu         | jumbo              | string  | MTU of ``attached_switch_interface_name``
interface_allowed_vlans | all              | string  | Valid values: all, none. Allowed vlans on ``attached_switch_interface_name``
interface_bpduguard_enabled | true         | boolean | Enable BPDU guard on ``attached_switch_interface_name``
interface_porttype_fast_enabled | false    | boolean | Enable port fast on ``attached_switch_interface_name``
interface_admin_state | true               | boolean | Admin state for ``attached_switch_interface_name``

##### Example

```yaml
service_nodes:
- service_node_name: "sn_1"
  external_fabric_name: "ext_fabric_1"
  service_node_type: "Firewall"
  service_node_form_factor: "Virtual"
  service_node_peer_name: "foo"
  service_node_interface_name: "eth0"
  attached_fabric_name: "f1"
  attached_switch_name: "leaf_1"
  attached_switch_interface_name: "Ethernet1/5"
  vpc_switches_attached: false
  link_template_name: "service_link_trunk"
  interface_speed: "Auto"
  interface_mtu: "jumbo"
  interface_allowed_vlans: "all"
  interface_bpduguard_enabled: true
  interface_porttype_fast_enabled: true
  interface_admin_state: true
```


### Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) for full text.

### Author Information

Allen Robel (@packetcalc)
