# Project Snowden

## Enterprise Network Engineering Lab

**Project Type:** Independent Network Engineering  
**Platform:** Cisco Packet Tracer  
**Status:** Active Development

Project Snowden is an evolving, multi-site Cisco networking project designed to develop practical network engineering, configuration, verification, and troubleshooting skills.

Unlike guided training exercises, Project Snowden is a progressive network built through independently documented lab scenarios.

The project begins with foundational network connectivity and progressively introduces more advanced enterprise networking technologies.

## Project Origin and Development

Project Snowden was independently designed and built from scratch in Cisco Packet Tracer as a progressive enterprise network engineering project.

Project Snowden is designed, implemented, and documented independently of guided CCNA training exercises.

The project provides an environment for independently practicing network design, device configuration, connectivity verification, troubleshooting, and technical documentation.

Future labs will expand upon the existing infrastructure, introducing additional technologies and increasingly complex network engineering scenarios.

## Network Environment

The initial network consists of:

- Cisco 2911 routers
- Cisco Catalyst 2960 switches
- Headquarters (HQ) and branch office networks
- Separate IPv4 LAN subnets
- An IPv4 point-to-point WAN connection
- Static routing between locations

The existing infrastructure will be expanded and modified as additional technologies are introduced.

## Lab Index

Each lab builds upon the existing network environment and documents the technologies implemented, configuration decisions, verification results, and engineering lessons learned.

### Completed Labs

| Lab | Description | Technologies | Documentation |
|---|---|---|---|
| Lab 001 — Two-Site Network Connectivity | Establish IPv4 connectivity between headquarters and a remote branch office | IPv4 addressing, static routing, Ethernet switching, ARP, ICMP, traceroute | [View Lab 001](lab-001-two-site-connectivity/README.md) |

### Planned Labs

| Lab | Description | Planned Technologies |
|---|---|---|
| Lab 002 — VLAN Segmentation, Trunking, and Inter-VLAN Routing | Introduce network segmentation and enable communication between VLANs | VLANs, IEEE 802.1Q trunking, router-on-a-stick |
| Lab 003+ — Future Network Engineering Scenarios | Expand the network with additional enterprise networking technologies | To be determined |

Additional labs will be added as Project Snowden develops.

## Lab Documentation Standards

Every completed Project Snowden lab follows the **Network Engineering Lab Report Standard v1.0**.

Each lab report contains the following sections:

1. Lab Overview
2. Learning Objectives
3. Network Topology
4. Addressing and Design
5. Implementation
6. Verification and Testing
7. Troubleshooting
8. Key Concepts and Lessons Learned
9. Lab Outcome
10. Supporting Files and References

Reports include verified configurations, technical observations, and supporting evidence where applicable.

[View the Master Lab Report Template](../templates/NETWORK_LAB_REPORT_TEMPLATE.md)

## Engineering Approach

Project Snowden follows a progressive engineering workflow.

**Design:** Define network requirements, topology, addressing, and intended behavior.

**Implement:** Configure the required Cisco devices and network technologies.

**Verify:** Confirm operational behavior through CLI commands, connectivity testing, and network inspection.

**Troubleshoot:** Investigate unexpected behavior and document findings and corrections.

**Document:** Record configuration summaries, test results, technical decisions, and lessons learned in a standardized report.

This approach is intended to develop repeatable engineering practices rather than simply complete configuration exercises.

## Project Goals

1. Develop practical Cisco networking and troubleshooting skills.
2. Build and maintain an evolving enterprise-style network.
3. Practice independent network design, implementation, and verification.
4. Document technical decisions, configurations, and network changes.
5. Develop systematic troubleshooting procedures.
6. Create a professional networking portfolio demonstrating practical engineering experience.

## Related Resources

- [CCNA Network Engineering Portfolio](../README.md) — Main repository and completed lab index
- [Network Engineering Notes](../network-engineering-notes/README.md) — Technical references and networking concepts
- [Jeremy's IT Lab](../jeremys-it-lab/README.md) — Guided CCNA exercises documented separately

---

*Project Snowden is an independent educational network engineering project developed during preparation for the Cisco CCNA certification.*
