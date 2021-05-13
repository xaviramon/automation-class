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
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF1A | 172.16.77.11/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | l3leaf | EMEA_NORTH_01_LEAF1B | 172.16.77.12/24 | vEOS-LAB | Provisioned |
| EMEA_NORTH_01 | spine | EMEA_NORTH_01_SPINE1 | 172.16.77.21/24 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet1 | spine | EMEA_NORTH_01_SPINE1 | Ethernet1 |
| l3leaf | EMEA_NORTH_01_LEAF1A | Ethernet2 | mlag_peer | EMEA_NORTH_01_LEAF1B | Ethernet2 |
| l3leaf | EMEA_NORTH_01_LEAF1B | Ethernet1 | spine | EMEA_NORTH_01_SPINE1 | Ethernet2 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| P2P Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ----------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 4 | 1.57 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| EMEA_NORTH_01_LEAF1A | Ethernet1 | 172.31.255.1/31 | EMEA_NORTH_01_SPINE1 | Ethernet1 | 172.31.255.0/31 |
| EMEA_NORTH_01_LEAF1B | Ethernet1 | 172.31.255.9/31 | EMEA_NORTH_01_SPINE1 | Ethernet2 | 172.31.255.8/31 |

## Overlay Loopback Interfaces (BGP EVPN Peering)

| Overlay Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------------ | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 3 | 1.18 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1A | 192.168.255.5/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1B | 192.168.255.6/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_SPINE1 | 192.168.255.1/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)

| VTEP Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.254.0/24 | 256 | 2 | 0.79 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1A | 192.168.254.5/32 |
| EMEA_NORTH_01 | EMEA_NORTH_01_LEAF1B | 192.168.254.5/32 |
