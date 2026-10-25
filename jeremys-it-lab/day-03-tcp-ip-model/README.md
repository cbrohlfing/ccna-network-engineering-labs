# Day 03 — TCP/IP Model and Packet Tracer Simulation Mode

**Course:** Jeremy's IT Lab — CCNA 200-301  
**Lab Type:** Guided Protocol Analysis  
**Platform:** Cisco Packet Tracer  
**Status:** Completed  
**Related Reading:** *Acing the CCNA Exam*, Volume 1, Chapter 4 — OSI and TCP/IP Models

---

## 1. Lab Overview

This lab introduced Cisco Packet Tracer's Simulation Mode as a tool for observing network traffic and understanding the functions of the OSI and TCP/IP layers.

Using a preconfigured network topology provided by Jeremy's IT Lab, I followed the guided exercise to examine Spanning Tree Protocol (STP), Open Shortest Path First (OSPF), and Dynamic Host Configuration Protocol (DHCP) traffic.

The focus was on identifying protocol information at different layers, observing encapsulation, and understanding how Packet Tracer represents network communication.

No network configuration changes were required.

## 2. Learning Objectives

- Navigate Cisco Packet Tracer's Simulation Mode.
- Inspect protocol data units (PDUs) and their associated layer information.
- Identify Layer 1, Layer 2, and Layer 3 information.
- Observe application-layer traffic and its encapsulation.
- Generate DHCP traffic using command-line utilities.
- Relate network protocols to the OSI and TCP/IP models.
- Understand how Simulation Mode can assist with future troubleshooting.

## 3. Network Topology

The lab used Jeremy's preconfigured Packet Tracer topology.

### Devices

| Device | Role |
|---|---|
| R1 | Router |
| R2 | Router |
| SW1 | Switch |
| SW2 | Switch |
| PC1 | Client workstation |
| SRV1 | Server |

### Network Overview

The topology contained two IPv4 networks:

- `192.168.1.0/24` — Client/server LAN
- `10.0.0.0/24` — Router-to-router network

The switches connected devices within the local network, while the routers provided connectivity between the two IP networks.

The existing topology was used without modification.

## 4. Addressing and Design

The following addressing information was identified in the guided lab:

| Device / Interface | IPv4 Address | Network |
|---|---|---|
| SRV1 | `192.168.1.100` | `192.168.1.0/24` |
| R1 G0/0 | `192.168.1.1` | `192.168.1.0/24` |
| R1 G0/1 | `10.0.0.1` | `10.0.0.0/24` |
| R2 G0/0 | `10.0.0.2` | `10.0.0.0/24` |
| PC1 | DHCP-assigned | `192.168.1.0/24` |

The topology was already configured. The exercise did not require assigning IP addresses, configuring routing, or modifying switch settings.

## 5. Implementation

### Step 1 — Examine Network Traffic

Opened Packet Tracer's **Simulation Mode** and inspected existing protocol traffic.

**STP traffic**

- Selected an STP PDU originating from SW2.
- Examined the Layer 2 IEEE 802.3 header.
- Observed information associated with Ethernet frame encapsulation.
- Reviewed Layer 1 information identifying outgoing physical interfaces.

**OSPF traffic**

- Selected an OSPF PDU associated with R1.
- Examined information at Layers 1, 2, and 3.
- Identified source and destination IPv4 addressing in the Layer 3 information.
- Observed how a routing protocol uses lower-layer services to transmit messages.

### Step 2 — Generate DHCP Traffic

Opened the command prompt on PC1 through:

`PC1 → Desktop → Command Prompt`

Used the following commands:

```text
ipconfig
ipconfig /release
ipconfig /renew
```

These commands were used to inspect the current IP configuration, release the DHCP-assigned address, and request an address again.

### Step 3 — Inspect DHCP Encapsulation

In Simulation Mode:

- Selected generated DHCP traffic.
- Inspected the OSI Model view.
- Observed application-layer information at Layer 7.
- Examined UDP information at Layer 4.
- Reviewed Layer 3, Layer 2, and Layer 1 information.
- Used the simulation playback controls to observe traffic movement.

## 6. Verification and Testing

This was an observational lab rather than a connectivity-configuration exercise.

| Observation | Expected behavior | Result |
|---|---|---|
| STP inspection | Layer 2 and Layer 1 information visible | Observed during guided lab |
| OSPF inspection | Layer 3 IP information visible alongside lower layers | Observed during guided lab |
| DHCP release/renew | DHCP traffic generated in Simulation Mode | Observed during guided lab |
| DHCP PDU inspection | Application, transport, network, data link, and physical information visible | Observed during guided lab |
| Simulation playback | Protocol events can be examined sequentially | Completed during guided lab |

No independent ping tests, routing-table verification, or configuration validation were performed as part of this exercise.

## 7. Troubleshooting

No configuration problems or troubleshooting incidents were reported during the guided exercise.

The primary troubleshooting-related skill introduced was using **Simulation Mode** to inspect traffic at different protocol layers.

This provides a foundation for future investigations involving addressing, encapsulation, switching, routing, and protocol behavior.

## 8. Key Concepts and Lessons Learned

### Protocols operate at different layers

The simulation demonstrated that protocols have different responsibilities:

| Protocol | Primary layer | Purpose |
|---|---|---|
| STP | Layer 2 — Data Link | Helps prevent switching loops |
| OSPF | Layer 3 — Network | Exchanges routing information |
| DHCP | Application | Provides automatic IP configuration |
| UDP | Layer 4 — Transport | Transports DHCP messages |
| Ethernet | Layers 1 and 2 | Physical transmission and local frame delivery |

### Encapsulation is observable

Packet Tracer's PDU inspection tools make the encapsulation process visible.

Application data is carried by transport-layer protocols, encapsulated in network-layer packets, and transmitted using data-link frames and physical signaling.

### The OSI model is useful for analysis

Although TCP/IP is the protocol suite used by modern networks, the OSI model provides a useful reference for examining protocol behavior.

Packet Tracer displays application-layer information under Layer 7, while Layers 5 and 6 may have no separate information for typical TCP/IP traffic.

### Simulation Mode supports troubleshooting

Simulation Mode can help identify where communication is occurring, which protocols are involved, and how network devices process traffic.

It is a useful complement to Cisco IOS commands and connectivity tests.

## 9. Lab Outcome

**Status: Completed**

Successfully followed the guided Packet Tracer exercise and examined STP, OSPF, and DHCP traffic through Simulation Mode.

The lab reinforced concepts from Chapter 4 of *Acing the CCNA Exam*, including:

- OSI and TCP/IP layer responsibilities
- Protocol encapsulation
- Network-layer IP addressing
- Data-link framing
- Transport-layer communication
- Application-layer protocols

The associated Chapter 4 knowledge assessment was completed with a score of **10/10 (100%)**.

This exercise established a foundation for using Packet Tracer Simulation Mode in future networking labs.

## 10. Supporting Files and References

### Lab Files

| File | Description |
|---|---|
| `day-03-tcp-ip-model.pkt` | Original Jeremy's IT Lab Packet Tracer exercise file — pending upload |

The original Packet Tracer exercise file is retained without configuration changes because this lab involved protocol observation rather than network modification.

### References

- **Jeremy's IT Lab:** CCNA 200-301 course, Day 03 — TCP/IP Model and associated lab
- **Jeremy McDowell:** *Acing the CCNA Exam*, Volume 1, Chapter 4
- **Cisco Packet Tracer:** Simulation Mode and PDU inspection tools

### Attribution

The network topology and guided exercise were created by Jeremy's IT Lab. This report documents my participation, observations, and learning outcomes. It does not represent the original topology or exercise as my own design.
