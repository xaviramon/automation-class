# EMEA

# Table of Contents
<!-- toc -->

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Overlay Loopback Interfaces (BGP EVPN Peering)](#overlay-loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-leafs-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

<!-- toc -->
# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF1A | 192.168.0.12/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF1B | 192.168.0.13/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF2A | 192.168.0.14/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF2B | 192.168.0.15/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF3A | 192.168.0.16/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF3B | 192.168.0.17/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | spine | EMEA_NORTH_01_SPINE1 | 192.168.0.10/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | spine | EMEA_NORTH_01_SPINE2 | 192.168.0.11/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF1A | 192.168.1.12/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF1B | 192.168.1.13/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF2A | 192.168.1.14/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF2B | 192.168.1.15/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF3A | 192.168.1.16/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | l3leaf | EMEA_NORTH_02_LEAF3B | 192.168.1.17/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | spine | EMEA_NORTH_02_SPINE1 | 192.168.1.10/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_02 | spine | EMEA_NORTH_02_SPINE2 | 192.168.1.11/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH | super-spine | EMEA_NORTH_SUPERSPINE1 | 192.168.0.1/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH | super-spine | EMEA_NORTH_SUPERSPINE2 | 192.168.0.2/24 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet1 |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet1 |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet12 | mlag_peer | EMEA_NORTH_01_LEAF1B | Ethernet12 |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet13 | mlag_peer | EMEA_NORTH_01_LEAF1B | Ethernet13 |
| l3leaf | EMEA_NORTH_01_LEAF1B | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet2 |
| l3leaf | EMEA_NORTH_01_LEAF1B | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet2 |
| l3leaf | EMEA_NORTH_01_LEAF2A | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet3 |
| l3leaf | EMEA_NORTH_01_LEAF2A | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet3 |
| l3leaf | EMEA_NORTH_01_LEAF2A | Ethernet12 | mlag_peer | EMEA_NORTH_01_LEAF2B | Ethernet12 |
| l3leaf | EMEA_NORTH_01_LEAF2A | Ethernet13 | mlag_peer | EMEA_NORTH_01_LEAF2B | Ethernet13 |
| l3leaf | EMEA_NORTH_01_LEAF2B | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet4 |
| l3leaf | EMEA_NORTH_01_LEAF2B | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet4 |
| l3leaf | EMEA_NORTH_01_LEAF3A | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet5 |
| l3leaf | EMEA_NORTH_01_LEAF3A | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet5 |
| l3leaf | EMEA_NORTH_01_LEAF3A | Ethernet12 | mlag_peer | EMEA_NORTH_01_LEAF3B | Ethernet12 |
| l3leaf | EMEA_NORTH_01_LEAF3A | Ethernet13 | mlag_peer | EMEA_NORTH_01_LEAF3B | Ethernet13 |
| l3leaf | EMEA_NORTH_01_LEAF3B | Ethernet10 | spine | EMEA_NORTH_01_SPINE1 | Ethernet6 |
| l3leaf | EMEA_NORTH_01_LEAF3B | Ethernet11 | spine | EMEA_NORTH_01_SPINE2 | Ethernet6 |
| spine | EMEA_NORTH_01_SPINE1 | Ethernet10 | super-spine | EMEA_NORTH_SUPERSPINE1 | Ethernet1 |
| spine | EMEA_NORTH_01_SPINE1 | Ethernet11 | super-spine | EMEA_NORTH_SUPERSPINE2 | Ethernet1 |
| spine | EMEA_NORTH_01_SPINE2 | Ethernet10 | super-spine | EMEA_NORTH_SUPERSPINE1 | Ethernet2 |
| spine | EMEA_NORTH_01_SPINE2 | Ethernet11 | super-spine | EMEA_NORTH_SUPERSPINE2 | Ethernet2 |
| l3leaf | EMEA_NORTH_02_LEAF1A | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet2 |
| l3leaf | EMEA_NORTH_02_LEAF1A | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet2 |
| l3leaf | EMEA_NORTH_02_LEAF1A | Ethernet12 | mlag_peer | EMEA_NORTH_02_LEAF1B | Ethernet12 |
| l3leaf | EMEA_NORTH_02_LEAF1A | Ethernet13 | mlag_peer | EMEA_NORTH_02_LEAF1B | Ethernet13 |
| l3leaf | EMEA_NORTH_02_LEAF1B | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet3 |
| l3leaf | EMEA_NORTH_02_LEAF1B | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet3 |
| l3leaf | EMEA_NORTH_02_LEAF2A | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet4 |
| l3leaf | EMEA_NORTH_02_LEAF2A | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet4 |
| l3leaf | EMEA_NORTH_02_LEAF2A | Ethernet12 | mlag_peer | EMEA_NORTH_02_LEAF2B | Ethernet12 |
| l3leaf | EMEA_NORTH_02_LEAF2A | Ethernet13 | mlag_peer | EMEA_NORTH_02_LEAF2B | Ethernet13 |
| l3leaf | EMEA_NORTH_02_LEAF2B | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet5 |
| l3leaf | EMEA_NORTH_02_LEAF2B | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet5 |
| l3leaf | EMEA_NORTH_02_LEAF3A | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet9 |
| l3leaf | EMEA_NORTH_02_LEAF3A | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet9 |
| l3leaf | EMEA_NORTH_02_LEAF3A | Ethernet12 | mlag_peer | EMEA_NORTH_02_LEAF3B | Ethernet12 |
| l3leaf | EMEA_NORTH_02_LEAF3A | Ethernet13 | mlag_peer | EMEA_NORTH_02_LEAF3B | Ethernet13 |
| l3leaf | EMEA_NORTH_02_LEAF3B | Ethernet2 | spine | EMEA_NORTH_02_SPINE1 | Ethernet10 |
| l3leaf | EMEA_NORTH_02_LEAF3B | Ethernet3 | spine | EMEA_NORTH_02_SPINE2 | Ethernet10 |
| spine | EMEA_NORTH_02_SPINE1 | Ethernet11 | super-spine | EMEA_NORTH_SUPERSPINE2 | Ethernet3 |
| spine | EMEA_NORTH_02_SPINE2 | Ethernet11 | super-spine | EMEA_NORTH_SUPERSPINE2 | Ethernet4 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| P2P Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ----------- | ------------------- | ------------------ | ------------------ |
| 172.31.1.0/24 | 256 | 8 | 3.13 % |
| 172.31.2.0/24 | 256 | 4 | 1.57 % |
| 172.31.155.0/24 | 256 | 24 | 9.38 % |
| 172.31.255.0/24 | 256 | 24 | 9.38 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| EMEA_NORTH_01_LEAF1A | Ethernet10 | 172.31.255.1/31 | EMEA_NORTH_01_SPINE1 | Ethernet1 | 172.31.255.0/31 |
| EMEA_NORTH_01_LEAF1A | Ethernet11 | 172.31.255.3/31 | EMEA_NORTH_01_SPINE2 | Ethernet1 | 172.31.255.2/31 |
| EMEA_NORTH_01_LEAF1B | Ethernet10 | 172.31.255.9/31 | EMEA_NORTH_01_SPINE1 | Ethernet2 | 172.31.255.8/31 |
| EMEA_NORTH_01_LEAF1B | Ethernet11 | 172.31.255.11/31 | EMEA_NORTH_01_SPINE2 | Ethernet2 | 172.31.255.10/31 |
| EMEA_NORTH_01_LEAF2A | Ethernet10 | 172.31.255.17/31 | EMEA_NORTH_01_SPINE1 | Ethernet3 | 172.31.255.16/31 |
| EMEA_NORTH_01_LEAF2A | Ethernet11 | 172.31.255.19/31 | EMEA_NORTH_01_SPINE2 | Ethernet3 | 172.31.255.18/31 |
| EMEA_NORTH_01_LEAF2B | Ethernet10 | 172.31.255.25/31 | EMEA_NORTH_01_SPINE1 | Ethernet4 | 172.31.255.24/31 |
| EMEA_NORTH_01_LEAF2B | Ethernet11 | 172.31.255.27/31 | EMEA_NORTH_01_SPINE2 | Ethernet4 | 172.31.255.26/31 |
| EMEA_NORTH_01_LEAF3A | Ethernet10 | 172.31.255.33/31 | EMEA_NORTH_01_SPINE1 | Ethernet5 | 172.31.255.32/31 |
| EMEA_NORTH_01_LEAF3A | Ethernet11 | 172.31.255.35/31 | EMEA_NORTH_01_SPINE2 | Ethernet5 | 172.31.255.34/31 |
| EMEA_NORTH_01_LEAF3B | Ethernet10 | 172.31.255.41/31 | EMEA_NORTH_01_SPINE1 | Ethernet6 | 172.31.255.40/31 |
| EMEA_NORTH_01_LEAF3B | Ethernet11 | 172.31.255.43/31 | EMEA_NORTH_01_SPINE2 | Ethernet6 | 172.31.255.42/31 |
| EMEA_NORTH_01_SPINE1 | Ethernet10 | 172.31.1.1/31 | EMEA_NORTH_SUPERSPINE1 | Ethernet1 | 172.31.1.0/31 |
| EMEA_NORTH_01_SPINE1 | Ethernet11 | 172.31.1.129/31 | EMEA_NORTH_SUPERSPINE2 | Ethernet1 | 172.31.1.128/31 |
| EMEA_NORTH_01_SPINE2 | Ethernet10 | 172.31.1.3/31 | EMEA_NORTH_SUPERSPINE1 | Ethernet2 | 172.31.1.2/31 |
| EMEA_NORTH_01_SPINE2 | Ethernet11 | 172.31.1.131/31 | EMEA_NORTH_SUPERSPINE2 | Ethernet2 | 172.31.1.130/31 |
| EMEA_NORTH_02_LEAF1A | Ethernet2 | 172.31.155.1/31 | EMEA_NORTH_02_SPINE1 | Ethernet2 | 172.31.155.0/31 |
| EMEA_NORTH_02_LEAF1A | Ethernet3 | 172.31.155.3/31 | EMEA_NORTH_02_SPINE2 | Ethernet2 | 172.31.155.2/31 |
| EMEA_NORTH_02_LEAF1B | Ethernet2 | 172.31.155.9/31 | EMEA_NORTH_02_SPINE1 | Ethernet3 | 172.31.155.8/31 |
| EMEA_NORTH_02_LEAF1B | Ethernet3 | 172.31.155.11/31 | EMEA_NORTH_02_SPINE2 | Ethernet3 | 172.31.155.10/31 |
| EMEA_NORTH_02_LEAF2A | Ethernet2 | 172.31.155.17/31 | EMEA_NORTH_02_SPINE1 | Ethernet4 | 172.31.155.16/31 |
| EMEA_NORTH_02_LEAF2A | Ethernet3 | 172.31.155.19/31 | EMEA_NORTH_02_SPINE2 | Ethernet4 | 172.31.155.18/31 |
| EMEA_NORTH_02_LEAF2B | Ethernet2 | 172.31.155.25/31 | EMEA_NORTH_02_SPINE1 | Ethernet5 | 172.31.155.24/31 |
| EMEA_NORTH_02_LEAF2B | Ethernet3 | 172.31.155.27/31 | EMEA_NORTH_02_SPINE2 | Ethernet5 | 172.31.155.26/31 |
| EMEA_NORTH_02_LEAF3A | Ethernet2 | 172.31.155.33/31 | EMEA_NORTH_02_SPINE1 | Ethernet9 | 172.31.155.32/31 |
| EMEA_NORTH_02_LEAF3A | Ethernet3 | 172.31.155.35/31 | EMEA_NORTH_02_SPINE2 | Ethernet9 | 172.31.155.34/31 |
| EMEA_NORTH_02_LEAF3B | Ethernet2 | 172.31.155.41/31 | EMEA_NORTH_02_SPINE1 | Ethernet10 | 172.31.155.40/31 |
| EMEA_NORTH_02_LEAF3B | Ethernet3 | 172.31.155.43/31 | EMEA_NORTH_02_SPINE2 | Ethernet10 | 172.31.155.42/31 |
| EMEA_NORTH_02_SPINE1 | Ethernet11 | 172.31.2.129/31 | EMEA_NORTH_SUPERSPINE2 | Ethernet3 | 172.31.2.128/31 |
| EMEA_NORTH_02_SPINE2 | Ethernet11 | 172.31.2.131/31 | EMEA_NORTH_SUPERSPINE2 | Ethernet4 | 172.31.2.130/31 |

## Overlay Loopback Interfaces (BGP EVPN Peering)

| Overlay Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------------ | ------------------- | ------------------ | ------------------ |
| 192.168.100.0/24 | 256 | 2 | 0.79 % |
| 192.168.155.0/24 | 256 | 8 | 3.13 % |
| 192.168.255.0/24 | 256 | 8 | 3.13 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1A | 192.168.255.5/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1B | 192.168.255.6/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF2A | 192.168.255.7/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF2B | 192.168.255.8/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF3A | 192.168.255.9/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF3B | 192.168.255.10/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_SPINE1 | 192.168.255.1/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_SPINE2 | 192.168.255.2/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF1A | 192.168.155.5/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF1B | 192.168.155.6/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF2A | 192.168.155.7/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF2B | 192.168.155.8/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF3A | 192.168.155.9/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF3B | 192.168.155.10/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_SPINE1 | 192.168.155.1/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_SPINE2 | 192.168.155.2/32 |
| EMEA_NORTH | EMEA_NORTH_SUPERSPINE1 | 192.168.100.1/32 |
| EMEA_NORTH | EMEA_NORTH_SUPERSPINE2 | 192.168.100.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)

| VTEP Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.154.0/24 | 256 | 6 | 2.35 % |
| 192.168.254.0/24 | 256 | 6 | 2.35 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1A | 192.168.254.5/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1B | 192.168.254.5/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF2A | 192.168.254.7/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF2B | 192.168.254.7/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF3A | 192.168.254.9/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF3B | 192.168.254.9/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF1A | 192.168.154.5/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF1B | 192.168.154.5/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF2A | 192.168.154.7/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF2B | 192.168.154.7/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF3A | 192.168.154.9/32 |
| EMEA_NORTH_02 | EMEA_NORTH_02_LEAF3B | 192.168.154.9/32 |
