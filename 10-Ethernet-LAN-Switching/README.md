
# Ethernet LAN Switching

This section contains my study notes, concepts, commands, observations, and practical understanding of **Ethernet LAN Switching**.

The main focus is understanding how Ethernet networks operate at **OSI Layer 1 and Layer 2**, how Ethernet frames are structured, how switches learn MAC addresses, and how hosts use ARP and ICMP to communicate.

---

# Table of Contents

1. [OSI Model – Physical Layer](#1-osi-model--physical-layer)
2. [OSI Model – Data Link Layer](#2-osi-model--data-link-layer)
3. [LANs](#3-lans)
4. [OSI Model – PDUs](#4-osi-model--pdus)
5. [Ethernet Frame](#5-ethernet-frame)
   - [Preamble and SFD](#51-preamble-and-sfd)
   - [Ethernet Frame Minimum Size](#52-ethernet-frame-minimum-size)
   - [Destination and Source MAC](#53-destination-and-source-mac)
   - [Type / Length](#54-type--length)
   - [Frame Check Sequence](#55-frame-check-sequence-fcs)
6. [Ethernet Standards](#6-ethernet-standards)
7. [MAC Addresses](#7-mac-addresses)
8. [Decimal and Hexadecimal](#8-decimal-and-hexadecimal)
9. [Ethernet LAN Switching](#9-ethernet-lan-switching)
10. [ARP](#10-arp)
11. [ARP Request](#11-arp-request)
12. [Ping](#12-ping)
13. [Useful Cisco Commands](#13-useful-cisco-commands)
14. [Key Takeaways](#14-key-takeaways)
15. [Troubleshooting Mental Model](#15-troubleshooting-mental-model)

---

# 1. OSI Model – Physical Layer

The **Physical Layer (Layer 1)** is responsible for transmitting raw bits across the physical medium.

At Layer 1, data is represented as:

```text
0 and 1
````

Layer 1 does not understand:

* MAC addresses
* IP addresses
* TCP
* UDP
* Applications
* Ethernet switching logic

Its job is simply to move bits from one device to another through a physical medium.

## Examples of Layer 1 media

* Copper Ethernet cables
* Fibre-optic cables
* Radio/wireless signals
* Electrical signals
* Light signals

The important idea is:

```text
Layer 1 = Bits + Physical Medium
```

---

# 2. OSI Model – Data Link Layer

The **Data Link Layer (Layer 2)** is responsible for communication between devices on the same local network.

Important Layer 2 concepts include:

* Ethernet
* MAC addresses
* Ethernet frames
* Switches
* VLANs
* Frame forwarding
* Frame checking
* ARP-related Layer 2 delivery

The Data Link Layer is commonly divided conceptually into:

```text
Data Link Layer
        |
        +---- LLC
        |
        +---- MAC
```

The **MAC (Media Access Control)** portion is particularly important for Ethernet switching.

Cisco Ethernet switches primarily operate at **Layer 2**.

---

# 3. LANs

LAN stands for:

> Local Area Network

A LAN connects devices within a relatively local geographical area.

Examples include:

* Home networks
* Office networks
* University networks
* Computer labs
* Enterprise floors
* Building networks

## Typical LAN devices

* PCs
* Servers
* Printers
* Switches
* Access points
* Routers

A typical Ethernet LAN commonly uses switches to connect end devices.

Example:

```text
             +--------+
             | Switch |
             +--------+
              /   |   \
             /    |    \
           PC1   PC2   PC3
```

The switch provides Layer 2 connectivity between the devices.

---

# 4. OSI Model – PDUs

PDU stands for:

> Protocol Data Unit

A PDU is the name given to data as it moves through the different layers of the OSI model.

The common PDU names are:

| OSI Layer              | PDU                |
| ---------------------- | ------------------ |
| Layer 7 - Application  | Data               |
| Layer 6 - Presentation | Data               |
| Layer 5 - Session      | Data               |
| Layer 4 - Transport    | Segment / Datagram |
| Layer 3 - Network      | Packet             |
| Layer 2 - Data Link    | Frame              |
| Layer 1 - Physical     | Bits               |

For Ethernet switching, the most important PDU is:

```text
Layer 2 = Frame
```

At Layer 1, the frame is converted into bits for transmission over the physical medium.

---

# 5. Ethernet Frame

An Ethernet frame is the Layer 2 PDU used by Ethernet networks.

A simplified Ethernet frame can be represented as:

```text
+----------+-----+----------+----------+-------------+------+
| Preamble | SFD | Dest MAC | Src MAC  | Type/Length | FCS  |
+----------+-----+----------+----------+-------------+------+
    7 B      1 B     6 B        6 B          2 B        4 B
```

The major components are:

1. Preamble
2. Start Frame Delimiter (SFD)
3. Destination MAC address
4. Source MAC address
5. Type / Length
6. Payload
7. Frame Check Sequence (FCS)

---

## 5.1 Preamble and SFD

### Preamble

The Ethernet preamble is used for synchronization between the sender and receiver.

It is:

```text
7 bytes
```

The preamble consists of a repeating bit pattern used to allow the receiving device to synchronize with the incoming frame.

---

## Start Frame Delimiter (SFD)

SFD stands for:

> Start Frame Delimiter

The SFD indicates that the actual Ethernet frame is about to begin.

Size:

```text
1 byte
```

The SFD value is commonly represented as:

```text
10101011
```

Therefore:

```text
Preamble = 7 bytes
SFD      = 1 byte
```

---

# 5.2 Ethernet Frame Minimum Size

An important Ethernet concept is the minimum Ethernet frame size.

The minimum Ethernet frame size is:

```text
64 bytes
```

This is measured from:

```text
Destination MAC
        ↓
Source MAC
        ↓
Type/Length
        ↓
Payload
        ↓
FCS
```

The preamble and SFD are not included in the 64-byte Ethernet frame size.

The minimum frame size was historically important for Ethernet collision detection.

---

# 5.3 Destination and Source MAC

Every Ethernet frame contains:

```text
Destination MAC Address
Source MAC Address
```

Each MAC address is:

```text
48 bits
6 bytes
12 hexadecimal digits
```

Common formats include:

```text
AA:BB:CC:DD:EE:FF
```

or:

```text
AA-BB-CC-DD-EE-FF
```

or Cisco's commonly used format:

```text
AABB.CCDD.EEFF
```

Example:

```text
00D0.FFC4.0E8B
```

---

## Source MAC

The source MAC identifies the device that transmitted the Ethernet frame.

Example:

```text
Source MAC:
00D0.FFC4.0E8B
```

---

## Destination MAC

The destination MAC identifies the intended Layer 2 destination.

Example:

```text
Destination MAC:
0040.0BC6.7651
```

A switch uses the destination MAC address to determine where to forward the frame.

---

# 5.4 Type / Length

The Ethernet Type/Length field is:

```text
2 bytes
```

This field can identify the protocol carried inside the Ethernet frame.

For example:

```text
0x0800 = IPv4
0x86DD = IPv6
```

The decimal representation of:

```text
0x0800
```

is:

```text
2048
```

The field has two interpretations depending on its value:

```text
Value > 1536
        ↓
EtherType

Value <= 1500
        ↓
Length
```

Important example:

```text
0x0800
```

means:

```text
IPv4
```

And:

```text
0x86DD
```

means:

```text
IPv6
```

---

# 5.5 Frame Check Sequence (FCS)

FCS stands for:

> Frame Check Sequence

FCS is located at the end of the Ethernet frame.

Size:

```text
4 bytes
```

The FCS is used to detect errors that may have occurred during transmission.

Ethernet uses a CRC-based calculation for this purpose.

CRC stands for:

> Cyclic Redundancy Check

The important relationship is:

```text
Layer 2
   |
   +---- Ethernet Frame
             |
             +---- FCS
```

Therefore, whenever I see:

```text
FCS
CRC
Frame Check Sequence
```

I should immediately associate it with:

```text
OSI Layer 2
Ethernet Frame
Error Detection
```

---

# Ethernet Frame Summary

A simplified Ethernet frame can be remembered as:

```text
Preamble
   ↓
SFD
   ↓
Destination MAC
   ↓
Source MAC
   ↓
Type / Length
   ↓
Payload
   ↓
FCS
```

Important sizes:

| Field           |    Size |
| --------------- | ------: |
| Preamble        | 7 bytes |
| SFD             |  1 byte |
| Destination MAC | 6 bytes |
| Source MAC      | 6 bytes |
| Type/Length     | 2 bytes |
| FCS             | 4 bytes |

---

# 6. Ethernet Standards

Ethernet has been defined and extended through IEEE 802.3 standards.

Important standards encountered during the study include:

| Standard | Description                           |
| -------- | ------------------------------------- |
| 802.3i   | 10BASE-T                              |
| 802.3u   | Fast Ethernet                         |
| 802.3ab  | Gigabit Ethernet                      |
| 802.3z   | Gigabit Ethernet over fibre           |
| 802.3ae  | 10 Gigabit Ethernet                   |
| 802.3an  | 10 Gigabit Ethernet over twisted-pair |

Example from the study notes:

```text
802.3z
1000BASE-LX
```

Typical reach depends on the fibre and implementation.

The important idea is that Ethernet standards define how Ethernet operates over different physical media and speeds.

---

# 7. MAC Addresses

MAC stands for:

> Media Access Control

A MAC address is a Layer 2 hardware address used for Ethernet communication.

## MAC address size

A standard Ethernet MAC address contains:

```text
48 bits
=
6 bytes
=
12 hexadecimal digits
```

Example:

```text
00:D0:FF:C4:0E:8B
```

Cisco format:

```text
00D0.FFC4.0E8B
```

---

# MAC Address and OSI Layer

A very important exam concept:

```text
MAC Address
     ↓
Layer 2
     ↓
Data Link Layer
```

Do not confuse:

```text
MAC address → Layer 2
IP address  → Layer 3
```

---

# Switch MAC Address Table

A Layer 2 switch maintains a MAC address table.

The switch dynamically learns MAC addresses by examining the **source MAC address** of incoming Ethernet frames.

Conceptually:

```text
PC1
 |
 | Frame
 ↓
Switch
 |
 +---- Learns PC1's Source MAC
 |
 +---- Associates MAC with incoming port
```

Example:

```text
MAC Address        Port
-------------------------
AAAA.BBBB.CCCC     Fa0/1
DDDD.EEEE.FFFF     Fa0/2
```

The switch can then use this information to make forwarding decisions.

---

# Dynamically Learned MAC Address

Switches normally learn MAC addresses dynamically.

The basic process is:

```text
Frame arrives
      ↓
Switch examines Source MAC
      ↓
Switch checks MAC table
      ↓
Source MAC is learned
      ↓
MAC is associated with incoming interface
```

This is one of the fundamental mechanisms behind Ethernet switching.

---

# Clearing Dynamic MAC Addresses

A dynamic MAC address entry can be cleared from the MAC address table.

Example command:

```text
clear mac address-table dynamic interface <interface-id>
```

Example:

```text
clear mac address-table dynamic interface fa0/1
```

This removes dynamically learned MAC addresses associated with the specified interface.

---

# 8. Decimal and Hexadecimal

Networking frequently uses both decimal and hexadecimal representations.

## Decimal

Decimal is base 10.

Digits:

```text
0 1 2 3 4 5 6 7 8 9
```

Example:

```text
2048
```

---

# Hexadecimal

Hexadecimal is base 16.

Digits:

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

Where:

```text
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

Hexadecimal is heavily used in networking because it provides a compact representation of binary values.

For example:

```text
0x0800
```

represents:

```text
2048
```

And:

```text
0x86DD
```

represents the EtherType for IPv6.

---

# Why MAC Addresses Use Hexadecimal

A MAC address contains:

```text
48 bits
```

Writing 48 bits as binary would be difficult to read.

Instead, hexadecimal is used.

Example:

```text
Binary:
10101010 10111011 11001100 11011101 11101110 11111111
```

Can be represented more conveniently as:

```text
AA:BB:CC:DD:EE:FF
```

Therefore:

```text
48 bits
=
6 bytes
=
12 hexadecimal digits
```

---

# 9. Ethernet LAN Switching

Ethernet switching is primarily a **Layer 2 operation**.

A switch receives Ethernet frames and decides where those frames should be forwarded.

The most important information used by a Layer 2 switch is:

```text
Source MAC
Destination MAC
Incoming Interface
MAC Address Table
```

---

# Basic Switching Process

Consider:

```text
PC1 -------- Switch -------- PC2
```

Suppose PC1 sends a frame to PC2.

The process is approximately:

```text
PC1
 |
 | Ethernet Frame
 | Source MAC = PC1
 | Destination MAC = PC2
 ↓
Switch
 |
 +---- Learn Source MAC
 |
 +---- Search Destination MAC
 |
 +---- Forward / Flood
 |
 ↓
PC2
```

---

# Source MAC Learning

When a frame enters a switch:

```text
Frame arrives
      ↓
Switch reads Source MAC
      ↓
Switch checks MAC table
      ↓
Switch learns Source MAC
      ↓
MAC → Incoming Port
```

Example:

```text
PC1 MAC = AAAA.BBBB.CCCC
PC1 connected to Fa0/1
```

The switch may learn:

```text
AAAA.BBBB.CCCC → Fa0/1
```

---

# Known Unicast

If the destination MAC is already known:

```text
Destination MAC
       ↓
MAC table lookup
       ↓
MAC found
       ↓
Forward only through associated port
```

Example:

```text
PC1 ---- Fa0/1
          |
        Switch
          |
       Fa0/2 ---- PC2
```

If the switch knows:

```text
PC2 MAC → Fa0/2
```

the frame can be forwarded directly to:

```text
Fa0/2
```

It does not need to send the frame out every other port.

---

# Unknown Unicast

If the destination MAC is not in the MAC address table, the switch does not yet know where the destination is.

The switch floods the frame out the appropriate ports within the same broadcast domain, except the port on which the frame was received.

Conceptually:

```text
Unknown Destination MAC
          ↓
       Switch
      /   |   \
     /    |    \
   PC1   PC2   PC3
```

The switch floods the frame so the destination can respond.

Once the destination responds, the switch can learn its MAC address from the source MAC of the response.

---

# Broadcast

A broadcast Ethernet frame is intended for all devices in the broadcast domain.

The Ethernet broadcast MAC address is:

```text
FF:FF:FF:FF:FF:FF
```

Cisco format:

```text
FFFF.FFFF.FFFF
```

Switches flood broadcast frames within the appropriate Layer 2 domain.

Examples of traffic that can involve Layer 2 broadcast behavior include ARP requests.

---

# Important Switching Terms

| Term            | Meaning                                            |
| --------------- | -------------------------------------------------- |
| Source MAC      | MAC address of the sender                          |
| Destination MAC | MAC address of intended Layer 2 receiver           |
| MAC table       | Table mapping MAC addresses to switch interfaces   |
| Known unicast   | Destination MAC is known                           |
| Unknown unicast | Destination MAC is not known                       |
| Broadcast       | Destination is all devices in the broadcast domain |
| Flooding        | Sending a frame out multiple appropriate ports     |

---

# 10. ARP

ARP stands for:

> Address Resolution Protocol

ARP is used to discover the MAC address associated with an IPv4 address on the local network.

The important relationship is:

```text
IPv4 Address
      ↓
ARP
      ↓
MAC Address
```

For example, a PC may know:

```text
192.168.100.102
```

but need to discover:

```text
00AA.BBCC.DDEE
```

ARP provides this mapping.

---

# Why ARP Is Needed

Applications generally communicate using IP addresses.

Ethernet delivers frames using MAC addresses.

Therefore, when a host wants to communicate with another IPv4 host on the local network, it may need to determine:

```text
IP address → MAC address
```

ARP performs this resolution.

---

# ARP Process

Suppose:

```text
PC1:
IP = 192.168.100.101

PC2:
IP = 192.168.100.102
```

PC1 wants to communicate with PC2.

PC1 may first ask:

```text
Who has 192.168.100.102?
```

This is an ARP Request.

The ARP request is broadcast at Layer 2.

Conceptually:

```text
PC1
 |
 | ARP Request
 | "Who has 192.168.100.102?"
 ↓
Switch
 / | \
/  |  \
PC2 PC3 PC4
```

PC2 recognizes that the requested IP address belongs to it.

PC2 responds with its MAC address.

---

# ARP Request

An ARP Request is typically broadcast.

The Ethernet destination MAC is:

```text
FFFF.FFFF.FFFF
```

The message is effectively asking:

```text
Who has this IP address?
```

The device owning that IP address responds with its MAC address.

The result is:

```text
IP Address
     ↓
MAC Address
```

The host can then use that MAC address when constructing an Ethernet frame.

---

# ARP Summary

```text
Host knows:
192.168.100.102

Host needs:
MAC address

        ↓

ARP Request

        ↓

"Who has 192.168.100.102?"

        ↓

Destination responds

        ↓

MAC address learned

        ↓

Ethernet frame can be constructed
```

---

# 11. Ping

`ping` is commonly used to test IP connectivity.

Ping uses:

> ICMP — Internet Control Message Protocol

A normal ping uses:

```text
ICMP Echo Request
        ↓
ICMP Echo Reply
```

Example:

```text
PC1> ping 192.168.100.102
```

If successful:

```text
Reply from 192.168.100.102
```

---

# What Happens During a Ping?

Suppose:

```text
PC1 = 192.168.100.101
PC2 = 192.168.100.102
```

PC1 wants to ping PC2.

A simplified sequence is:

```text
PC1
 |
 | 1. Determine destination
 |
 | 2. ARP if MAC address is unknown
 |
 | 3. Build Ethernet frame
 |
 | 4. Send ICMP Echo Request
 ↓
Switch
 |
 ↓
PC2
 |
 | 5. PC2 sends ICMP Echo Reply
 ↓
Switch
 |
 ↓
PC1
```

Therefore, a simple ping can involve multiple concepts:

```text
IP
 ↓
ARP
 ↓
MAC
 ↓
Ethernet Frame
 ↓
Switching
 ↓
ICMP
```

---

# Ping Is More Than "Just Ping"

When a ping works, several things may have worked correctly.

For example:

```text
Physical connectivity
        ↓
Ethernet
        ↓
MAC addressing
        ↓
Switching
        ↓
ARP
        ↓
IP addressing
        ↓
ICMP
        ↓
Echo Reply
```

This is why `ping` is such a useful troubleshooting tool.

---

# 12. Useful Cisco Commands

## Show MAC Address Table

```text
show mac address-table
```

This displays MAC addresses learned by the switch.

---

## Show Dynamic MAC Addresses

```text
show mac address-table dynamic
```

This focuses on dynamically learned MAC addresses.

---

## Clear Dynamic MAC Entries

```text
clear mac address-table dynamic
```

To clear dynamic entries associated with an interface:

```text
clear mac address-table dynamic interface <interface-id>
```

Example:

```text
clear mac address-table dynamic interface fa0/1
```

---

## Show VLAN Information

```text
show vlan brief
```

Useful for checking:

* VLANs
* Access ports
* Port membership

---

## Show Interface Status

```text
show interfaces status
```

Useful for quickly checking:

* Port status
* VLAN
* Speed
* Duplex
* Interface type

---

## Show Interface Details

```text
show interfaces
```

Provides detailed information about an interface.

---

## Show IP Interface Brief

```text
show ip interface brief
```

Useful for routers and Layer 3 interfaces.

---

## Test Connectivity

```text
ping <destination-ip>
```

Example:

```text
ping 192.168.100.1
```

---

# 13. Practical Ethernet Switching Workflow

When troubleshooting a basic Ethernet LAN, I should not immediately assume that the switch is broken.

I should work through the layers.

A useful troubleshooting sequence is:

```text
Physical Layer
      ↓
Interface Status
      ↓
VLAN Membership
      ↓
MAC Address Learning
      ↓
ARP
      ↓
IP Addressing
      ↓
Ping / ICMP
```

---

# Physical Layer Check

First verify:

```text
Is the cable connected?
Is the interface up?
Is the correct port being used?
```

Useful command:

```text
show interfaces status
```

Look for:

```text
connected
```

---

# VLAN Check

Verify that the port belongs to the expected VLAN.

Command:

```text
show vlan brief
```

Example:

```text
VLAN Name       Status    Ports
---- ---------- --------- ----------
1    default    active    Fa0/1
```

---

# MAC Learning Check

After devices communicate, check whether the switch has learned their MAC addresses.

Command:

```text
show mac address-table
```

Look for:

```text
MAC Address        Port
-------------------------
AAAA.BBBB.CCCC     Fa0/1
DDDD.EEEE.FFFF     Fa0/2
```

This tells us that the switch has associated those MAC addresses with specific interfaces.

---

# ARP Check

On an end host, ARP information can be inspected using:

```text
arp -a
```

The ARP table can show mappings such as:

```text
IP Address          MAC Address
192.168.100.102     xxxx.xxxx.xxxx
```

This helps determine whether the host has resolved an IPv4 address to a MAC address.

---

# Ping Check

Finally:

```text
ping <destination-ip>
```

Example:

```text
ping 192.168.100.102
```

If ping succeeds, the Layer 2 and Layer 3 path is functioning sufficiently for that traffic.

---

# 14. Key Takeaways

## OSI Layers

The Ethernet switching topics are mainly concentrated around:

```text
Layer 1 → Physical
Layer 2 → Data Link
Layer 3 → Network
```

The most important relationship is:

```text
Bits       → Layer 1
Frames     → Layer 2
Packets    → Layer 3
Segments   → Layer 4
```

---

# Ethernet

Ethernet is primarily associated with:

```text
Layer 2
```

Ethernet uses:

```text
MAC Addresses
Ethernet Frames
Switches
```

---

# MAC Address

Remember:

```text
48 bits
6 bytes
12 hexadecimal digits
```

Example:

```text
AABB.CCDD.EEFF
```

---

# Ethernet Frame

Remember the major fields:

```text
Preamble
SFD
Destination MAC
Source MAC
Type/Length
Payload
FCS
```

Important sizes:

```text
Preamble = 7 bytes
SFD      = 1 byte
MAC      = 6 bytes each
Type     = 2 bytes
FCS      = 4 bytes
```

---

# FCS

Remember:

```text
FCS
 ↓
Layer 2
 ↓
Ethernet Frame
 ↓
Error Detection
 ↓
CRC
```

---

# Switch

A switch primarily operates at:

```text
Layer 2
```

It learns:

```text
Source MAC → Incoming Port
```

It then uses the destination MAC address to decide where to forward the frame.

---

# ARP

Remember:

```text
ARP
 ↓
IPv4 Address → MAC Address
```

An ARP Request is typically broadcast.

Example:

```text
"Who has 192.168.100.102?"
```

---

# Ping

Ping commonly uses:

```text
ICMP
```

The basic process is:

```text
Echo Request
      ↓
Echo Reply
```

But before successful communication can occur on a local Ethernet network, ARP and Layer 2 delivery may also be involved.

---

# 15. Troubleshooting Mental Model

One of the most useful lessons from this topic is to think in layers instead of guessing.

When a host cannot communicate, ask:

```text
1. Is the physical connection working?
             ↓
2. Is the switch port connected?
             ↓
3. Is the port in the correct VLAN?
             ↓
4. Is the switch learning the source MAC?
             ↓
5. Does the switch know the destination MAC?
             ↓
6. Is ARP resolving the IPv4 address?
             ↓
7. Does the host have the correct IP address?
             ↓
8. Does ping succeed?
```

This approach prevents random configuration changes.

---

# Final Mental Model

The complete Ethernet communication process can be visualised as:

```text
Application
     ↓
Transport
     ↓
IP / Network Layer
     ↓
ARP resolves IP → MAC
     ↓
Ethernet Frame
     ↓
Source MAC + Destination MAC
     ↓
Switch examines MAC table
     ↓
Frame forwarded / flooded
     ↓
Physical transmission
     ↓
Bits
```

And in the reverse direction:

```text
Bits
 ↓
Physical Layer
 ↓
Ethernet Frame
 ↓
Destination MAC
 ↓
Switching
 ↓
IP Packet
 ↓
Transport
 ↓
Application
```

---

# Quick Revision Sheet

| Concept                | Remember                   |
| ---------------------- | -------------------------- |
| LAN                    | Local Area Network         |
| Ethernet               | Mainly Layer 2             |
| Switch                 | Mainly Layer 2             |
| MAC                    | Layer 2                    |
| IP                     | Layer 3                    |
| Frame                  | Layer 2 PDU                |
| Packet                 | Layer 3 PDU                |
| Bits                   | Layer 1 PDU                |
| MAC size               | 48 bits / 6 bytes          |
| MAC representation     | Hexadecimal                |
| Ethernet frame minimum | 64 bytes                   |
| SFD                    | 1 byte                     |
| Preamble               | 7 bytes                    |
| FCS                    | 4 bytes                    |
| FCS purpose            | Error detection            |
| CRC                    | Cyclic Redundancy Check    |
| IPv4 EtherType         | 0x0800                     |
| IPv6 EtherType         | 0x86DD                     |
| ARP                    | IPv4 → MAC resolution      |
| ARP Request            | Broadcast                  |
| Broadcast MAC          | FFFF.FFFF.FFFF             |
| Ping                   | Uses ICMP                  |
| MAC learning           | Source MAC → incoming port |

---

# Core Commands

```text
show interfaces status

show vlan brief

show mac address-table

show mac address-table dynamic

clear mac address-table dynamic

clear mac address-table dynamic interface <interface-id>

show interfaces

show ip interface brief

ping <destination-ip>

arp -a
```

---

# Key Lesson

The most important thing I want to remember from Ethernet LAN Switching is:

> **A switch does not primarily make forwarding decisions using IP addresses. A Layer 2 Ethernet switch uses MAC addresses and its MAC address table to forward Ethernet frames.**

The overall relationship is:

```text
IP Address
    ↓
ARP
    ↓
MAC Address
    ↓
Ethernet Frame
    ↓
Switch
    ↓
MAC Address Table
    ↓
Forward / Flood
    ↓
Destination
```

This forms the foundation for understanding more advanced topics such as:

* VLANs
* Trunking
* STP / RSTP
* EtherChannel
* Inter-VLAN Routing
* Router-on-a-Stick
* HSRP
* DHCP
* ACLs
* NAT
* Enterprise network troubleshooting


