# DC2_FABRIC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| DC2_FABRIC | l2leaf | DC2-L2LEAF1A | 10.255.0.17/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | l3leaf | DC2-LEAF1A | 10.255.0.13/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | l3leaf | DC2-LEAF1B | 10.255.0.14/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | spine | DC2-SPINE1 | 10.255.0.11/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | spine | DC2-SPINE2a | 10.255.0.12/24 | vEOS-LAB | Provisioned |
| DC2_FABRIC | spine | DC2-SPINE3 | 10.255.0.100/24 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l2leaf | DC2-L2LEAF1A | Ethernet1 | l3leaf | DC2-LEAF1A | Ethernet5 |
| l2leaf | DC2-L2LEAF1A | Ethernet2 | l3leaf | DC2-LEAF1B | Ethernet5 |
| l3leaf | DC2-LEAF1A | Ethernet1 | spine | DC2-SPINE1 | Ethernet1 |
| l3leaf | DC2-LEAF1A | Ethernet2 | spine | DC2-SPINE2a | Ethernet1 |
| l3leaf | DC2-LEAF1A | Ethernet3 | mlag_peer | DC2-LEAF1B | Ethernet3 |
| l3leaf | DC2-LEAF1A | Ethernet4 | mlag_peer | DC2-LEAF1B | Ethernet4 |
| l3leaf | DC2-LEAF1B | Ethernet1 | spine | DC2-SPINE1 | Ethernet2 |
| l3leaf | DC2-LEAF1B | Ethernet2 | spine | DC2-SPINE2a | Ethernet2 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 8 | 3.13 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| DC2-LEAF1A | Ethernet1 | 172.31.255.1/31 | DC2-SPINE1 | Ethernet1 | 172.31.255.0/31 |
| DC2-LEAF1A | Ethernet2 | 172.31.255.3/31 | DC2-SPINE2a | Ethernet1 | 172.31.255.2/31 |
| DC2-LEAF1B | Ethernet1 | 172.31.255.7/31 | DC2-SPINE1 | Ethernet2 | 172.31.255.6/31 |
| DC2-LEAF1B | Ethernet2 | 172.31.255.9/31 | DC2-SPINE2a | Ethernet2 | 172.31.255.8/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 5 | 1.96 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC2_FABRIC | DC2-LEAF1A | 192.168.255.3/32 |
| DC2_FABRIC | DC2-LEAF1B | 192.168.255.4/32 |
| DC2_FABRIC | DC2-SPINE1 | 192.168.255.1/32 |
| DC2_FABRIC | DC2-SPINE2a | 192.168.255.2/32 |
| DC2_FABRIC | DC2-SPINE3 | 192.168.255.3/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.254.0/24 | 256 | 2 | 0.79 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC2_FABRIC | DC2-LEAF1A | 192.168.254.3/32 |
| DC2_FABRIC | DC2-LEAF1B | 192.168.254.3/32 |
