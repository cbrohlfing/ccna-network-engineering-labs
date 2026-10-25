# Lab 001 — Two-Site Network Connectivity

**Project:** Project Snowden  
**Status:** Completed  
**Platform:** Cisco Packet Tracer

## 1. Objective

Establish and verify IPv4 connectivity between a headquarters network and a remote branch office using Cisco routers, switches, and static routing.

The lab introduces foundational enterprise networking concepts and establishes the initial infrastructure for future Project Snowden expansions.

## 2. Network Architecture

The network consists of two locations:

**Headquarters (HQ)**
- Cisco 2911 router
- Cisco Catalyst 2960 switch
- Local end devices

**Branch Office**
- Cisco 2911 router
- Cisco Catalyst 2960 switch
- Local end devices

The locations are interconnected through a point-to-point IPv4 WAN subnet using a /30 prefix.

## 3. Technologies Demonstrated

- Cisco IOS CLI configuration
- IPv4 interface addressing
- Static route configuration
- Ethernet switching and MAC address learning
- Address Resolution Protocol (ARP)
- Layer 2 and Layer 3 forwarding
- ICMP echo testing
- Traceroute and TTL behavior

## 4. Implementation

The lab involved configuring router interfaces, establishing LAN and WAN connectivity, and adding static routes so that devices on each site could communicate.

Switches provided Layer 2 connectivity within each LAN.

Static routes enabled forwarding between the headquarters and branch networks.

## 5. Verification

Connectivity and forwarding behavior were examined using:

- `ping`
- `tracert` / `traceroute`
- `show ip route`
- `show ip interface brief`
- MAC address table inspection
- ARP table inspection
- Packet Tracer Simulation Mode

The lab established and verified connectivity between the two sites.

## 6. Key Learning Outcomes

### Layer 2 vs. Layer 3 Forwarding

Switches forward Ethernet frames using MAC addresses, while routers forward IP packets between networks using routing tables.

### ARP and Next-Hop Addressing

When sending traffic to a remote subnet, a host sends the Ethernet frame toward its default gateway.

The destination IP address remains that of the remote host, while Ethernet source and destination MAC addresses change at each routed hop.

### Static Routing

Static routes allow routers to forward traffic toward networks that are not directly connected.

### TTL and Traceroute

The IP Time to Live (TTL) field is reduced as packets pass through routers. Traceroute uses this behavior to help identify intermediate routing hops.

## 7. Future Development

Lab 001 provides the foundation for the next phase of Project Snowden:

**Lab 002 — VLANs, Trunking, and Inter-VLAN Routing**

Planned additions include:
- VLAN segmentation
- IEEE 802.1Q trunking
- Router-on-a-stick
- Inter-VLAN connectivity testing

## 8. Supporting Files

The Packet Tracer topology file, network diagram, and sanitized configuration exports will be added when available.

---

*This lab is part of Project Snowden, an independent network engineering portfolio developed during CCNA preparation.*
