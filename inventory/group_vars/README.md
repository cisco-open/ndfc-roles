# group_vars

Contains vars required by ndfc_* roles

### Requirements

json_query (``pip install jmespath``)

### 01_fabrics.yml

#### lan_classic_fabrics

A dictionary of dictionaries.  Some of the more frequently-used variables are:

TODO: complete this table...

Variable               | Example        | Type       | Description
-----------------------|----------------|------------|-------------------
FABRIC_NAME            | LC_1           | string     | Fabric name
LOOPBACK0_IP_RANGE     | 10.201.0.0/22  | string     | prefix/mask defining DCI loopback address range
IS_READ_ONLY           | false          | boolean    | If ``true`` the fabric will be created in monitor mode and no edits can be made to it.  If ``false``, the fabric will be created in read/write mode.

##### Example

```yaml
lan_classic:
    LC_1:
        FABRIC_NAME: LC_1
        PM_ENABLE: false
        FABRIC_TYPE: External
        FABRIC_TECHNOLOGY: LANClassic
        FF: LANClassic
        PM_ENABLE_PREV: false
        INBAND_MGMT_PREV: false
        FEATURE_PTP_INTERNAL: false
        DEPLOYMENT_FREEZE: false
        LOOPBACK0_IP_RANGE: 10.1.0.0/22
        INBAND_ENABLE_PREV: false
        MGMT_V6PREFIX: 64
        DCI_SUBNET_RANGE: 10.10.1.0/24
        DCI_SUBNET_TARGET_MASK: 30
        ENABLE_NETFLOW_PREV: ""
        DHCP_START_INTERNAL: ""
        DHCP_END_INTERNAL: ""
        MGMT_GW_INTERNAL: ""
        MGMT_PREFIX_INTERNAL: ""
        BOOTSTRAP_MULTISUBNET_INTERNAL: ""
        MGMT_V6PREFIX_INTERNAL: ""
        DHCP_IPV6_ENABLE_INTERNAL: ""
        POWER_REDUNDANCY_MODE: ps-redundant
        MPLS_HANDOFF: false
        MPLS_LB_ID: ""
        AAA_REMOTE_IP_ENABLED: false
        SNMP_SERVER_HOST_TRAP: true
        CDP_ENABLE: false
        ENABLE_NXAPI: false
        ENABLE_NXAPI_HTTP: false
        INBAND_MGMT: false
        FEATURE_PTP: false
        PTP_LB_ID: ""
        PTP_DOMAIN_ID: ""
        FABRIC_FREEFORM: ""
        AAA_SERVER_CONF: ""
        SUBINTERFACE_RANGE: 2-511
        MPLS_LOOPBACK_IP_RANGE: ""
        enableRealTimeBackup: false
        enableScheduledBackup: false
        scheduledTime: ""
        INBAND_ENABLE: false
        DHCP_ENABLE: false
        DHCP_IPV6_ENABLE: ""
        DHCP_START: ""
        DHCP_END: ""
        MGMT_GW: ""
        MGMT_PREFIX: ""
        ENABLE_AAA: false
        BOOTSTRAP_CONF: ""
        BOOTSTRAP_MULTISUBNET: ""
        ENABLE_NETFLOW: false
        NETFLOW_EXPORTER_LIST: ""
        NETFLOW_RECORD_LIST: ""
        NETFLOW_MONITOR_LIST: ""
        IS_READ_ONLY: false
        BOOTSTRAP_ENABLE: false
```

#### easy_fabric

aka. VXLAN/EVPN Fabrics

A dictionary of dictionaries.  Some of the more frequently-used variables are:

TODO: complete this table

Variable              | Example       | Type        | Description
----------------------|---------------|-------------|-------------------
FABRIC_NAME           | fabric_1      | string      | Fabric name
BGP_AS                | 65001         | string      | Fabric BGP autonomous system number
ANYCAST_RP_IP_RANGE   | 10.254.1.0/24 | net/prefix  | Fabric PIM RP. Set only if REPLICATION_MODE == Multicast
LOOPBACK0_IP_RANGE    | 10.2.0.0/22   | net/prefix  | Loopback for routing protocols (OSPF/BGP)
LOOPBACK1_IP_RANGE    | 10.3.0.0/22   | net/prefix  | Loopback for VTEP, associated with nve1 interface
SUBNET_RANGE          | 10.4.0.0/16   | net/prefix  | Inter-device links e.g. spine-leaf
FABRIC_MTU            | 1500          | integer     | Packet Maximum Transfer Unit within the fabric
REPLICATION_MODE      | Multicast     | string      | Replication mode of the fabric. Multicast or Ingress.
ENABLE_PVLAN          | false         | boolean     | Mandatory. enable/disable PVLAN

NOTE: variables below (mis)spelled DEAFULT_* e.g. DEAFULT_QUEUING_POLICY_CLOUDSCALE,
are correct (i.e. NDFC expects these to be spelled incorrectly).  A bug to fix these
was filed, but was Closed with no action taken.

##### Example

```yaml
easy_fabric:
    f1:
        FABRIC_NAME: f1
        BGP_AS: 65001
        SITE_ID: 65001
        OSPF_AREA_ID: 0.0.0.0
        L2_SEGMENT_ID_RANGE: 30000-49000
        L3_PARTITION_ID_RANGE: 50000-59000
        NETWORK_VLAN_RANGE: 2300-2999
        VRF_VLAN_RANGE: 2000-2299
        SUBINTERFACE_RANGE: 2-511
        LOOPBACK0_IP_RANGE: 10.10.0.0/22
        LOOPBACK1_IP_RANGE: 10.11.0.0/22
        SUBNET_RANGE: 10.12.0.0/16
        LOOPBACK0_IPV6_RANGE: ""
        LOOPBACK1_IPV6_RANGE: ""
        V6_SUBNET_RANGE: ""
        SUBNET_TARGET_MASK: 30
        DCI_SUBNET_RANGE: 10.13.0.0/16
        DCI_SUBNET_TARGET_MASK: 30
        SERVICE_NETWORK_VLAN_RANGE: 3000-3199
        ROUTE_MAP_SEQUENCE_NUMBER_RANGE: 1-65534
        FABRIC_MTU: 9216
        L2_HOST_INTF_MTU: 9216
        REPLICATION_MODE: Ingress
        ANYCAST_GW_MAC: 2020.0000.00aa
        CDP_ENABLE: false
        ENABLE_EVPN: true
        ENABLE_NGOAM: true
        ENABLE_TENANT_DHCP: true
        ENABLE_MACSEC: false
        ENABLE_NXAPI: true
        ENABLE_PBR: false
        PM_ENABLE: false
        ENABLE_PVLAN: false
        ENABLE_NETFLOW: false
        ENABLE_VPC_PEER_LINK_NATIVE_VLAN: false
        ENABLE_NXAPI_HTTP: true
        ENABLE_TRM: false
        BOOTSTRAP_ENABLE: false
        BFD_ENABLE: false
        BFD_IBGP_ENABLE: false
        BFD_OSPF_ENABLE: false
        BFD_ISIS_ENABLE: false
        BFD_PIM_ENABLE: false
        BFD_AUTH_ENABLE: false
        DHCP_ENABLE: false
        DHCP_IPV6_ENABLE: ""
        DHCP_START: ""
        DHCP_END: ""
        UNDERLAY_IS_V6: false
        USE_LINK_LOCAL: false
        V6_SUBNET_TARGET_MASK: ""
        LINK_STATE_ROUTING: ospf
        VPC_DELAY_RESTORE_TIME: 60
        RR_COUNT: 2
        BGP_AS_PREV: ""
        PM_ENABLE_PREV: false
        ENABLE_FABRIC_VPC_DOMAIN_ID_PREV: ""
        FABRIC_VPC_DOMAIN_ID_PREV: ""
        LINK_STATE_ROUTING_TAG_PREV: ""
        OVERLAY_MODE_PREV: ""
        ENABLE_PVLAN_PREV: ""
        FABRIC_MTU_PREV: 9216
        L2_HOST_INTF_MTU_PREV: 9216
        DEPLOYMENT_FREEZE: false
        INBAND_MGMT_PREV: false
        BOOTSTRAP_ENABLE_PREV: false
        MGMT_V6PREFIX: 64
        ENABLE_NETFLOW_PREV: ""
        FABRIC_TYPE: Switch_Fabric
        ENABLE_AGENT: false
        AGENT_INTF: eth0
        SSPINE_ADD_DEL_DEBUG_FLAG: Disable
        BRFIELD_DEBUG_FLAG: Disable
        ACTIVE_MIGRATION: false
        FF: Easy_Fabric
        MSO_SITE_ID: ""
        MSO_CONTROLER_ID: ""
        MSO_SITE_GROUP_NAME: ""
        PREMSO_PARENT_FABRIC: ""
        MSO_CONNECTIVITY_DEPLOYED: ""
        ANYCAST_RP_IP_RANGE_INTERNAL: ""
        DHCP_START_INTERNAL: ""
        DHCP_END_INTERNAL: ""
        DHCP_IPV6_ENABLE_INTERNAL: ""
        MGMT_GW_INTERNAL: ""
        MGMT_PREFIX_INTERNAL: ""
        BOOTSTRAP_MULTISUBNET_INTERNAL: ""
        MGMT_V6PREFIX_INTERNAL: ""
        UNNUM_DHCP_START_INTERNAL: ""
        UNNUM_DHCP_END_INTERNAL: ""
        FEATURE_PTP_INTERNAL: false
        SSPINE_COUNT: 0
        SPINE_COUNT: 0
        abstract_feature_leaf: base_feature_leaf_upg
        abstract_feature_spine: base_feature_spine_upg
        abstract_dhcp: base_dhcp
        abstract_multicast: base_multicast_11_1
        abstract_anycast_rp: anycast_rp
        abstract_loopback_interface: int_fabric_loopback_11_1
        abstract_isis: base_isis_level2
        abstract_ospf: base_ospf
        abstract_vpc_domain: base_vpc_domain_11_1
        abstract_vlan_interface: int_fabric_vlan_11_1
        abstract_isis_interface: isis_interface
        abstract_ospf_interface: ospf_interface_11_1
        abstract_pim_interface: pim_interface
        abstract_route_map: route_map
        abstract_bgp: base_bgp
        abstract_bgp_rr: evpn_bgp_rr
        abstract_bgp_neighbor: evpn_bgp_rr_neighbor
        abstract_extra_config_leaf: extra_config_leaf
        abstract_extra_config_spine: extra_config_spine
        abstract_extra_config_tor: extra_config_tor
        abstract_extra_config_bootstrap: extra_config_bootstrap_11_1
        temp_anycast_gateway: anycast_gateway
        temp_vpc_domain_mgmt: vpc_domain_mgmt
        temp_vpc_peer_link: int_vpc_peer_link_po
        abstract_routed_host: int_routed_host
        abstract_trunk_host: int_trunk_host
        L3VNI_MCAST_GROUP: ""
        PHANTOM_RP_LB_ID1: ""
        PHANTOM_RP_LB_ID2: ""
        PHANTOM_RP_LB_ID3: ""
        PHANTOM_RP_LB_ID4: ""
        VPC_PEER_LINK_VLAN: 3600
        VPC_PEER_KEEP_ALIVE_OPTION: management
        VPC_AUTO_RECOVERY_TIME: 360
        VPC_DELAY_RESTORE: 150
        VPC_PEER_LINK_PO: 500
        VPC_ENABLE_IPv6_ND_SYNC: true
        ADVERTISE_PIP_BGP: false
        ENABLE_FABRIC_VPC_DOMAIN_ID: false
        FABRIC_VPC_DOMAIN_ID: ""
        FABRIC_VPC_QOS_POLICY_NAME: ""
        BGP_LB_ID: 0
        NVE_LB_ID: 1
        ANYCAST_LB_ID: ""
        LINK_STATE_ROUTING_TAG: UNDERLAY
        OSPF_AUTH_KEY_ID: ""
        OSPF_AUTH_KEY: ""
        ISIS_LEVEL: ""
        ISIS_P2P_ENABLE: false
        ISIS_AUTH_ENABLE: false
        ISIS_AUTH_KEYCHAIN_NAME: ""
        ISIS_AUTH_KEYCHAIN_KEY_ID: ""
        ISIS_AUTH_KEY: ""
        ISIS_OVERLOAD_ENABLE: false
        ISIS_OVERLOAD_ELAPSE_TIME: ""
        BGP_AUTH_KEY_TYPE: ""
        BGP_AUTH_KEY: ""
        PIM_HELLO_AUTH_KEY: ""
        BFD_AUTH_KEY_ID: ""
        BFD_AUTH_KEY: ""
        IBGP_PEER_TEMPLATE: ""
        IBGP_PEER_TEMPLATE_LEAF: ""
        default_vrf: Default_VRF_Universal
        default_network: Default_Network_Universal
        vrf_extension_template: Default_VRF_Extension_Universal
        network_extension_template: Default_Network_Extension_Universal
        OVERLAY_MODE: config-profile
        default_pvlan_sec_network: ""
        HOST_INTF_ADMIN_STATE: true
        POWER_REDUNDANCY_MODE: ps-redundant
        COPP_POLICY: strict
        HD_TIME: 180
        BROWNFIELD_NETWORK_NAME_FORMAT: Auto_Net_VNI$$VNI$$_VLAN$$VLAN_ID$$
        BROWNFIELD_SKIP_OVERLAY_NETWORK_ATTACHMENTS: false
        STRICT_CC_MODE: false
        AAA_REMOTE_IP_ENABLED: false
        SNMP_SERVER_HOST_TRAP: true
        ANYCAST_BGW_ADVERTISE_PIP: false
        PTP_LB_ID: ""
        PTP_DOMAIN_ID: ""
        MPLS_LB_ID: ""
        TCAM_ALLOCATION: true
        DEAFULT_QUEUING_POLICY_CLOUDSCALE: ""
        DEAFULT_QUEUING_POLICY_R_SERIES: ""
        DEAFULT_QUEUING_POLICY_OTHER: ""
        MACSEC_KEY_STRING: ""
        MACSEC_ALGORITHM: ""
        MACSEC_FALLBACK_KEY_STRING: ""
        MACSEC_FALLBACK_ALGORITHM: ""
        MACSEC_CIPHER_SUITE: ""
        MACSEC_REPORT_TIMER: ""
        STP_ROOT_OPTION: unmanaged
        STP_VLAN_RANGE: ""
        MST_INSTANCE_RANGE: ""
        STP_BRIDGE_PRIORITY: ""
        EXTRA_CONF_LEAF: ""
        EXTRA_CONF_SPINE: ""
        EXTRA_CONF_TOR: ""
        EXTRA_CONF_INTRA_LINKS: ""
        STATIC_UNDERLAY_IP_ALLOC: false
        MPLS_LOOPBACK_IP_RANGE: ""
        ROUTER_ID_RANGE: ""
        VRF_LITE_AUTOCONFIG: Manual
        AUTO_SYMMETRIC_VRF_LITE: false
        AUTO_VRFLITE_IFC_DEFAULT_VRF: false
        AUTO_SYMMETRIC_DEFAULT_VRF: false
        DEFAULT_VRF_REDIS_BGP_RMAP: ""
        DNS_SERVER_IP_LIST: ""
        DNS_SERVER_VRF: ""
        NTP_SERVER_IP_LIST: ""
        NTP_SERVER_VRF: ""
        SYSLOG_SERVER_IP_LIST: ""
        SYSLOG_SEV: ""
        SYSLOG_SERVER_VRF: ""
        AAA_SERVER_CONF: ""
        MGMT_GW: ""
        MGMT_PREFIX: ""
        BOOTSTRAP_MULTISUBNET: ""
        SEED_SWITCH_CORE_INTERFACES: ""
        SPINE_SWITCH_CORE_INTERFACES: ""
        INBAND_DHCP_SERVERS: ""
        UNNUM_BOOTSTRAP_LB_ID: ""
        UNNUM_DHCP_START: ""
        UNNUM_DHCP_END: ""
        ENABLE_AAA: false
        BOOTSTRAP_CONF: ""
        enableRealTimeBackup: ""
        enableScheduledBackup: ""
        scheduledTime: ""
        NETFLOW_EXPORTER_LIST: ""
        NETFLOW_RECORD_LIST: ""
        NETFLOW_MONITOR_LIST: ""
        FABRIC_INTERFACE_TYPE: p2p
        VPC_DOMAIN_ID_RANGE: 1-1000
        FABRIC_VPC_QOS: false
        OSPF_AUTH_ENABLE: false
        BGP_AUTH_ENABLE: false
        GRFIELD_DEBUG_FLAG: Disable
        FEATURE_PTP: false
        MPLS_HANDOFF: false
        ENABLE_DEFAULT_QUEUING_POLICY: false
        INBAND_MGMT: false
        MULTICAST_GROUP_SUBNET: ""
        RP_COUNT: ""
        RP_MODE: ""
        RP_LB_ID: ""
        PIM_HELLO_AUTH_ENABLE: false
        ANYCAST_RP_IP_RANGE: ""
```

#### msd - Multisite Domain Fabrics

A dictionary of dictionaries.  Some of the more frequently-used variables are:

TODO: complete this table

Variable               | Example        | Type       | Description
-----------------------|----------------|-----------|-------------------
FABRIC_NAME            | fabric_1       | string     | Fabric name
ANYCAST_GW_MAC         | 2020.0000.00aa | string     | Shared mac-address for all leafs
BORDER_GWY_CONNECTIONS | Direct_To_BGWS | string     | The type of BGP peering within the MSD fabric.  Valid options: ``Manual``, ``Direct_To_BGWS``, ``Centralized_To_Route_Server``
DCI_SUBNET_RANGE       | 10.100.1.0/24  | net/prefix  | Range of IPv4 addresses to use for inter-device links within the MSD fabric
DCI_SUBNET_TARGET_MASK | 30             | integer     | Subnet mask to use for inter-device links within the MSD fabric. min: 8, max: 31
DELAY_RESTORE          | 300            | integer     | Multi-Site underlay and overlay control plane convergence time in seconds.  min: 30, max: 1000
L2_SEGMENT_ID_RANGE    | 30000-49000    | string      | Range for L2 VNIs. min: 1, max: 16777214
L3_PARTITION_ID_RANGE  | 50000-59000    | string      | Range for L3 VNIs. min: 1, max: 16777214
LOOPBACK100_IP_RANGE   | 10.100.0.0/24  | net/prefix  | range for BGW loopback interfaces associated with multisite
MS_LOOPBACK_ID         | 100            | integer     | loopback ID for the multisite loopback interface. min: 0, max: 1023
MS_UNDERLAY_AUTOCONFIG | true           | boolean     | Enable ``true`` or disable ``false`` the multi-site underlay autoconfiguration

##### Example

```yaml
msd:
    MSD:
        FABRIC_NAME: MSD
        BORDER_GWY_CONNECTIONS: Direct_To_BGWS
        LOOPBACK0_IP_RANGE: 10.2.0.0/22
        LOOPBACK1_IP_RANGE: 10.3.0.0/22
        SUBNET_RANGE: 10.4.0.0/16
        LOOPBACK100_IP_RANGE: 10.10.0.0/24
        MS_LOOPBACK_ID: 100
        DCI_SUBNET_RANGE: 10.10.1.0/24
        DCI_SUBNET_TARGET_MASK: 30
        SITE_ID: 65001
        BGW_ROUTING_TAG: 54321
        BGW_ROUTING_TAG_PREV: 54321
        ANYCAST_GW_MAC: 2020.0000.00aa
        L2_SEGMENT_ID_RANGE: 30000-49000
        L3_PARTITION_ID_RANGE: 50000-59000
        DELAY_RESTORE: 300
        ENABLE_BGP_BFD: false
        ENABLE_BGP_SEND_COMM: false
        ENABLE_BGP_LOG_NEIGHBOR_CHANGE: false
        MS_UNDERLAY_AUTOCONFIG: false
        TOR_AUTO_DEPLOY: false
        ENABLE_PVLAN: false
        default_vrf: Default_VRF_Universal
        default_network: Default_Network_Universal
        vrf_extension_template: Default_VRF_Extension_Universal
        network_extension_template: Default_Network_Extension_Universal
        default_pvlan_sec_network: ""
        ENABLE_PVLAN_PREV: ""
        FABRIC_TYPE: MFD
        FF: MSD
        MSO_CONTROLER_ID: ""
        MSO_SITE_GROUP_NAME: ""
        PREMSO_PARENT_FABRIC: ""
        DCNM_ID: ""
        MS_IFC_BGP_PASSWORD_ENABLE_PREV: ""
        MS_IFC_BGP_AUTH_KEY_TYPE_PREV: ""
        MS_IFC_BGP_PASSWORD_PREV: ""
        RP_SERVER_IP: ""
        BGP_RP_ASN: ""
        ENABLE_RS_REDIST_DIRECT: false
        RS_ROUTING_TAG: ""
        CLOUDSEC_AUTOCONFIG: false
        CLOUDSEC_KEY_STRING: ""
        CLOUDSEC_ALGORITHM: ""
        CLOUDSEC_ENFORCEMENT: ""
        CLOUDSEC_REPORT_TIMER: ""
        MS_IFC_BGP_PASSWORD_ENABLE: false
        MS_IFC_BGP_PASSWORD: ""
        MS_IFC_BGP_AUTH_KEY_TYPE: ""
        enableScheduledBackup: ""
        scheduledTime: ""
```


#### external - External Fabrics

A dictionary of dictionaries.  Some of the more frequently-used variables are:

TODO: complete this table

Variable               | Example        | Type      | Description
-----------------------|----------------|-----------|-------------------
FABRIC_NAME            | ext_fabric_1   | string    | Fabric name
BGP_AS                 | 65201          | string    | Fabric BGP ASN
DCI_SUBNET_RANGE       | 10.101.1.0/24  | string    | prefix/mask defining DCI subnet address range
DCI_SUBNET_TARGET_MASK | 30             | integer   | subnet mask for DCI subnets
LOOPBACK0_IP_RANGE     | 10.201.0.0/22  | string    | prefix/mask defining DCI loopback address range
POWER_REDUNDANCY_MODE  | ps-redundant   | string    | ps-redundant,combined,insrc-redundant
SUBINTERFACE_RANGE     | 2-512          | string    | Per Border Dot1q Range For VRF Lite Connectivity (Min:2, Max:4093)

##### Example

```yaml
external:
    ext_fabric_1:
        FABRIC_NAME: ext_fabric_1
        BGP_AS: 65201
        PM_ENABLE: false
        EXT_FABRIC_TYPE: External Connectivity Network
        PM_ENABLE_PREV: false
        INBAND_MGMT_PREV: false
        FEATURE_PTP_INTERNAL: false
        DEPLOYMENT_FREEZE: false
        LOOPBACK0_IP_RANGE: 10.201.0.0/22
        FABRIC_TYPE: External
        FF: External
        MSO_SITE_ID: ""
        MSO_CONTROLER_ID: ""
        MSO_SITE_GROUP_NAME: ""
        PREMSO_PARENT_FABRIC: ""
        MSO_CONNECTIVITY_DEPLOYED: ""
        INBAND_ENABLE_PREV: false
        MGMT_V6PREFIX: 64
        DCI_SUBNET_RANGE: 10.10.1.0/24
        DCI_SUBNET_TARGET_MASK: 30
        ENABLE_NETFLOW_PREV: ""
        DHCP_START_INTERNAL: ""
        DHCP_END_INTERNAL: ""
        MGMT_GW_INTERNAL: ""
        MGMT_PREFIX_INTERNAL: ""
        BOOTSTRAP_MULTISUBNET_INTERNAL: ""
        MGMT_V6PREFIX_INTERNAL: ""
        DHCP_IPV6_ENABLE_INTERNAL: ""
        POWER_REDUNDANCY_MODE: ps-redundant
        MPLS_HANDOFF: false
        MPLS_LB_ID: ""
        AAA_REMOTE_IP_ENABLED: false
        SNMP_SERVER_HOST_TRAP: true
        CDP_ENABLE: false
        ENABLE_NXAPI: false
        ENABLE_NXAPI_HTTP: false
        INBAND_MGMT: false
        FEATURE_PTP: false
        PTP_LB_ID: ""
        PTP_DOMAIN_ID: ""
        FABRIC_FREEFORM: ""
        AAA_SERVER_CONF: ""
        SUBINTERFACE_RANGE: 2-511
        MPLS_LOOPBACK_IP_RANGE: ""
        enableRealTimeBackup: ""
        enableScheduledBackup: ""
        scheduledTime: ""
        INBAND_ENABLE: false
        DHCP_ENABLE: false
        DHCP_IPV6_ENABLE: ""
        DHCP_START: ""
        DHCP_END: ""
        MGMT_GW: ""
        MGMT_PREFIX: ""
        ENABLE_AAA: false
        BOOTSTRAP_CONF: ""
        BOOTSTRAP_MULTISUBNET: ""
        ENABLE_NETFLOW: false
        NETFLOW_EXPORTER_LIST: ""
        NETFLOW_RECORD_LIST: ""
        NETFLOW_MONITOR_LIST: ""
        IS_READ_ONLY: false
        BOOTSTRAP_ENABLE: false
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
    switch_fabric: "{{ lan_classic.LC_1.name }}"
    ip: 172.22.150.99
    role: leaf
    preserve_config: true
  # switch_fabric f1
  leaf_1:
    name: leaf_1
    switch_fabric: "{{ easy_fabric.f1.name }}"
    msd_fabric: "{{ msd.MSD.name }}"
    ip: 172.22.150.102
    role: leaf
    preserve_config: false
  leaf_2:
    name: leaf_2
    switch_fabric: "{{ easy_fabric.f1.name }}"
    msd_fabric: "{{ msd.MSD.name }}"
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
    fabric: "{{ easy_fabric.f1.name }}"
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
    fabric: "{{ easy_fabric.f1.name }}"
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

Dictionary which define VRFs and their attachments (device).
This follows the same property names and (more or less) the general structure as the corresponding Ansible [cisco.dcnm_vrf](https://github.com/CiscoDevNet/ansible-dcnm/blob/main/docs/cisco.dcnm.dcnm_vrf_module.rst) module.

Variable               | Example        | Type         | Description
-----------------------|----------------|--------------|-------------------
fabric                 | f1             | string       | Fabric in which vrf resides
import_vpn_rt          | 65000:50001    | string       | vpn route-target to import
import_evpn_rt         | 65000:50001    | string       | evpn route-target to import
vrf_name               | vrf_1          | string       | name of the vrf
vrf_id                 | 9003031        | integer      | vrf Layer3 VNI / vn-segment
vlan_id                | 3031           | integer      | vrf associated vlan 
vrf_template           | TemplateVrf    | string       | Overlay VRF Template For Leafs
vrf_extension_template | TemplateExVrf  | string       | Overlay VRF Template For Borders
service_vrf_template   | ServiceVrf     | string       | Service vrf template
attach                 | See example    | list of dict | List of mgmt0 ip addresses of switches on which the VRF is configured
attach.ip_address      | 192.168.1.1    | IP address   | mgmt0 address of the switch to which the vrf is attached

##### Example
```yaml
vrfs:
  f1_v1:
    name: f1_v1
    fabric: "{{ easy_fabric.f1.name }}"
    vrf_name: v1
    vrf_id: 63031
    vlan_id: 3031
    # You could explicitely list these as well...
    # import_vpn_rt: 65001:63031,65002:63032
    # import_evpn_rt: 65001:63031,65002:63032
    import_vpn_rt: "{{ easy_fabric.f1.BGP_AS }}:63031,{{ easy_fabric.f2.BGP_AS }}:63032"
    import_evpn_rt: "{{ easy_fabric.f1.BGP_AS }}:63031,{{ easy_fabric.f2.BGP_AS }}:63032"
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
    fabric: "{{ easy_fabric.f1.name }}"
    vrf_name: v2
    vrf_id: 63032
    vlan_id: 3032
    import_vpn_rt: "{{ easy_fabric.f1.BGP_AS }}:63031,{{ easy_fabric.f2.BGP_AS }}:63032"
    import_evpn_rt: "{{ easy_fabric.f1.BGP_AS }}:63031,{{ easy_fabric.f2.BGP_AS }}:63032"
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
