# EMEA_NORTH_02_SPINE2
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
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Quality Of Service](#quality-of-service)

<!-- toc -->
# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 192.168.1.11/24 | 192.168.0.1 |

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
   ip address 192.168.1.11/24
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

# Spanning Tree

## Spanning Tree Summary

STP mode: **none**

### Global Spanning-Tree Settings


## Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
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

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet2 | P2P_LINK_TO_EMEA_NORTH_02_LEAF1A_Ethernet3 | routed | - | 172.31.155.2/31 | default | 1500 | false | - | - |
| Ethernet3 | P2P_LINK_TO_EMEA_NORTH_02_LEAF1B_Ethernet3 | routed | - | 172.31.155.10/31 | default | 1500 | false | - | - |
| Ethernet4 | P2P_LINK_TO_EMEA_NORTH_02_LEAF2A_Ethernet3 | routed | - | 172.31.155.18/31 | default | 1500 | false | - | - |
| Ethernet5 | P2P_LINK_TO_EMEA_NORTH_02_LEAF2B_Ethernet3 | routed | - | 172.31.155.26/31 | default | 1500 | false | - | - |
| Ethernet7 | P2P_LINK_TO_EMEA_NORTH_SUPERSPINE1_Ethernet4 | routed | - | 172.31.2.3/31 | default | 1500 | false | - | - |
| Ethernet8 | P2P_LINK_TO_EMEA_NORTH_SUPERSPINE2_Ethernet4 | routed | - | 172.31.2.131/31 | default | 1500 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet2
   description P2P_LINK_TO_EMEA_NORTH_02_LEAF1A_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.2/31
!
interface Ethernet3
   description P2P_LINK_TO_EMEA_NORTH_02_LEAF1B_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.10/31
!
interface Ethernet4
   description P2P_LINK_TO_EMEA_NORTH_02_LEAF2A_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.18/31
!
interface Ethernet5
   description P2P_LINK_TO_EMEA_NORTH_02_LEAF2B_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.155.26/31
!
interface Ethernet7
   description P2P_LINK_TO_EMEA_NORTH_SUPERSPINE1_Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.2.3/31
!
interface Ethernet8
   description P2P_LINK_TO_EMEA_NORTH_SUPERSPINE2_Ethernet4
   no shutdown
   mtu 1500
   no switchport
   ip address 172.31.2.131/31
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 192.168.155.2/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 192.168.155.2/32
```

# Routing

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true|| MGMT | false |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false || MGMT | false |


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
| 65200|  192.168.155.2 |

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
| Next-hop unchanged | True |
| Source | Loopback0 |
| Bfd | true |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF |
| -------- | --------- | --- |
| 172.31.2.2 | 65001 | default |
| 172.31.2.130 | 65001 | default |
| 172.31.155.3 | 65101 | default |
| 172.31.155.11 | 65101 | default |
| 172.31.155.19 | 65102 | default |
| 172.31.155.27 | 65102 | default |
| 192.168.100.1 | 65001 | default |
| 192.168.100.2 | 65001 | default |
| 192.168.155.5 | 65101 | default |
| 192.168.155.6 | 65101 | default |
| 192.168.155.7 | 65102 | default |
| 192.168.155.8 | 65102 | default |

### Router BGP EVPN Address Family

#### Router BGP EVPN MAC-VRFs

#### Router BGP EVPN VRFs

### Router BGP Device Configuration

```eos
!
router bgp 65200
   router-id 192.168.155.2
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 q+VNViP5i4rVjW1cxFv2wA==
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 AQQvKeimxJu+uGQ/yYvv9w==
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.31.2.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.2.2 remote-as 65001
   neighbor 172.31.2.2 description EMEA_NORTH_SUPERSPINE1_Ethernet4
   neighbor 172.31.2.130 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.2.130 remote-as 65001
   neighbor 172.31.2.130 description EMEA_NORTH_SUPERSPINE2_Ethernet4
   neighbor 172.31.155.3 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.3 remote-as 65101
   neighbor 172.31.155.3 description EMEA_NORTH_02_LEAF1A_Ethernet3
   neighbor 172.31.155.11 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.11 remote-as 65101
   neighbor 172.31.155.11 description EMEA_NORTH_02_LEAF1B_Ethernet3
   neighbor 172.31.155.19 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.19 remote-as 65102
   neighbor 172.31.155.19 description EMEA_NORTH_02_LEAF2A_Ethernet3
   neighbor 172.31.155.27 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.31.155.27 remote-as 65102
   neighbor 172.31.155.27 description EMEA_NORTH_02_LEAF2B_Ethernet3
   neighbor 192.168.100.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.100.1 remote-as 65001
   neighbor 192.168.100.1 description EMEA_NORTH_SUPERSPINE1
   neighbor 192.168.100.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.100.2 remote-as 65001
   neighbor 192.168.100.2 description EMEA_NORTH_SUPERSPINE2
   neighbor 192.168.155.5 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.5 remote-as 65101
   neighbor 192.168.155.5 description EMEA_NORTH_02_LEAF1A
   neighbor 192.168.155.6 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.6 remote-as 65101
   neighbor 192.168.155.6 description EMEA_NORTH_02_LEAF1B
   neighbor 192.168.155.7 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.7 remote-as 65102
   neighbor 192.168.155.7 description EMEA_NORTH_02_LEAF2A
   neighbor 192.168.155.8 peer group EVPN-OVERLAY-PEERS
   neighbor 192.168.155.8 remote-as 65102
   neighbor 192.168.155.8 description EMEA_NORTH_02_LEAF2B
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 192.168.155.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.155.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

# Quality Of Service
