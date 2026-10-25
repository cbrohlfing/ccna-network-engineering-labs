# Lab 001 — Two-Site Network Connectivity

**Project:** Project Snowden  
**Status:** Completed  
**Platform:** Cisco Packet Tracer

## 1. Objective

Establish and verify IPv4 connectivity between a headquarters network and a remote branch office using Cisco routers, switches, and static routing.

The lab introduces foundational enterprise networking concepts and establishes the initial infrastructure for future Project Snowden expansions.

## 2. Network Architecture

The network consists of two locations:

### Network Topology

![Project Snowden Lab 001 Network Topology](Snowdon%20Lab%20001%20Topology.png)

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

## 9. Network Addressing Plan

The completed lab uses three IPv4 networks:

| Network | Subnet | Purpose |
|---|---|---|
| Headquarters LAN | `192.168.10.0/24` | HQ end-device connectivity |
| Point-to-point WAN | `10.0.0.0/30` | Connection between routers |
| Branch LAN | `192.168.30.0/24` | Branch end-device connectivity |

### Device Addressing

| Device | Interface | IPv4 Address | Subnet Mask |
|---|---|---|---|
| R1-HQ | Gi0/0 | 192.168.10.1 | 255.255.255.0 |
| R1-HQ | Gi0/1 | 10.0.0.1 | 255.255.255.252 |
| R2-Branch | Gi0/0 | 192.168.30.1 | 255.255.255.0 |
| R2-Branch | Gi0/1 | 10.0.0.2 | 255.255.255.252 |
| PC-HQ1 | Fa0 | 192.168.10.10 | 255.255.255.0 |
| PC-BR1 | Fa0 | 192.168.30.10 | 255.255.255.0 |

**Default gateways:**

- PC-HQ1: `192.168.10.1`
- PC-BR1: `192.168.30.1`

PC-HQ2 and PC-BR2 were physically connected but reserved for future exercises.

## 10. Router Configuration

The following are the verified configuration summaries from the completed lab, not full running-configuration exports.

### R1-HQ

```cisco
hostname R1-HQ

interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown

ip route 192.168.30.0 255.255.255.0 10.0.0.2
```

### R2-Branch

```cisco
hostname R2-Branch

interface GigabitEthernet0/0
 ip address 192.168.30.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 ip address 10.0.0.2 255.255.255.252
 no shutdown

ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

Both routers' configurations were saved to NVRAM using:

```cisco
copy running-config startup-config
```

## 11. Routing Verification

The routing tables confirmed that both routers had connected, local, and static routes.

### R1-HQ

```text
C 10.0.0.0/30 is directly connected, GigabitEthernet0/1
L 10.0.0.1/32 is directly connected, GigabitEthernet0/1
C 192.168.10.0/24 is directly connected, GigabitEthernet0/0
L 192.168.10.1/32 is directly connected, GigabitEthernet0/0
S 192.168.30.0/24 [1/0] via 10.0.0.2
```

### R2-Branch

```text
C 10.0.0.0/30 is directly connected, GigabitEthernet0/1
L 10.0.0.2/32 is directly connected, GigabitEthernet0/1
S 192.168.10.0/24 [1/0] via 10.0.0.1
C 192.168.30.0/24 is directly connected, GigabitEthernet0/0
L 192.168.30.1/32 is directly connected, GigabitEthernet0/0
```

**Routing concepts demonstrated:**

- `C` — Directly connected network
- `L` — Local interface host route
- `S` — Static route
- `[1/0]` — Administrative distance 1, metric 0

Static routes on both routers provided forward and return paths between the two LANs.

## 12. Connectivity Verification

The following results were recorded during the completed Packet Tracer lab.

| Test | Successful Pings |
|---|---|
| R2-Branch → R1-HQ WAN interface | 4/5 |
| PC-HQ1 → HQ default gateway | 4/4 |
| PC-BR1 → Branch default gateway | 4/4 |
| PC-HQ1 → PC-BR1 | 3/4 |
| PC-BR1 → PC-HQ1 | 4/4 |

Initial timeouts were consistent with ARP resolution delays in Packet Tracer. End-to-end communication was successfully established in both directions.

### Traceroute

A traceroute from PC-HQ1 to PC-BR1 identified the following path:

```text
tracert 192.168.30.10

1  192.168.10.1
2  10.0.0.2
3  192.168.30.10
```

The path confirmed that traffic passed through the headquarters router and branch router before reaching the destination host.

Some individual traceroute probes timed out, but the trace completed.

## 13. ARP and Ethernet Switching

The lab included inspection of ARP tables and switch MAC address tables.

### Example ARP Observation

PC-HQ1 resolved its default gateway:

```text
192.168.10.1 -> 0001.9781.2901
```

### Switch MAC Address Learning

SW1-HQ dynamically learned the following entries:

```text
VLAN 1    0000.0cea.6405    Fa0/1
VLAN 1    0001.9781.2901    Gi0/1
```

These observations demonstrated that:

- ARP maps local IPv4 addresses to Ethernet MAC addresses.
- Switches dynamically learn source MAC addresses.
- Switches use destination MAC addresses when forwarding frames.
- Routers rewrite Ethernet framing when forwarding packets between networks.
- The original IP destination remains unchanged during normal routing.

## 14. Lab Completion

**Result:** Two-site IPv4 connectivity successfully established and verified.

The completed Packet Tracer network provides the foundation for subsequent Project Snowden labs, including VLAN segmentation, 802.1Q trunking, and inter-VLAN routing.
---

*This lab is part of Project Snowden, an independent network engineering portfolio developed during CCNA preparation.*
