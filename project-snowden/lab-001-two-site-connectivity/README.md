# Lab 001 — Two-Site Network Connectivity

**Project:** Project Snowden  
**Lab ID:** 001  
**Completion Date:** 2026-10-23  
**Status:** Completed  
**Platform:** Cisco Packet Tracer  
**Lab Type:** Independent

## 1. Lab Overview

### Objective

Design, configure, and verify IPv4 connectivity between a headquarters network and a remote branch office using Cisco routers, Layer 2 switches, and static routing.

The lab establishes the initial network infrastructure for Project Snowden, an independent network engineering lab environment developed during CCNA preparation.

### Scope

The implementation includes two IPv4 LANs connected by a point-to-point WAN subnet. Static routes provide connectivity between the two sites.

Dynamic routing protocols, VLAN segmentation, and inter-VLAN routing are outside the scope of Lab 001.

## 2. Learning Objectives

- Configure Cisco IOS router interfaces and IPv4 addressing.
- Establish Layer 2 Ethernet connectivity using Cisco switches.
- Configure static routes for communication between remote networks.
- Understand connected, local, and static routing-table entries.
- Examine ARP resolution and dynamic MAC address learning.
- Verify network connectivity using ICMP and traceroute.
- Understand TTL behavior during routed packet forwarding.
- Save router configurations to NVRAM.

## 3. Network Topology

### Topology Diagram

![Project Snowden Lab 001 Network Topology](Snowdon%20Lab%20001%20Topology.png)

### Devices and Equipment

| Device | Model / Platform | Role |
|---|---|---|
| R1-HQ | Cisco 2911 | Headquarters router |
| SW1-HQ | Cisco 2960-24TT | Headquarters access switch |
| PC-HQ1 | Packet Tracer PC | Configured headquarters endpoint |
| PC-HQ2 | Packet Tracer PC | Reserved endpoint |
| R2-Branch | Cisco 2911 | Branch router |
| SW2-Branch | Cisco 2960-24TT | Branch access switch |
| PC-BR1 | Packet Tracer PC | Configured branch endpoint |
| PC-BR2 | Packet Tracer PC | Reserved endpoint |

### Architecture

Each location contains a router, an Ethernet switch, and two connected PCs.

The headquarters and branch routers are interconnected through the `10.0.0.0/30` WAN network.

The switches provide Layer 2 connectivity within their respective LANs, while the routers provide Layer 3 forwarding between networks.

PC-HQ2 and PC-BR2 were physically connected but intentionally left unconfigured for future lab exercises.

## 4. Addressing and Design

### Network Allocation

| Network | IPv4 Subnet | Purpose |
|---|---|---|
| Headquarters LAN | `192.168.10.0/24` | HQ endpoint connectivity |
| Point-to-point WAN | `10.0.0.0/30` | Inter-router communication |
| Branch LAN | `192.168.30.0/24` | Branch endpoint connectivity |

### Device Addressing

| Device | Interface | IPv4 Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| R1-HQ | Gi0/0 | 192.168.10.1 | 255.255.255.0 | N/A |
| R1-HQ | Gi0/1 | 10.0.0.1 | 255.255.255.252 | N/A |
| R2-Branch | Gi0/0 | 192.168.30.1 | 255.255.255.0 | N/A |
| R2-Branch | Gi0/1 | 10.0.0.2 | 255.255.255.252 | N/A |
| PC-HQ1 | Fa0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC-BR1 | Fa0 | 192.168.30.10 | 255.255.255.0 | 192.168.30.1 |

### Design Considerations

The `/30` WAN subnet provides two usable IPv4 host addresses, suitable for the point-to-point connection between R1-HQ and R2-Branch.

Each LAN uses a separate `/24` subnet, with the local router interface serving as the default gateway for its configured endpoint.

Static routing was selected to demonstrate fundamental routing behavior before introducing dynamic routing protocols.

## 5. Implementation

### Configuration Summary

Both routers were configured with IPv4 addresses on their LAN and WAN interfaces. The interfaces were enabled using `no shutdown`.

A static route was configured on each router to reach the remote LAN through the opposite router's WAN interface.

The switches provided Ethernet connectivity using their existing Layer 2 switching functionality.

### Device Configurations

The following are verified configuration summaries from the completed lab, not full running-configuration exports.

**R1-HQ — Headquarters Router**

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

**R2-Branch — Branch Router**

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

### Configuration Persistence

Both routers' configurations were saved to NVRAM using:

```cisco
copy running-config startup-config
```

R1-HQ's startup configuration was inspected and verified. R2-Branch reported a successful save.

## 6. Verification and Testing

### Verification Commands

The completed lab used the following commands and diagnostic tools:

```cisco
show ip interface brief
show ip route
show ip arp
show mac address-table
```

Endpoint testing included:

```text
ping
tracert
arp -a
```

Packet Tracer Simulation Mode was also used to examine network behavior.

### Routing Table Verification

**R1-HQ**

```text
C 10.0.0.0/30 is directly connected, GigabitEthernet0/1
L 10.0.0.1/32 is directly connected, GigabitEthernet0/1
C 192.168.10.0/24 is directly connected, GigabitEthernet0/0
L 192.168.10.1/32 is directly connected, GigabitEthernet0/0
S 192.168.30.0/24 [1/0] via 10.0.0.2
```

**R2-Branch**

```text
C 10.0.0.0/30 is directly connected, GigabitEthernet0/1
L 10.0.0.2/32 is directly connected, GigabitEthernet0/1
S 192.168.10.0/24 [1/0] via 10.0.0.1
C 192.168.30.0/24 is directly connected, GigabitEthernet0/0
L 192.168.30.1/32 is directly connected, GigabitEthernet0/0
```

The routing tables confirmed the presence of directly connected networks, local interface routes, and static routes.

### Connectivity Test Results

| Test | Expected Result | Observed Result | Status |
|---|---|---|---|
| R2-Branch → R1-HQ WAN | Reachable | 4/5 replies | Pass |
| PC-HQ1 → HQ gateway | Reachable | 4/4 replies | Pass |
| PC-BR1 → Branch gateway | Reachable | 4/4 replies | Pass |
| PC-HQ1 → PC-BR1 | Reachable | 3/4 replies | Pass |
| PC-BR1 → PC-HQ1 | Reachable | 4/4 replies | Pass |

**Result:** Bidirectional end-to-end connectivity was verified between the headquarters and branch networks.

### Traceroute Evidence

A traceroute from PC-HQ1 to PC-BR1 produced the following path:

```text
tracert 192.168.30.10

1  192.168.10.1
2  10.0.0.2
3  192.168.30.10
```

The trace confirmed that traffic traversed both routers before reaching the destination.

Some individual traceroute probes timed out, but the trace completed.

ICMP Echo Replies with TTL 126 were also observed, consistent with an initial TTL of 128 being decremented by two routers.

### ARP and MAC Address Evidence

**PC-HQ1 ARP table**

```text
192.168.10.1 -> 0001.9781.2901
```

**R2-Branch ARP table**

```text
10.0.0.1 -> 0001.9781.2902
10.0.0.2 -> 0006.2A0B.C002
```

**SW1-HQ MAC address table**

```text
VLAN 1    0000.0cea.6405    Fa0/1
VLAN 1    0001.9781.2901    Gi0/1
```

These observations confirmed local IPv4-to-MAC resolution and dynamic Ethernet MAC address learning.

## 7. Troubleshooting

### Initial ICMP Timeouts

| Issue | Diagnosis | Resolution / Outcome |
|---|---|---|
| Initial ping requests timed out | Behavior was consistent with ARP resolution delays in Packet Tracer | Subsequent requests succeeded; no persistent connectivity failure was observed |
| Some traceroute probes timed out | Individual probe responses were not received | The complete path was successfully identified |

The initial ping failures were consistent with normal ARP resolution behavior, although ARP was not conclusively established as the cause of every timeout.

### Troubleshooting Approach

The lab demonstrated a structured verification process:

1. Verify physical connectivity and interface status.
2. Confirm IPv4 addressing and subnet masks.
3. Inspect connected and static routes.
4. Test local default-gateway connectivity.
5. Test remote-network connectivity.
6. Examine ARP and MAC address tables.
7. Use traceroute to inspect the routed path.

## 8. Key Concepts and Lessons Learned

### Layer 2 vs. Layer 3 Forwarding

Ethernet switches forward frames using MAC addresses, while routers forward IP packets based on destination IPv4 addresses and routing tables.

### ARP and Next-Hop Addressing

When communicating with a remote subnet, a host resolves the MAC address of its default gateway rather than the MAC address of the remote destination.

As packets pass through routers, the Ethernet framing changes at each routed hop, while the destination IPv4 address remains unchanged during normal routing.

### Static Routing and Return Paths

Static routes provide manually defined paths to remote networks.

Successful communication requires appropriate forward and return routes.

### Routing Table Interpretation

- `C` — Directly connected network
- `L` — Local interface host route
- `S` — Static route
- `[1/0]` — Administrative distance 1 and metric 0

### TTL and Traceroute

Routers decrement the IPv4 TTL field when forwarding packets. Traceroute uses TTL expiration behavior to identify intermediate routing devices.

### Engineering Takeaways

- Validate connectivity at each network layer rather than relying on a single successful ping.
- Confirm routing in both directions.
- Distinguish ARP tables from switch MAC address tables.
- Investigate initial packet loss before treating it as a persistent failure.
- Save and verify configurations to preserve network state.

## 9. Lab Outcome

**Final Status:** Completed

The lab successfully established and verified two-site IPv4 connectivity using Cisco routers, Ethernet switches, and static routing.

Both headquarters and branch endpoints communicated across the point-to-point WAN connection.

The completed topology provides the foundation for additional Project Snowden exercises.

### Limitations

- Static routing only; no dynamic routing protocol.
- No VLAN segmentation or inter-VLAN routing.
- Two endpoints reserved for future configuration.
- Configuration excerpts are verified summaries, not full running-configuration exports.

## 10. Supporting Files and References

### Supporting Files

- Completed Cisco Packet Tracer Lab 001 project (`.pkt`) in this directory
- [Network Topology Diagram](Snowdon%20Lab%20001%20Topology.png)
- This README containing verified configuration summaries and testing evidence

### References and Attribution

- Cisco IOS CLI and IPv4 networking concepts
- Project Snowden — independently developed network engineering lab

### Next Steps

**Lab 002 — VLAN Segmentation, Trunking, and Inter-VLAN Routing**

Planned additions:

- VLANs 10 and 20 at headquarters
- VLANs 30 and 40 at the branch
- IEEE 802.1Q trunk links
- Router-on-a-stick configuration
- Inter-VLAN connectivity testing

---

*Documented using Network Engineering Lab Report Standard v1.0.*
