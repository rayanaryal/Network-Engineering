# Q01 — Inter-VLAN Routing and DHCP Troubleshooting Lab

## Scenario

A user can reach a server in the **same VLAN**, but cannot reach a server located in **another VLAN**.

This scenario can have several possible causes, including:

- A Layer 3 routing problem
- An incorrect default gateway
- An incorrect subnet mask
- A routed interface being down or incorrectly configured
- An ACL or other policy blocking the traffic

Rather than only answering the scenario theoretically, I built a working network from scratch in **Cisco Packet Tracer** to understand how VLANs, DHCP, default gateways, and routing work together.

---

## Lab Objectives

The objectives of this lab are to:

- Create two separate VLANs
- Place end devices into the correct VLANs
- Use separate IPv4 networks for each VLAN
- Configure router interfaces as the default gateways
- Configure the router as a DHCP server
- Dynamically assign IPv4 addressing to end devices
- Enable communication between the two networks
- Verify same-VLAN and inter-network connectivity
- Troubleshoot configuration problems encountered during the lab

The workflow for the lab is:

```text
Design the Networks
        ↓
Create the VLANs
        ↓
Assign Switchports
        ↓
Configure Router Interfaces
        ↓
Configure DHCP
        ↓
Obtain Client Addresses
        ↓
Test Connectivity
        ↓
Troubleshoot
        ↓
Verify End-to-End Communication
```

---

## Network Design

I used two separate networks and VLANs:

| Department | VLAN | Network | Default Gateway |
|---|---:|---|---|
| HR | 10 | `192.168.1.0/24` | `192.168.1.1` |
| Sales | 20 | `192.168.2.0/24` | `192.168.2.1` |

A single router connects both networks.

```text
             R1
        /           \
192.168.1.1       192.168.2.1
     |                 |
   VLAN 10           VLAN 20
     HR               Sales
     |                 |
    SW1               SW2
```

Because both networks are directly connected to the same router, a dynamic routing protocol is not required for communication between them.

---

> **Lab approach:** Build a fully working network first, understand why each component is required, test connectivity, and document any problems encountered during implementation.
