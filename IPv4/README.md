# IPv4 — Internet Protocol Version 4

This section contains my study notes and practical learning on **IPv4 (Internet Protocol Version 4)**.

The topics covered include:

- Introduction to IPv4
- Introduction to routing
- IPv4 addresses
- Decimal and hexadecimal numbers
- Binary numbers
- Binary-to-decimal conversion
- Decimal-to-binary conversion
- IPv4 address structure
- CIDR prefix length
- Loopback addresses
- Network addresses
- Broadcast addresses
- First and last usable host addresses
- Host calculations
- Cisco interface commands
- IPv4 address classes
- Classful IPv4 addressing
- Network ID, Broadcast ID and host ranges
- IPv4 packet structure
- IPv4 header
- IPv4 header fields
- IPv4 fragmentation
- TTL
- Protocol field
- Header checksum
- Source and destination IPv4 addresses
- IPv4 options
- Wireshark packet analysis
- IPv4 troubleshooting
- Practice questions

---

# 1. Introduction to Routing

A **router** is a Layer 3 networking device that connects different IP networks.

Routers make forwarding decisions using **IP addresses** and their routing tables.

For example:

```text
PC1
 |
SW1
 |
Router
 |
SW2
 |
PC2
```

If PC1 and PC2 are located on different IP networks, the router provides Layer 3 connectivity between them.

A router examines the **destination IP address** of a packet and determines where the packet should be forwarded.

---

# 2. IPv4 Addresses

IPv4 stands for:

**Internet Protocol Version 4**

An IPv4 address is:

- 32 bits long
- 4 bytes long
- Divided into four 8-bit octets
- Normally written using dotted-decimal notation

Example:

```text
192.168.1.254
```

Each octet can contain a value from:

```text
0 - 255
```

Because there are four octets and each octet contains 8 bits:

```text
8 + 8 + 8 + 8 = 32 bits
```

An IPv4 address can therefore be represented as:

```text
xxxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
```

where every `x` represents a binary bit.

---

# 3. Decimal and Hexadecimal

## Decimal

Decimal is **base 10**.

It uses ten digits:

```text
0 1 2 3 4 5 6 7 8 9
```

For example:

```text
192
255
10
172
```

IPv4 addresses are normally displayed using decimal notation.

Example:

```text
192.168.1.10
```

---

## Hexadecimal

Hexadecimal is **base 16**.

It uses:

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

The values are:

```text
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

Examples:

```text
10 decimal = A hexadecimal
15 decimal = F hexadecimal
16 decimal = 10 hexadecimal
255 decimal = FF hexadecimal
```

Hexadecimal is commonly encountered when working with:

- MAC addresses
- Ethernet frames
- Packet captures
- Network device identifiers

Example MAC address:

```text
00:D0:FF:C4:0E:8B
```

---

# 4. Binary — Base 2

Binary is **base 2**.

It uses only two digits:

```text
0
1
```

Each IPv4 octet contains 8 bits.

The place values of an 8-bit binary number are:

```text
128 64 32 16 8 4 2 1
```

For example:

```text
192
```

can be represented as:

```text
11000000
```

because:

```text
128 + 64 = 192
```

Therefore:

```text
192 = 11000000
```

Another example:

```text
255 = 11111111
```

because:

```text
128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255
```

---

# 5. Binary-to-Decimal Conversion

To convert binary to decimal, use the binary place values:

```text
128 64 32 16 8 4 2 1
```

## Example

Convert:

```text
11000000
```

Place the bits underneath the values:

```text
128 64 32 16 8 4 2 1
  1  1  0  0 0 0 0 0
```

Add the values where the bit is `1`:

```text
128 + 64 = 192
```

Therefore:

```text
11000000 = 192
```

## Another Example

Convert:

```text
10101010
```

```text
128 64 32 16 8 4 2 1
  1  0  1  0 1 0 1 0
```

Add:

```text
128 + 32 + 8 + 2 = 170
```

Therefore:

```text
10101010 = 170
```

---

# 6. Decimal-to-Binary Conversion

To convert decimal to binary, determine which binary place values are required.

The 8-bit place values are:

```text
128 64 32 16 8 4 2 1
```

## Example: 192

```text
192 = 128 + 64
```

Therefore:

```text
192 = 11000000
```

## Example: 10

```text
10 = 8 + 2
```

Therefore:

```text
10 = 00001010
```

## Example: 255

```text
255 = 128 + 64 + 32 + 16 + 8 + 4 + 2 + 1
```

Therefore:

```text
255 = 11111111
```

---

# 7. IPv4 Address Structure

An IPv4 address contains two conceptual parts:

```text
Network Portion + Host Portion
```

For example:

```text
192.168.1.10/24
```

The `/24` prefix means:

```text
24 bits = Network portion
8 bits  = Host portion
```

Therefore:

```text
Network bits: 24
Host bits:     8
```

The subnet mask is:

```text
255.255.255.0
```

Binary:

```text
11111111.11111111.11111111.00000000
```

The `1`s represent the network portion.

The `0`s represent the host portion.

---

# 8. CIDR Prefix Length

CIDR stands for:

**Classless Inter-Domain Routing**

A prefix length tells us how many bits belong to the network portion.

Examples:

```text
/8
/16
/24
```

For example:

```text
192.168.1.10/24
```

means:

```text
24 network bits
8 host bits
```

Another example:

```text
10.10.10.5/8
```

means:

```text
8 network bits
24 host bits
```

The number of host bits can be calculated using:

```text
Host bits = 32 - Prefix Length
```

---

# 9. Loopback Addresses

A loopback address is used by a device to communicate with itself.

The IPv4 loopback range is:

```text
127.0.0.0/8
```

The most commonly used loopback address is:

```text
127.0.0.1
```

It is commonly referred to as:

```text
localhost
```

Example:

```bash
ping 127.0.0.1
```

This tests the local TCP/IP stack without requiring communication with another device.

---

# 10. Network Address

The network address, also called the **Network ID (NID)**, identifies the network itself.

The host bits are all set to:

```text
0
```

Example:

```text
43.109.23.12/8
```

With a `/8` prefix, the first octet represents the network portion.

Therefore:

```text
Network ID = 43.0.0.0
```

The host portion is:

```text
109.23.12
```

---

# 11. Broadcast Address

The broadcast address is used to communicate with all hosts within a subnet.

For a subnet, the host bits of the broadcast address are all set to:

```text
1
```

Example:

```text
43.109.23.12/8
```

Network:

```text
43.0.0.0
```

Broadcast:

```text
43.255.255.255
```

---

# 12. First and Last Usable Host Addresses

For a normal IPv4 subnet:

```text
Network Address
First Usable Host
...
Last Usable Host
Broadcast Address
```

The network address and broadcast address are normally not assigned to hosts.

For example:

```text
Network:      192.168.1.0
First host:   192.168.1.1
Last host:    192.168.1.254
Broadcast:    192.168.1.255
```

---

# 13. Number of Hosts

The number of usable host addresses can be calculated using:

```text
2^n - 2
```

where:

```text
n = number of host bits
```

The `-2` accounts for:

- Network address
- Broadcast address

---

## Example: /24

An IPv4 address contains 32 bits.

For `/24`:

```text
32 - 24 = 8 host bits
```

Therefore:

```text
2^8 - 2
```

```text
256 - 2 = 254
```

So a `/24` network provides:

```text
254 usable host addresses
```

---

## Example: /16

```text
32 - 16 = 16 host bits
```

Therefore:

```text
2^16 - 2
```

```text
65,536 - 2 = 65,534
```

So:

```text
/16 = 65,534 usable hosts
```

---

# 14. IPv4 Address Classes

Traditional IPv4 addressing used five address classes:

- Class A
- Class B
- Class C
- Class D
- Class E

The first octet can be used to determine the class.

| Class | Range | First Binary Pattern | Purpose |
|---|---|---|---|
| A | 1–126 | `0xxxxxxx` | Large networks |
| B | 128–191 | `10xxxxxx` | Medium networks |
| C | 192–223 | `110xxxxx` | Smaller networks |
| D | 224–239 | `1110xxxx` | Multicast |
| E | 240–255 | `1111xxxx` | Experimental / reserved |

These class ranges were part of traditional **classful IPv4 addressing**.

Modern networks generally use **CIDR/classless addressing** instead.

---

# 15. Class A

Class A addresses traditionally have:

```text
First octet: 1–126
```

Binary pattern:

```text
0xxxxxxx
```

A traditional Class A network uses:

```text
/8
```

Example:

```text
43.109.23.12/8
```

Network ID:

```text
43.0.0.0
```

Broadcast:

```text
43.255.255.255
```

First usable host:

```text
43.0.0.1
```

Last usable host:

```text
43.255.255.254
```

Number of host bits:

```text
24
```

Maximum usable hosts:

```text
2^24 - 2 = 16,777,214
```

---

# 16. Class B

Class B addresses traditionally have:

```text
First octet: 128–191
```

Binary pattern:

```text
10xxxxxx
```

A traditional Class B network uses:

```text
/16
```

Example:

```text
129.221.23.13/16
```

Network ID:

```text
129.221.0.0
```

Broadcast:

```text
129.221.255.255
```

First usable host:

```text
129.221.0.1
```

Last usable host:

```text
129.221.255.254
```

Number of host bits:

```text
16
```

Maximum usable hosts:

```text
2^16 - 2 = 65,534
```

---

# 17. Class C

Class C addresses traditionally have:

```text
First octet: 192–223
```

Binary pattern:

```text
110xxxxx
```

A traditional Class C network uses:

```text
/24
```

Example:

```text
209.211.3.0/24
```

Network ID:

```text
209.211.3.0
```

Broadcast:

```text
209.211.3.255
```

Usable host range:

```text
209.211.3.1
-
209.211.3.254
```

Maximum usable hosts:

```text
2^8 - 2 = 254
```

---

# 18. Class D

Class D addresses are:

```text
224–239
```

Binary pattern:

```text
1110xxxx
```

Class D is used for:

**Multicast**

Class D addresses are not used for normal host addressing in the same way as Classes A, B and C.

---

# 19. Class E

Class E addresses are:

```text
240–255
```

Binary pattern:

```text
1111xxxx
```

They are traditionally associated with:

**Experimental / reserved purposes**

They are not normally used for ordinary host addressing.

---

# 20. Example — IPv4 Address Calculation

Consider:

```text
43.109.23.12/8
```

Because the prefix is `/8`:

```text
Network bits = 8
Host bits = 24
```

Network ID:

```text
43.0.0.0
```

Broadcast ID:

```text
43.255.255.255
```

First usable IP:

```text
43.0.0.1
```

Last usable IP:

```text
43.255.255.254
```

Maximum usable hosts:

```text
2^24 - 2
= 16,777,214
```

---

# 21. Example — /16

Consider:

```text
129.221.23.13/16
```

Network bits:

```text
16
```

Host bits:

```text
32 - 16 = 16
```

Network ID:

```text
129.221.0.0
```

Broadcast:

```text
129.221.255.255
```

First usable IP:

```text
129.221.0.1
```

Last usable IP:

```text
129.221.255.254
```

Maximum usable hosts:

```text
2^16 - 2
= 65,534
```

---

# 22. Example — /24

Consider:

```text
209.211.3.0/24
```

Network ID:

```text
209.211.3.0
```

Broadcast:

```text
209.211.3.255
```

Usable range:

```text
209.211.3.1
-
209.211.3.254
```

Maximum usable hosts:

```text
254
```

---

# 23. Cisco Router Interfaces

Cisco router interfaces can be inspected using:

```bash
show ip interface brief
```

This command provides a summary of:

- Interface name
- IP address
- Interface status
- Protocol status
- Configuration method

Example:

```text
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   192.168.100.1   YES manual up                    up
```

---

# 24. Interface Status

A Cisco interface has two important status indicators:

```text
Status
Protocol
```

For an operational interface, we normally want:

```text
Status: up
Protocol: up
```

Example:

```text
up                    up
```

This indicates that the physical and data-link portions of the interface are operational.

---

# 25. Configuring an IPv4 Address on a Router Interface

A router interface can be configured using:

```bash
Router(config)# interface GigabitEthernet0/0/0
Router(config-if)# ip address 192.168.100.1 255.255.255.0
Router(config-if)# no shutdown
```

The `ip address` command assigns the IPv4 address and subnet mask.

The:

```text
no shutdown
```

command enables the interface.

After configuration, verify it using:

```bash
show ip interface brief
```

---

# 26. IPv4 Packet Structure

When IPv4 data is transmitted across a network, IPv4 adds a header to the packet.

A simplified representation is:

```text
+-------------------------------+
|        IPv4 Header            |
+-------------------------------+
|            Data               |
+-------------------------------+
```

The IPv4 header contains information required to deliver and process the packet.

The header contains several fields, including:

- Version
- IHL
- DSCP
- ECN
- Total Length
- Identification
- Flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source Address
- Destination Address
- Options

---

# 27. IPv4 Header

The IPv4 header is at the beginning of an IPv4 packet.

The header contains control information used by network devices to process the packet.

The IPv4 header contains fields of different sizes.

Important fields include:

- Version
- IHL
- DSCP
- ECN
- Total Length
- Identification
- Flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source IP Address
- Destination IP Address
- Options

---

# 28. Version Field — 4 Bits

The Version field is:

```text
4 bits
```

It identifies which version of IP is being used.

For IPv4:

```text
Version = 4
```

The binary representation of 4 is:

```text
0100
```

Therefore, an IPv4 packet has:

```text
Version = 0100
```

---

# 29. Internet Header Length — IHL

The Internet Header Length (IHL) field is:

```text
4 bits
```

It indicates the length of the IPv4 header.

The normal IPv4 header without options is:

```text
20 bytes
```

The IHL value is measured in:

```text
32-bit words
```

Therefore:

```text
IHL = 5
```

represents:

```text
5 × 4 bytes = 20 bytes
```

If IPv4 options are present, the header becomes longer.

The maximum IHL value is:

```text
15
```

Therefore the maximum IPv4 header size is:

```text
15 × 4 = 60 bytes
```

---

# 30. DSCP Field

The Differentiated Services Code Point (DSCP) field is:

```text
6 bits
```

It is used to classify IP traffic.

DSCP can be used with Quality of Service (QoS) mechanisms to indicate how traffic should be treated.

For example, network devices can use traffic classifications to provide different forwarding behaviour to different types of traffic.

---

# 31. ECN Field

The Explicit Congestion Notification (ECN) field is:

```text
2 bits
```

ECN provides a mechanism for indicating network congestion without necessarily dropping packets.

It works together with congestion-aware transport protocols such as TCP.

---

# 32. Total Length Field

The IPv4 Total Length field is:

```text
16 bits
```

It represents the total length of the IPv4 packet.

This includes:

```text
IPv4 Header + Data
```

The minimum IPv4 packet size is:

```text
20 bytes
```

The maximum IPv4 packet size is:

```text
65,535 bytes
```

Therefore:

```text
Total Length = Header + Data
```

---

# 33. Identification Field

The IPv4 Identification field is:

```text
16 bits
```

It is used in fragmentation.

When an IPv4 packet is fragmented, fragments originating from the same original packet use the same Identification value.

This allows the receiving host to associate the fragments with the original packet.

---

# 34. Flags Field

The IPv4 Flags field is:

```text
3 bits
```

The flags are associated with fragmentation.

Important flags include:

- Reserved
- DF — Don't Fragment
- MF — More Fragments

## DF — Don't Fragment

The DF bit indicates that the packet should not be fragmented.

If fragmentation is required but DF is set, the packet cannot simply be fragmented.

## MF — More Fragments

The MF bit indicates whether more fragments follow.

For fragmented packets:

```text
MF = 1
```

means:

```text
More fragments follow.
```

For the final fragment:

```text
MF = 0
```

---

# 35. Fragment Offset

The Fragment Offset field is:

```text
13 bits
```

It identifies the position of a fragment within the original IPv4 packet.

The receiving device uses:

- Identification
- Fragment Offset
- MF flag

to help reconstruct the original packet.

The Fragment Offset is measured in:

```text
8-byte units
```

---

# 36. IPv4 Fragmentation

Fragmentation can occur when an IPv4 packet is larger than the maximum packet size supported by a network link.

The maximum frame payload supported by a link is related to its:

**MTU — Maximum Transmission Unit**

If an IPv4 packet is too large and fragmentation is permitted, it can be divided into smaller fragments.

Conceptually:

```text
Original IPv4 Packet
        |
        v
+-------+-------+-------+
| Frag1 | Frag2 | Frag3 |
+-------+-------+-------+
```

Each fragment contains its own IPv4 header.

The fragments can be identified using the Identification field.

Their position is determined using the Fragment Offset field.

The MF flag indicates whether additional fragments follow.

---

# 37. Time To Live — TTL

The Time To Live (TTL) field is:

```text
8 bits
```

TTL prevents packets from circulating around a network indefinitely.

Each router that forwards an IPv4 packet normally decrements the TTL value by:

```text
1
```

Example:

```text
TTL = 64
```

After one router:

```text
TTL = 63
```

After another router:

```text
TTL = 62
```

If TTL reaches zero, the packet is discarded.

This mechanism helps protect networks from routing loops.

---

# 38. Protocol Field

The IPv4 Protocol field identifies the upper-layer protocol carried inside the IPv4 packet.

The field is:

```text
8 bits
```

Examples include:

- TCP
- UDP
- ICMP

Conceptually:

```text
IPv4
 |
 +---- TCP
 |
 +---- UDP
 |
 +---- ICMP
```

This allows the receiving system to determine how the payload should be processed.

For example:

```text
IPv4 packet
    |
    | Protocol = TCP
    v
TCP segment
```

---

# 39. Header Checksum

The IPv4 Header Checksum field is used to detect errors in the IPv4 header.

It checks the IPv4 header rather than the complete packet payload.

Routers may recalculate the checksum because fields such as TTL change as the packet travels through the network.

For example:

```text
Router receives packet
        |
        v
TTL decreases
        |
        v
IPv4 header changes
        |
        v
Header checksum is recalculated
```

---

# 40. Source IPv4 Address

The Source Address field contains the IPv4 address of the device that originated the packet.

The field is:

```text
32 bits
```

Example:

```text
Source IP:
192.168.1.10
```

---

# 41. Destination IPv4 Address

The Destination Address field contains the IPv4 address of the intended destination.

The field is:

```text
32 bits
```

Example:

```text
Destination IP:
192.168.1.20
```

A router examines the destination IP address when making a Layer 3 forwarding decision.

---

# 42. Source and Destination Example

Suppose:

```text
PC1 = 192.168.1.10
PC2 = 192.168.2.20
```

PC1 sends a packet to PC2.

The IPv4 header contains:

```text
Source IP:
192.168.1.10

Destination IP:
192.168.2.20
```

The router examines:

```text
Destination IP = 192.168.2.20
```

and uses its routing table to determine where to forward the packet.

---

# 43. IPv4 Options

The IPv4 header can contain optional fields known as:

**Options**

Options are not present in the minimum IPv4 header.

Without options:

```text
IPv4 Header = 20 bytes
```

With options, the IPv4 header can become larger.

The maximum IPv4 header size is:

```text
60 bytes
```

---

# 44. Minimum and Maximum IPv4 Header Size

Minimum IPv4 header:

```text
20 bytes
```

Maximum IPv4 header:

```text
60 bytes
```

The difference is caused by the optional Options field.

Therefore:

```text
Minimum IHL = 5
Maximum IHL = 15
```

because each IHL unit represents:

```text
4 bytes
```

---

# 45. IPv4 Header Field Summary

| Field | Size | Purpose |
|---|---:|---|
| Version | 4 bits | Identifies IPv4 |
| IHL | 4 bits | IPv4 header length |
| DSCP | 6 bits | Traffic classification / QoS |
| ECN | 2 bits | Congestion notification |
| Total Length | 16 bits | Total packet size |
| Identification | 16 bits | Fragment identification |
| Flags | 3 bits | Fragmentation control |
| Fragment Offset | 13 bits | Fragment position |
| TTL | 8 bits | Limits packet lifetime |
| Protocol | 8 bits | Identifies upper-layer protocol |
| Header Checksum | 16 bits | Detects IPv4 header errors |
| Source Address | 32 bits | Sender IPv4 address |
| Destination Address | 32 bits | Destination IPv4 address |
| Options | Variable | Optional IPv4 header information |

---

# 46. IPv4 Packet and Encapsulation

IPv4 operates at:

**OSI Layer 3 — Network Layer**

A simplified encapsulation process is:

```text
Application Data
       |
       v
Transport Header + Data
       |
       v
IPv4 Header + Transport Segment
       |
       v
IPv4 Packet
```

The IPv4 packet is then encapsulated inside a Layer 2 frame before being transmitted across the local network.

Conceptually:

```text
+-------------------+
| Ethernet Header   |
+-------------------+
| IPv4 Header       |
+-------------------+
| TCP/UDP/ICMP      |
+-------------------+
| Application Data  |
+-------------------+
| Ethernet Trailer  |
+-------------------+
```

---

# 47. Wireshark Packet Capture

Wireshark can be used to inspect network packets.

It allows network engineers to examine protocol headers and packet contents.

For IPv4 traffic, useful fields to inspect include:

- Version
- Header Length
- DSCP
- ECN
- Total Length
- Identification
- Flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source Address
- Destination Address
- Options

Wireshark can therefore be used to connect theoretical IPv4 concepts with real packet captures.

For example, when analysing a ping:

```text
PC1
 |
 v
ICMP
 |
 v
IPv4
 |
 v
Ethernet
 |
 v
Network
```

The IPv4 header contains the source and destination IPv4 addresses, while the Protocol field identifies the payload as ICMP.

---

# 48. Important IPv4 Relationships

## IPv4 Address

```text
32 bits
```

## IPv4 Header

Minimum:

```text
20 bytes
```

Maximum:

```text
60 bytes
```

## IPv4 Total Length

Maximum:

```text
65,535 bytes
```

## TTL

```text
8 bits
```

## Source Address

```text
32 bits
```

## Destination Address

```text
32 bits
```

---

# 49. Important Cisco Commands

## Display interface information

```bash
show ip interface brief
```

## Enter configuration mode

```bash
configure terminal
```

## Enter an interface

```bash
interface GigabitEthernet0/0/0
```

## Configure an IPv4 address

```bash
ip address 192.168.100.1 255.255.255.0
```

## Enable the interface

```bash
no shutdown
```

## Verify interface configuration

```bash
show ip interface brief
```

---

# 50. IPv4 Troubleshooting Approach

When troubleshooting IPv4 connectivity, check the following.

## Step 1 — Check the host IP address

Verify:

- IP address
- Subnet mask
- Default gateway

## Step 2 — Check the physical connection

Make sure the interface/link is operational.

## Step 3 — Check the switch port

Verify that the switch port is connected and assigned to the correct VLAN.

## Step 4 — Check the router interface

Use:

```bash
show ip interface brief
```

Look for:

```text
up/up
```

## Step 5 — Test the local TCP/IP stack

Use:

```bash
ping 127.0.0.1
```

## Step 6 — Test the default gateway

Example:

```bash
ping 192.168.1.1
```

## Step 7 — Test the remote host

Example:

```bash
ping 192.168.2.20
```

This provides a structured way to identify where connectivity is failing.

---

# 51. Key Calculations to Remember

## Number of usable hosts

```text
2^n - 2
```

where:

```text
n = number of host bits
```

## Host bits

```text
Host bits = 32 - Prefix Length
```

Example:

```text
/24

32 - 24 = 8 host bits
```

## Usable hosts for /24

```text
2^8 - 2
= 254
```

## Usable hosts for /16

```text
2^16 - 2
= 65,534
```

## Usable hosts for /8

```text
2^24 - 2
= 16,777,214
```

---

# 52. Quick IPv4 Addressing Reference

| Prefix | Host Bits | Usable Hosts |
|---|---:|---:|
| `/8` | 24 | 16,777,214 |
| `/16` | 16 | 65,534 |
| `/24` | 8 | 254 |

---

# 53. Quick Address Calculation Examples

## Example 1

```text
43.109.23.12/8
```

Network ID:

```text
43.0.0.0
```

Broadcast:

```text
43.255.255.255
```

First Host:

```text
43.0.0.1
```

Last Host:

```text
43.255.255.254
```

Usable Hosts:

```text
16,777,214
```

---

## Example 2

```text
129.221.23.13/16
```

Network ID:

```text
129.221.0.0
```

Broadcast:

```text
129.221.255.255
```

First Host:

```text
129.221.0.1
```

Last Host:

```text
129.221.255.254
```

Usable Hosts:

```text
65,534
```

---

## Example 3

```text
209.211.3.0/24
```

Network ID:

```text
209.211.3.0
```

Broadcast:

```text
209.211.3.255
```

First Host:

```text
209.211.3.1
```

Last Host:

```text
209.211.3.254
```

Usable Hosts:

```text
254
```

---

# 54. IPv4 Troubleshooting Mindset

When working with IPv4, I need to distinguish between:

- Host address
- Network address
- Broadcast address

I also need to understand:

- Prefix length
- Subnet mask
- Network bits
- Host bits
- Usable host range

For routing, I need to understand that routers make forwarding decisions using:

```text
Destination IPv4 Address
```

and their:

```text
Routing Table
```

---

# 55. IPv4 Header — Key Points

The IPv4 header provides information required for packet delivery and processing.

The most important fields to remember are:

- Version
- IHL
- Total Length
- Identification
- Flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source IP
- Destination IP

A useful way to remember the purpose of some fields is:

```text
Version
    ↓
Which IP version?

IHL
    ↓
How long is the header?

Total Length
    ↓
How large is the packet?

Identification
    ↓
Which fragments belong together?

Flags
    ↓
How should fragmentation be handled?

Fragment Offset
    ↓
Where does this fragment belong?

TTL
    ↓
How long can the packet remain in the network?

Protocol
    ↓
What upper-layer protocol is carried?

Checksum
    ↓
Is the IPv4 header valid?

Source IP
    ↓
Who sent the packet?

Destination IP
    ↓
Where is the packet going?
```

---

# 56. Practice Quiz

## Question 1

Which bit will be set to `1` on all IPv4 packet fragments except the last fragment?

### Answer

**MF — More Fragments**

The MF flag indicates that additional fragments follow.

Therefore:

```text
MF = 1
```

means:

```text
More fragments follow.
```

For the final fragment:

```text
MF = 0
```

---

# 57. Final IPv4 Study Summary

IPv4 is a **32-bit Layer 3 addressing and packet delivery protocol**.

An IPv4 address consists of:

```text
32 bits
```

and is normally written as:

```text
x.x.x.x
```

IPv4 addressing requires understanding:

- Network Portion
- Host Portion
- Prefix Length
- Subnet Mask
- Network Address
- Broadcast Address
- Usable Host Range

Traditional IPv4 classes are:

- Class A
- Class B
- Class C
- Class D
- Class E

The usable host formula is:

```text
2^n - 2
```

where `n` is the number of host bits.

The IPv4 header contains important information such as:

- Version
- IHL
- DSCP
- ECN
- Total Length
- Identification
- Flags
- Fragment Offset
- TTL
- Protocol
- Header Checksum
- Source Address
- Destination Address
- Options

IPv4 fragmentation is controlled using:

```text
Identification
Flags
Fragment Offset
```

TTL prevents packets from circulating indefinitely through routing loops.

The Protocol field identifies the upper-layer protocol, such as:

```text
TCP
UDP
ICMP
```

Routers use the **destination IPv4 address** to make Layer 3 forwarding decisions.

---

# 58. Key Takeaways

The main concepts I learned from this IPv4 study are:

- IPv4 addresses are 32 bits.
- IPv4 addresses contain four 8-bit octets.
- Binary uses base 2.
- Decimal uses base 10.
- Hexadecimal uses base 16.
- IPv4 uses network and host portions.
- CIDR prefixes identify the number of network bits.
- `/24` provides 8 host bits and 254 usable hosts.
- `/16` provides 16 host bits and 65,534 usable hosts.
- `/8` provides 24 host bits and 16,777,214 usable hosts.
- Network addresses identify networks.
- Broadcast addresses communicate with all hosts in a subnet.
- `127.0.0.1` is the commonly used IPv4 loopback address.
- Routers operate primarily at OSI Layer 3.
- Routers use destination IPv4 addresses when making forwarding decisions.
- The minimum IPv4 header is 20 bytes.
- The maximum IPv4 header is 60 bytes.
- TTL limits how long an IPv4 packet can remain in the network.
- The Protocol field identifies the upper-layer protocol.
- IPv4 fragmentation uses Identification, Flags and Fragment Offset.
- The MF flag indicates that more fragments follow.
- The IPv4 Header Checksum protects the IPv4 header.
- Wireshark can be used to inspect IPv4 headers in real packet captures.

---

# IPv4 Learning Progress

Topics studied:

- [x] Introduction to routing
- [x] IPv4 addressing
- [x] Decimal numbers
- [x] Hexadecimal numbers
- [x] Binary numbers
- [x] Binary-to-decimal conversion
- [x] Decimal-to-binary conversion
- [x] IPv4 address structure
- [x] CIDR prefix length
- [x] Loopback addresses
- [x] Network addresses
- [x] Broadcast addresses
- [x] Host calculations
- [x] IPv4 address classes
- [x] Cisco interface commands
- [x] IPv4 packet structure
- [x] IPv4 header
- [x] IPv4 header fields
- [x] IPv4 fragmentation
- [x] TTL
- [x] Protocol field
- [x] Header checksum
- [x] Source and destination IP addresses
- [x] IPv4 options
- [x] Wireshark packet capture
- [x] IPv4 troubleshooting
- [x] IPv4 practice questions

---

## Study Focus

This study helped build a practical understanding of how IPv4 addressing works at **OSI Layer 3**, how routers use destination IP addresses for forwarding decisions, and how IPv4 packet headers carry the information required for delivery.

The combination of **binary calculations, IPv4 addressing, Cisco configuration, packet structure, fragmentation, and Wireshark analysis** provides a foundation for further study of:

- Subnetting
- VLSM
- Routing protocols
- ACLs
- NAT
- IPv6
- Network troubleshooting
- Network security
