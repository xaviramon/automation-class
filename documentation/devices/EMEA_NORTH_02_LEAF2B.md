# EMEA_NORTH_02_LEAF2B
# Table of Contents
<!-- toc -->

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [Name Servers](#name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [RADIUS Servers](#radius-servers)
- [Monitoring](#monitoring)
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Virtual Source NAT](#virtual-source-nat)
  - [Virtual Source NAT Summary](#virtual-source-nat-summary)
  - [Virtual Source NAT Configuration](#virtual-source-nat-configuration)
- [Quality Of Service](#quality-of-service)

<!-- toc -->
# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 192.168.0.15/24 | 192.168.0.1 |

#### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | oob_management | oob | MGMT | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   no shutdown
   vrf MGMT
   ip address 192.168.0.15/24
```

## DNS Domain

### DNS domain: atd.lab

### DNS Domain Device Configuration

```eos
!
dns domain atd.lab
!
```

## Name Servers

### Name Servers Summary

| Name Server | Source VRF |
| ----------- | ---------- |
| 1.1.1.1 | MGMT |
| 8.8.8.8 | MGMT |

### Name Servers Device Configuration

```eos
ip name-server vrf MGMT 1.1.1.1
ip name-server vrf MGMT 8.8.8.8
```

## NTP

### NTP Summary

- Local Interface: Management1

| Node | Primary |
| ---- | ------- |
| 192.168.0.1 | true |

### NTP Device Configuration

```eos
!
ntp local-interface  Management1
ntp server  192.168.0.1 prefer
```

## Management API HTTP

### Management API HTTP Summary

| HTTP | HTTPS |
| ---------- | ---------- |
| default | true |

### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |


### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

# Authentication

## Local Users

### Local Users Summary

| User | Privilege | Role |
| ---- | --------- | ---- |
| admin | 15 | network-admin |
| alumne | 15 | network-admin |

### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin nopassword
username alumne privilege 15 role network-admin secret sha512 THISISATEST
```

## RADIUS Servers

### RADIUS Servers

| VRF | RADIUS Servers |
| --- | ---------------|
|  default | 192.168.0.1 |

### RADIUS Servers Device Configuration

```eos
!
radius-server host 192.168.0.1 key 7 0207165218120E
```

# Monitoring

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| EMEA_NORTH_02_LEAF2 | Vlan4094 | 10.255.252.4 | Port-Channel1 |

Dual primary detection is disabled.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id EMEA_NORTH_02_LEAF2
   local-interface Vlan4094
   peer-address 10.255.252.4
   peer-link Port-Channel1
   reload-delay mlag 300
   reload-delay non-mlag 330
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **mstp**

### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

### Global Spanning-Tree Settings

Spanning Tree disabled for VLANs: **4093-4094**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 4096
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

## Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

# VLANs

## VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 110 | Tenant_A_OP_Zone_DB1 | none  |
| 111 | Tenant_A_OP_Zone_DB2 | none  |
| 120 | Tenant_A_WEB_Zone_1 | none  |
| 121 | Tenant_A_WEB_Zone_2 | none  |
| 130 | Tenant_A_APP_Zone_1 | none  |
| 131 | Tenant_A_APP_Zone_2 | none  |
| 140 | Tenant_A_DB_BZone_1 | none  |
| 141 | Tenant_A_DB_Zone_2 | none  |
| 150 | Tenant_A_WAN_Zone_1 | none  |
| 160 | Tenant_A_VMOTION | none  |
| 161 | Tenant_A_NFS | none  |
| 210 | Tenant_B_OP_Zone_1 | none  |
| 211 | Tenant_B_OP_Zone_2 | none  |
| 250 | Tenant_B_WAN_Zone_1 | none  |
| 3009 | MLAG_iBGP_Common_VRF_Services | LEAF_PEER_L3  |
| 3010 | MLAG_iBGP_Tenant_A_WEB_Zone | LEAF_PEER_L3  |
| 3011 | MLAG_iBGP_Tenant_A_APP_Zone | LEAF_PEER_L3  |
| 3013 | MLAG_iBGP_Tenant_A_WAN_Zone | LEAF_PEER_L3  |
| 3020 | MLAG_iBGP_Tenant_B_WAN_Zone | LEAF_PEER_L3  |
| 3129 | MLAG_iBGP_Tenant_A_DB_Zone | LEAF_PEER_L3  |
| 4093 | LEAF_PEER_L3 | LEAF_PEER_L3  |
| 4094 | MLAG_PEER | MLAG  |

## VLANs Device Configuration

```eos
!
vlan 110
   name Tenant_A_OP_Zone_DB1
!
vlan 111
   name Tenant_A_OP_Zone_DB2
!
vlan 120
   name Tenant_A_WEB_Zone_1
!
vlan 121
   name Tenant_A_WEB_Zone_2
!
vlan 130
   name Tenant_A_APP_Zone_1
!
vlan 131
   name Tenant_A_APP_Zone_2
!
vlan 140
   name Tenant_A_DB_BZone_1
!
vlan 141
   name Tenant_A_DB_Zone_2
!
vlan 150
   name Tenant_A_WAN_Zone_1
!
vlan 160
   name Tenant_A_VMOTION
!
vlan 161
   name Tenant_A_NFS
!
vlan 210
   name Tenant_B_OP_Zone_1
!
vlan 211
   name Tenant_B_OP_Zone_2
!
vlan 250
   name Tenant_B_WAN_Zone_1
!
vlan 3009
   name MLAG_iBGP_Common_VRF_Services
   trunk group LEAF_PEER_L3
!
vlan 3010
   name MLAG_iBGP_Tenant_A_WEB_Zone
   trunk group LEAF_PEER_L3
!
vlan 3011
   name MLAG_iBGP_Tenant_A_APP_Zone
   trunk group LEAF_PEER_L3
!
vlan 3013
   name MLAG_iBGP_Tenant_A_WAN_Zone
   trunk group LEAF_PEER_L3
!
vlan 3020
   name MLAG_iBGP_Tenant_B_WAN_Zone
   trunk group LEAF_PEER_L3
!
vlan 3129
   name MLAG_iBGP_Tenant_A_DB_Zone
   trunk group LEAF_PEER_L3
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet1 | MLAG_PEER_EMEA_NORTH_02_LEAF2A_Ethernet1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 1 |
| Ethernet6 | MLAG_PEER_EMEA_NORTH_02_LEAF2A_Ethernet6 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 1 |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet2 | P2P_LINK_TO_EMEA_NORTH_02_SPINE1_Ethernet5 | routed | - | 172.31.155.25/31 | default | 1500 | false | - | - |
| Ethernet3 | P2P_LINK_TO_EMEA_NORTH_02_SPINE2_Ethernet5 | routed | - | 172.31.155.27/31 | default | 1500 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description MLAG_PEER_EMEA_NORTH_02_LEAF2A_Ethernet1
   no shutdown
   channel-group 1 mode active
!
interface Ethernet2
   description P2P_LINK_TO_EMEA_NORTH_02_SPINE1_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.25/31
!
interface Ethernet3
   description P2P_LINK_TO_EMEA_NORTH_02_SPINE2_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.27/31
!
interface Ethernet6
   description MLAG_PEER_EMEA_NORTH_02_LEAF2A_Ethernet6
   no shutdown
   channel-group 1 mode active
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel1 | MLAG_PEER_EMEA_NORTH_02_LEAF2A_Po1 | switched | trunk | 2-4094 | - | ['LEAF_PEER_L3', 'MLAG'] | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel1
   description MLAG_PEER_EMEA_NORTH_02_LEAF2A_Po1
   no shutdown
   switchport
   switchport trunk allowed vlan 2-4094
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 192.168.155.8/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 192.168.154.7/32 |
| Loopback100 | Common_VRF_Services_VTEP_DIAGNOSTICS | Common_VRF_Services | 10.255.1.8/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |
| Loopback100 | Common_VRF_Services_VTEP_DIAGNOSTICS | Common_VRF_Services | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 192.168.155.8/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 192.168.154.7/32
!
interface Loopback100
   description Common_VRF_Services_VTEP_DIAGNOSTICS
   no shutdown
   vrf Common_VRF_Services
   ip address 10.255.1.8/32
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan110 |  Tenant_A_OP_Zone_DB1  |  Common_VRF_Services  |  9000  |  false  |
| Vlan111 |  Tenant_A_OP_Zone_DB2  |  Common_VRF_Services  |  -  |  true  |
| Vlan120 |  Tenant_A_WEB_Zone_1  |  Tenant_A_WEB_Zone  |  -  |  false  |
| Vlan121 |  Tenant_A_WEB_Zone_2  |  Tenant_A_WEB_Zone  |  -  |  false  |
| Vlan130 |  Tenant_A_APP_Zone_1  |  Tenant_A_APP_Zone  |  -  |  false  |
| Vlan131 |  Tenant_A_APP_Zone_2  |  Tenant_A_APP_Zone  |  -  |  false  |
| Vlan140 |  Tenant_A_DB_BZone_1  |  Tenant_A_DB_Zone  |  -  |  false  |
| Vlan141 |  Tenant_A_DB_Zone_2  |  Tenant_A_DB_Zone  |  -  |  false  |
| Vlan150 |  Tenant_A_WAN_Zone_1  |  Tenant_A_WAN_Zone  |  -  |  false  |
| Vlan210 |  Tenant_B_OP_Zone_1  |  Tenant_B_OP_Zone  |  -  |  false  |
| Vlan211 |  Tenant_B_OP_Zone_2  |  Tenant_B_OP_Zone  |  -  |  false  |
| Vlan250 |  Tenant_B_WAN_Zone_1  |  Tenant_B_WAN_Zone  |  -  |  false  |
| Vlan3009 |  MLAG_PEER_L3_iBGP: vrf Common_VRF_Services  |  Common_VRF_Services  |  1500  |  false  |
| Vlan3010 |  MLAG_PEER_L3_iBGP: vrf Tenant_A_WEB_Zone  |  Tenant_A_WEB_Zone  |  1500  |  false  |
| Vlan3011 |  MLAG_PEER_L3_iBGP: vrf Tenant_A_APP_Zone  |  Tenant_A_APP_Zone  |  1500  |  false  |
| Vlan3013 |  MLAG_PEER_L3_iBGP: vrf Tenant_A_WAN_Zone  |  Tenant_A_WAN_Zone  |  1500  |  false  |
| Vlan3020 |  MLAG_PEER_L3_iBGP: vrf Tenant_B_WAN_Zone  |  Tenant_B_WAN_Zone  |  1500  |  false  |
| Vlan3129 |  MLAG_PEER_L3_iBGP: vrf Tenant_A_DB_Zone  |  Tenant_A_DB_Zone  |  1500  |  false  |
| Vlan4093 |  MLAG_PEER_L3_PEERING  |  default  |  1500  |  false  |
| Vlan4094 |  MLAG_PEER  |  default  |  1500  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan110 |  Common_VRF_Services  |  -  |  10.1.10.1/24  |  -  |  -  |  -  |  -  |
| Vlan111 |  Common_VRF_Services  |  -  |  10.1.11.1/24  |  -  |  -  |  -  |  -  |
| Vlan120 |  Tenant_A_WEB_Zone  |  -  |  10.1.20.1/24  |  -  |  -  |  -  |  -  |
| Vlan121 |  Tenant_A_WEB_Zone  |  -  |  10.1.21.1/24  |  -  |  -  |  -  |  -  |
| Vlan130 |  Tenant_A_APP_Zone  |  -  |  10.1.30.1/24  |  -  |  -  |  -  |  -  |
| Vlan131 |  Tenant_A_APP_Zone  |  -  |  10.1.31.1/24  |  -  |  -  |  -  |  -  |
| Vlan140 |  Tenant_A_DB_Zone  |  -  |  10.1.40.1/24  |  -  |  -  |  -  |  -  |
| Vlan141 |  Tenant_A_DB_Zone  |  -  |  10.1.41.1/24  |  -  |  -  |  -  |  -  |
| Vlan150 |  Tenant_A_WAN_Zone  |  -  |  10.1.40.1/24  |  -  |  -  |  -  |  -  |
| Vlan210 |  Tenant_B_OP_Zone  |  -  |  -  |  -  |  -  |  -  |  -  |
| Vlan211 |  Tenant_B_OP_Zone  |  -  |  -  |  -  |  -  |  -  |  -  |
| Vlan250 |  Tenant_B_WAN_Zone  |  -  |  -  |  -  |  -  |  -  |  -  |
| Vlan3009 |  Common_VRF_Services  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3010 |  Tenant_A_WEB_Zone  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3011 |  Tenant_A_APP_Zone  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3013 |  Tenant_A_WAN_Zone  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3020 |  Tenant_B_WAN_Zone  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan3129 |  Tenant_A_DB_Zone  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4093 |  default  |  10.255.254.5/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  10.255.252.5/31  |  -  |  -  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan110
   description Tenant_A_OP_Zone_DB1
   no shutdown
   mtu 9000
   vrf Common_VRF_Services
   ip address virtual 10.1.10.1/24
   ip helper-address 192.168.1.100 vrf Common_VRF_Services source-interface Vlan110
!
interface Vlan111
   description Tenant_A_OP_Zone_DB2
   shutdown
   vrf Common_VRF_Services
   ip address virtual 10.1.11.1/24
!
interface Vlan120
   description Tenant_A_WEB_Zone_1
   no shutdown
   vrf Tenant_A_WEB_Zone
   ip address virtual 10.1.20.1/24
!
interface Vlan121
   description Tenant_A_WEB_Zone_2
   no shutdown
   vrf Tenant_A_WEB_Zone
   ip address virtual 10.1.21.1/24
!
interface Vlan130
   description Tenant_A_APP_Zone_1
   no shutdown
   vrf Tenant_A_APP_Zone
   ip address virtual 10.1.30.1/24
!
interface Vlan131
   description Tenant_A_APP_Zone_2
   no shutdown
   vrf Tenant_A_APP_Zone
   ip address virtual 10.1.31.1/24
!
interface Vlan140
   description Tenant_A_DB_BZone_1
   no shutdown
   vrf Tenant_A_DB_Zone
   ip address virtual 10.1.40.1/24
!
interface Vlan141
   description Tenant_A_DB_Zone_2
   no shutdown
   vrf Tenant_A_DB_Zone
   ip address virtual 10.1.41.1/24
!
interface Vlan150
   description Tenant_A_WAN_Zone_1
   no shutdown
   vrf Tenant_A_WAN_Zone
   ip address virtual 10.1.40.1/24
!
interface Vlan210
   description Tenant_B_OP_Zone_1
   no shutdown
   vrf Tenant_B_OP_Zone
!
interface Vlan211
   description Tenant_B_OP_Zone_2
   no shutdown
   vrf Tenant_B_OP_Zone
!
interface Vlan250
   description Tenant_B_WAN_Zone_1
   no shutdown
   vrf Tenant_B_WAN_Zone
!
interface Vlan3009
   description MLAG_PEER_L3_iBGP: vrf Common_VRF_Services
   no shutdown
   mtu 1500
   vrf Common_VRF_Services
   ip address 10.255.254.5/31
!
interface Vlan3010
   description MLAG_PEER_L3_iBGP: vrf Tenant_A_WEB_Zone
   no shutdown
   mtu 1500
   vrf Tenant_A_WEB_Zone
   ip address 10.255.254.5/31
!
interface Vlan3011
   description MLAG_PEER_L3_iBGP: vrf Tenant_A_APP_Zone
   no shutdown
   mtu 1500
   vrf Tenant_A_APP_Zone
   ip address 10.255.254.5/31
!
interface Vlan3013
   description MLAG_PEER_L3_iBGP: vrf Tenant_A_WAN_Zone
   no shutdown
   mtu 1500
   vrf Tenant_A_WAN_Zone
   ip address 10.255.254.5/31
!
interface Vlan3020
   description MLAG_PEER_L3_iBGP: vrf Tenant_B_WAN_Zone
   no shutdown
   mtu 1500
   vrf Tenant_B_WAN_Zone
   ip address 10.255.254.5/31
!
interface Vlan3129
   description MLAG_PEER_L3_iBGP: vrf Tenant_A_DB_Zone
   no shutdown
   mtu 1500
   vrf Tenant_A_DB_Zone
   ip address 10.255.254.5/31
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   no shutdown
   mtu 1500
   ip address 10.255.254.5/31
!
interface Vlan4094
   description MLAG_PEER
   no shutdown
   mtu 1500
   no autostate
   ip address 10.255.252.5/31
```

## VXLAN Interface

### VXLAN Interface Summary

#### Source Interface: Loopback1

#### UDP port: 4789

#### VLAN to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| 110 | 10110 |
| 111 | 50111 |
| 120 | 10120 |
| 121 | 10121 |
| 130 | 10130 |
| 131 | 10131 |
| 140 | 10140 |
| 141 | 10141 |
| 150 | 10150 |
| 160 | 55160 |
| 161 | 10161 |
| 210 | 20210 |
| 211 | 20211 |
| 250 | 20250 |

#### VRF to VNI Mappings

| VLAN | VNI |
| ---- | --- |
| Common_VRF_Services | 10 |
| Tenant_A_APP_Zone | 12 |
| Tenant_A_DB_Zone | 130 |
| Tenant_A_WAN_Zone | 14 |
| Tenant_A_WEB_Zone | 11 |
| Tenant_B_OP_Zone | 2000 |
| Tenant_B_WAN_Zone | 21 |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 110 vni 10110
   vxlan vlan 111 vni 50111
   vxlan vlan 120 vni 10120
   vxlan vlan 121 vni 10121
   vxlan vlan 130 vni 10130
   vxlan vlan 131 vni 10131
   vxlan vlan 140 vni 10140
   vxlan vlan 141 vni 10141
   vxlan vlan 150 vni 10150
   vxlan vlan 160 vni 55160
   vxlan vlan 161 vni 10161
   vxlan vlan 210 vni 20210
   vxlan vlan 211 vni 20211
   vxlan vlan 250 vni 20250
   vxlan vrf Common_VRF_Services vni 10
   vxlan vrf Tenant_A_APP_Zone vni 12
   vxlan vrf Tenant_A_DB_Zone vni 130
   vxlan vrf Tenant_A_WAN_Zone vni 14
   vxlan vrf Tenant_A_WEB_Zone vni 11
   vxlan vrf Tenant_B_OP_Zone vni 2000
   vxlan vrf Tenant_B_WAN_Zone vni 21
```

# Routing

## Virtual Router MAC Address

### Virtual Router MAC Address Summary

#### Virtual Router MAC Address: 00:1c:73:00:dc:01

### Virtual Router MAC Address Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:01
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true|| Common_VRF_Services | true |
| MGMT | false |
| Tenant_A_APP_Zone | true |
| Tenant_A_DB_Zone | true |
| Tenant_A_WAN_Zone | true |
| Tenant_A_WEB_Zone | true |
| Tenant_B_OP_Zone | true |
| Tenant_B_WAN_Zone | true |

### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf Common_VRF_Services
no ip routing vrf MGMT
ip routing vrf Tenant_A_APP_Zone
ip routing vrf Tenant_A_DB_Zone
ip routing vrf Tenant_A_WAN_Zone
ip routing vrf Tenant_A_WEB_Zone
ip routing vrf Tenant_B_OP_Zone
ip routing vrf Tenant_B_WAN_Zone
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false || Common_VRF_Services | false |
| MGMT | false |
| Tenant_A_APP_Zone | false |
| Tenant_A_DB_Zone | false |
| Tenant_A_WAN_Zone | false |
| Tenant_A_WEB_Zone | false |
| Tenant_B_OP_Zone | false |
| Tenant_B_WAN_Zone | false |


## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT  | 192.168.0.0/24 |  192.168.0.1  |  -  |  1  |  -  |  -  |  - |
| MGMT  | 0.0.0.0/0 |  192.168.0.1  |  -  |  1  |  -  |  -  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 192.168.0.0/24 192.168.0.1
ip route vrf MGMT 0.0.0.0/0 192.168.0.1
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65102|  192.168.155.8 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| graceful-restart restart-time 300 |
| graceful-restart |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Source | Loopback0 |
| Bfd | true |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65200 |
| Send community | all |
| Maximum routes | 12000 |

#### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65102 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF |
| -------- | --------- | --- |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default |
| 172.31.155.24 | Inherited from peer group IPv4-UNDERLAY-PEERS | default |
| 172.31.155.26 | Inherited from peer group IPv4-UNDERLAY-PEERS | default |
| 192.168.155.1 | 65200 | default |
| 192.168.155.2 | 65200 | default |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Common_VRF_Services |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Tenant_A_APP_Zone |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Tenant_A_DB_Zone |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Tenant_A_WAN_Zone |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Tenant_A_WEB_Zone |
| 10.255.254.4 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Tenant_B_WAN_Zone |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

##### VLAN Based

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 110 | 192.168.155.8:10110 | 10110:10110 | - | - | learned |
| 111 | 192.168.155.8:50111 | 50111:50111 | - | - | learned |
| 120 | 192.168.155.8:10120 | 10120:10120 | - | - | learned |
| 121 | 192.168.155.8:10121 | 10121:10121 | - | - | learned |
| 130 | 192.168.155.8:10130 | 10130:10130 | - | - | learned |
| 131 | 192.168.155.8:10131 | 10131:10131 | - | - | learned |
| 140 | 192.168.155.8:10140 | 10140:10140 | - | - | learned |
| 141 | 192.168.155.8:10141 | 10141:10141 | - | - | learned |
| 150 | 192.168.155.8:10150 | 10150:10150 | - | - | learned |
| 160 | 192.168.155.8:55160 | 55160:55160 | - | - | learned |
| 161 | 192.168.155.8:10161 | 10161:10161 | - | - | learned |
| 210 | 192.168.155.8:20210 | 20210:20210 | - | - | learned |
| 211 | 192.168.155.8:20211 | 20211:20211 | - | - | learned |
| 250 | 192.168.155.8:20250 | 20250:20250 | - | - | learned |

#### Router BGP EVPN VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| Common_VRF_Services | 192.168.155.8:10 | connected |
| Tenant_A_APP_Zone | 192.168.155.8:12 | connected |
| Tenant_A_DB_Zone | 192.168.155.8:130 | connected |
| Tenant_A_WAN_Zone | 192.168.155.8:14 | connected |
| Tenant_A_WEB_Zone | 192.168.155.8:11 | connected |
| Tenant_B_OP_Zone | 192.168.155.8:2000 | connected |
| Tenant_B_WAN_Zone | 192.168.155.8:21 | connected |

### Router BGP Device Configuration

```eos
!
router bgp 65102
   router-id 192.168.155.8
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS remote-as 65200
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65102
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER password 7 vnEaG8gMeQf3d3cN6PktXQ==
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 10.255.254.4 description EMEA_NORTH_02_LEAF2A
   neighbor 172.31.155.24 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.24 description EMEA_NORTH_02_SPINE1_Ethernet5
   neighbor 172.31.155.26 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.26 description EMEA_NORTH_02_SPINE2_Ethernet5
   neighbor 192.168.155.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.1 remote-as 65200
   neighbor 192.168.155.1 description EMEA_NORTH_02_SPINE1
   neighbor 192.168.155.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.2 remote-as 65200
   neighbor 192.168.155.2 description EMEA_NORTH_02_SPINE2
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 110
      rd 192.168.155.8:10110
      route-target both 10110:10110
      redistribute learned
   !
   vlan 111
      rd 192.168.155.8:50111
      route-target both 50111:50111
      redistribute learned
   !
   vlan 120
      rd 192.168.155.8:10120
      route-target both 10120:10120
      redistribute learned
   !
   vlan 121
      rd 192.168.155.8:10121
      route-target both 10121:10121
      redistribute learned
   !
   vlan 130
      rd 192.168.155.8:10130
      route-target both 10130:10130
      redistribute learned
   !
   vlan 131
      rd 192.168.155.8:10131
      route-target both 10131:10131
      redistribute learned
   !
   vlan 140
      rd 192.168.155.8:10140
      route-target both 10140:10140
      redistribute learned
   !
   vlan 141
      rd 192.168.155.8:10141
      route-target both 10141:10141
      redistribute learned
   !
   vlan 150
      rd 192.168.155.8:10150
      route-target both 10150:10150
      redistribute learned
   !
   vlan 160
      rd 192.168.155.8:55160
      route-target both 55160:55160
      redistribute learned
   !
   vlan 161
      rd 192.168.155.8:10161
      route-target both 10161:10161
      redistribute learned
   !
   vlan 210
      rd 192.168.155.8:20210
      route-target both 20210:20210
      redistribute learned
   !
   vlan 211
      rd 192.168.155.8:20211
      route-target both 20211:20211
      redistribute learned
   !
   vlan 250
      rd 192.168.155.8:20250
      route-target both 20250:20250
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf Common_VRF_Services
      rd 192.168.155.8:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_A_APP_Zone
      rd 192.168.155.8:12
      route-target import evpn 12:12
      route-target export evpn 12:12
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_A_DB_Zone
      rd 192.168.155.8:130
      route-target import evpn 130:130
      route-target export evpn 130:130
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_A_WAN_Zone
      rd 192.168.155.8:14
      route-target import evpn 14:14
      route-target export evpn 14:14
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_A_WEB_Zone
      rd 192.168.155.8:11
      route-target import evpn 11:11
      route-target export evpn 11:11
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
   !
   vrf Tenant_B_OP_Zone
      rd 192.168.155.8:2000
      route-target import evpn 2000:2000
      route-target export evpn 2000:2000
      router-id 192.168.155.8
      redistribute connected
   !
   vrf Tenant_B_WAN_Zone
      rd 192.168.155.8:21
      route-target import evpn 21:21
      route-target export evpn 21:21
      router-id 192.168.155.8
      neighbor 10.255.254.4 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
```

# BFD

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 1200 | 1200 | 3 |

### Router BFD Multihop Device Configuration

```eos
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

IGMP snooping is globally enabled.


| VLAN | IGMP Snooping |
| --- | --------------- |
| 110 | disabled |

### IP IGMP Snooping Device Configuration

```eos
!
no ip igmp snooping vlan 110
```

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 192.168.155.0/24 eq 32 |
| 20 | permit 192.168.154.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.155.0/24 eq 32
   seq 20 permit 192.168.154.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

#### RM-MLAG-PEER-IN

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | set origin incomplete |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| Common_VRF_Services | enabled |
| MGMT | disabled |
| Tenant_A_APP_Zone | enabled |
| Tenant_A_DB_Zone | enabled |
| Tenant_A_WAN_Zone | enabled |
| Tenant_A_WEB_Zone | enabled |
| Tenant_B_OP_Zone | enabled |
| Tenant_B_WAN_Zone | enabled |

## VRF Instances Device Configuration

```eos
!
vrf instance Common_VRF_Services
!
vrf instance MGMT
!
vrf instance Tenant_A_APP_Zone
!
vrf instance Tenant_A_DB_Zone
!
vrf instance Tenant_A_WAN_Zone
!
vrf instance Tenant_A_WEB_Zone
!
vrf instance Tenant_B_OP_Zone
!
vrf instance Tenant_B_WAN_Zone
```

# Virtual Source NAT

## Virtual Source NAT Summary

| Source NAT VRF | Source NAT IP Address |
| -------------- | --------------------- |
| Common_VRF_Services | 10.255.1.8 |

## Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf Common_VRF_Services address 10.255.1.8
```

# Quality Of Service
