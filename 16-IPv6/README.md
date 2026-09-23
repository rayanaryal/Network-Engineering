# IPv6

This section documents my understanding and hands-on study of **IPv6**, including IPv6 addressing, address representation, address types, IPv6 headers, Neighbor Discovery Protocol (NDP), SLAAC, Duplicate Address Detection (DAD), and IPv6 static routing.

These notes are based on my CCNA study material and practical Cisco networking learning.

---

# Table of Contents

1. [Exam Topics](#1-exam-topics)
2. [IPv6 Overview](#2-ipv6-overview)
3. [Hexadecimal](#3-hexadecimal)
4. [Binary to Hexadecimal](#4-binary-to-hexadecimal)
5. [Hexadecimal to Binary](#5-hexadecimal-to-binary)
6. [Why IPv6](#6-why-ipv6)
7. [IPv6 Address Representation](#7-ipv6-address-representation)
8. [Shortening IPv6 Addresses](#8-shortening-ipv6-addresses)
9. [Expanding IPv6 Addresses](#9-expanding-ipv6-addresses)
10. [IPv6 Prefixes](#10-ipv6-prefixes)
11. [Configuring IPv6 on a Cisco Router](#11-configuring-ipv6-on-a-cisco-router)
12. [Modified EUI-64](#12-modified-eui-64)
13. [Why a 64-bit Interface Identifier](#13-why-a-64-bit-interface-identifier)
14. [What EUI-64 Solves](#14-what-eui-64-solves)
15. [EUI-64 Conversion](#15-eui-64-conversion)
16. [Why Invert the 7th Bit](#16-why-invert-the-7th-bit)
17. [IPv6 Address Types](#17-ipv6-address-types)
18. [Global Unicast Addresses](#18-global-unicast-addresses)
19. [Unique Local Addresses](#19-unique-local-addresses)
20. [Link-Local Addresses](#20-link-local-addresses)
21. [Multicast Addresses](#21-multicast-addresses)
22. [Multicast Address Scopes](#22-multicast-address-scopes)
23. [IPv6 Multicast Groups](#23-ipv6-multicast-groups)
24. [Anycast Addresses](#24-anycast-addresses)
25. [Other IPv6 Addresses](#25-other-ipv6-addresses)
26. [IPv6 Header vs IPv4 Header](#26-ipv6-header-vs-ipv4-header)
27. [IPv6 Header Fields](#27-ipv6-header-fields)
28. [Version](#28-version)
29. [Traffic Class](#29-traffic-class)
30. [Flow Label](#30-flow-label)
31. [Payload Length](#31-payload-length)
32. [Next Header](#32-next-header)
33. [Hop Limit](#33-hop-limit)
34. [Source and Destination Addresses](#34-source-and-destination-addresses)
35. [Solicited-Node Multicast Address](#35-solicited-node-multicast-address)
36. [Solicited-Node Multicast Address CLI](#36-solicited-node-multicast-address-cli)
37. [Neighbor Discovery Protocol](#37-neighbor-discovery-protocol)
38. [Neighbor Solicitation](#38-neighbor-solicitation)
39. [Neighbor Advertisement](#39-neighbor-advertisement)
40. [IPv6 Neighbor Table](#40-ipv6-neighbor-table)
41. [SLAAC](#41-slaac)
42. [Duplicate Address Detection](#42-duplicate-address-detection)
43. [IPv6 Static Routing](#43-ipv6-static-routing)
44. [Link-Local Next-Hops](#44-link-local-next-hops)
45. [IPv6 Revision and Quiz](#45-ipv6-revision-and-quiz)
46. [Final IPv6 Cheat Sheet](#46-final-ipv6-cheat-sheet)

---

# 1. Exam Topics

The main IPv6 topics required for CCNA preparation include:

- IPv6 addressing
- IPv6 address representation
- IPv6 prefixes
- IPv6 address types
- IPv6 configuration
- Modified EUI-64
- Global Unicast Addresses
- Unique Local Addresses
- Link-Local Addresses
- Multicast
- Anycast
- IPv6 headers
- Neighbor Discovery Protocol
- Neighbor Solicitation
- Neighbor Advertisement
- IPv6 Neighbor Table
- SLAAC
- Duplicate Address Detection
- IPv6 static routing
- Link-local next-hops

The overall IPv6 study path can be represented as:

```text
IPv6
 |
 +-- Addressing
 |    |
 |    +-- Representation
 |    +-- Shortening
 |    +-- Expansion
 |    +-- Prefixes
 |
 +-- Address Generation
 |    |
 |    +-- Manual
 |    +-- EUI-64
 |    +-- SLAAC
 |
 +-- Address Types
 |    |
 |    +-- Global Unicast
 |    +-- Unique Local
 |    +-- Link-Local
 |    +-- Multicast
 |    +-- Anycast
 |    +-- Special Addresses
 |
 +-- IPv6 Header
 |    |
 |    +-- Version
 |    +-- Traffic Class
 |    +-- Flow Label
 |    +-- Payload Length
 |    +-- Next Header
 |    +-- Hop Limit
 |    +-- Source
 |    +-- Destination
 |
 +-- Neighbor Discovery
 |    |
 |    +-- NDP
 |    +-- NS
 |    +-- NA
 |    +-- Neighbor Table
 |    +-- SLAAC
 |    +-- DAD
 |
 +-- Routing
      |
      +-- Static Routes
      +-- Link-Local Next-Hops
```

---

# 2. IPv6 Overview

IPv6 was developed as the successor to IPv4.

The biggest difference in addressing is:

```text
IPv4 = 32 bits
IPv6 = 128 bits
```

IPv6 uses hexadecimal notation.

A complete IPv6 address contains:

```text
8 hextets
```

Each hextet contains:

```text
4 hexadecimal digits
```

Each hextet therefore represents:

```text
16 bits
```

So:

```text
8 × 16 = 128 bits
```

Example:

```text
2001:0DB8:5917:EABD:6562:17EA:C92D:59BD
```

---

# 3. Hexadecimal

IPv6 uses:

```text
Base 16
```

Hexadecimal uses:

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

The letters represent:

```text
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

---

## Number Systems

### Binary

```text
Base 2

0
1
```

Example:

```text
Binary 10 = Decimal 2
```

### Decimal

```text
Base 10

0 1 2 3 4 5 6 7 8 9
```

### Hexadecimal

```text
Base 16

0 1 2 3 4 5 6 7 8 9 A B C D E F
```

Example:

```text
Hexadecimal 10 = Decimal 16
```

---

# 4. Binary to Hexadecimal

Every hexadecimal digit represents exactly:

```text
4 binary bits
```

Therefore, to convert binary to hexadecimal:

```text
1. Divide the binary number into groups of 4 bits.
2. Convert each group to hexadecimal.
3. Combine the hexadecimal digits.
```

---

## Example

Convert:

```text
11011011
```

to hexadecimal.

Split into groups of four:

```text
1101 1011
```

Convert:

```text
1101 = D
1011 = B
```

Therefore:

```text
11011011 = DB
```

---

## Binary to Hexadecimal Table

```text
Binary   Decimal   Hex

0000       0        0
0001       1        1
0010       2        2
0011       3        3
0100       4        4
0101       5        5
0110       6        6
0111       7        7
1000       8        8
1001       9        9
1010      10        A
1011      11        B
1100      12        C
1101      13        D
1110      14        E
1111      15        F
```

---

# 5. Hexadecimal to Binary

To convert hexadecimal to binary:

```text
1. Separate each hexadecimal digit.
2. Convert each digit to 4 binary bits.
3. Combine the groups.
```

Example:

```text
EC
```

Convert:

```text
E = 1110
C = 1100
```

Therefore:

```text
EC = 11101100
```

---

## Another Example

```text
D7
```

Convert:

```text
D = 1101
7 = 0111
```

Therefore:

```text
D7 = 11010111
```

---

# 6. Why IPv6

The primary reason for IPv6 is the limitation of IPv4 address space.

IPv4 uses:

```text
32 bits
```

which provides:

```text
2^32
```

possible addresses.

That is approximately:

```text
4.29 billion addresses
```

As the Internet grew, IPv4 address space became insufficient.

Several techniques helped conserve IPv4 addresses:

```text
Private IPv4 addresses
NAT
VLSM
```

However, IPv6 provides a much larger address space.

IPv6 uses:

```text
128 bits
```

and provides:

```text
2^128
```

possible addresses.

---

## IPv4 vs IPv6

```text
IPv4
32 bits
        ↓
Limited address space

IPv6
128 bits
        ↓
Massive address space
```

---

# 7. IPv6 Address Representation

A full IPv6 address consists of:

```text
8 hextets
```

separated by colons.

Example:

```text
2001:0DB8:5917:EABD:6562:17EA:C92D:59BD
```

Each hextet contains:

```text
4 hexadecimal digits
```

Example:

```text
2001
0DB8
5917
EABD
6562
17EA
C92D
59BD
```

Each hextet represents:

```text
16 bits
```

Therefore:

```text
8 × 16 = 128 bits
```

---

## Typical `/64` Structure

A `/64` IPv6 network commonly consists of:

```text
64-bit Prefix
+
64-bit Interface Identifier
```

Example:

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

Conceptually:

```text
2001:DB8:8B00:0001 | 0000:0000:0000:0001
       64 bits       |       64 bits
          Prefix     | Interface Identifier
```

---

# 8. Shortening IPv6 Addresses

IPv6 addresses can be shortened using two main rules.

---

## Rule 1 — Remove Leading Zeros

Leading zeros in a hextet can be removed.

Example:

```text
0001 → 1
0DB8 → DB8
0020 → 20
0080 → 80
```

Example:

```text
2001:0DB8:0000:0000:20A1:0020:0080:34BD
```

becomes:

```text
2001:DB8:0:0:20A1:20:80:34BD
```

---

## Rule 2 — Replace Consecutive Zero Hextets with `::`

Example:

```text
2001:DB8:0:0:0:0:80:34BD
```

can become:

```text
2001:DB8::80:34BD
```

Important:

```text
:: can only be used once.
```

---

## IPv6 Shortening Examples

```text
2000:AB78:20:1BF:ED89::1
```

```text
FE80::2:0:0:FBE8
```

```text
AE89:2100:1AC:F0::20F
```

```text
2001:DB8:8B00:1000:2:BC0:D07:99
```

```text
2001:DB8::1000
```

---

# 9. Expanding IPv6 Addresses

When expanding an IPv6 address:

```text
1. Add leading zeros.
2. Expand ::
3. Make exactly 8 hextets.
4. Make every hextet exactly 4 hexadecimal digits.
```

---

## Example

Shortened:

```text
2001:DB8::1
```

Expanded:

```text
2001:0DB8:0000:0000:0000:0000:0000:0001
```

---

## Examples from the Notes

```text
FE80:0000:0000:0000:1010:02FC:0000:0009
```

```text
2001:0DB8:0001:0B23:2309:0000:0000:00C1
```

```text
FD00:0000:0000:0000:1000:0689:9000:0CDF
```

```text
FF02:0000:0000:0000:0000:0000:0000:0002
```

```text
0000:0000:0000:0000:0000:0000:0000:0001
```

---

## Example — `::1`

```text
::1
```

expands to:

```text
0000:0000:0000:0000:0000:0000:0000:0001
```

---

# 10. IPv6 Prefixes

The IPv6 prefix identifies the network portion of an IPv6 address.

Common prefix lengths include:

```text
/48
/56
/64
```

A common IPv6 LAN uses:

```text
/64
```

---

## Example

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

The first 64 bits are the prefix:

```text
2001:DB8:8B00:0001::/64
```

---

## `/48` Allocation

An organisation may receive:

```text
2001:DB8:8B00::/48
```

and create multiple `/64` subnets:

```text
2001:DB8:8B00:0001::/64
2001:DB8:8B00:0002::/64
2001:DB8:8B00:0003::/64
2001:DB8:8B00:0004::/64
```

---

## Different Prefix Lengths

The notes include examples such as:

```text
FE80::/9

2001:0DB8:1:B23::/64

2001:DB8:BAD:CAFE:1200::/71

2001:DB8:0:FEEC::0/62

2001:DB8:9BAD:BABE::00/63
```

When the prefix length does not fall exactly on a hextet boundary, count the required number of bits carefully.

---

# 11. Configuring IPv6 on a Cisco Router

First enable IPv6 routing globally:

```text
R1(config)# ipv6 unicast-routing
```

Then configure an IPv6 address on an interface:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1:1::1/64
R1(config-if)# no shutdown
```

---

## Example

```text
R1(config)# ipv6 unicast-routing

R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:0:1::1/64
R1(config-if)# no shutdown
```

Another interface:

```text
R1(config)# interface g0/1
R1(config-if)# ipv6 address 2001:db8:0:2::1/64
R1(config-if)# no shutdown
```

---

## Verify

```text
show ipv6 interface
```

```text
show ipv6 interface brief
```

```text
show ipv6 route
```

---

# 12. Modified EUI-64

Modified EUI-64 is a method for generating a:

```text
64-bit Interface Identifier
```

from a:

```text
48-bit MAC address
```

The basic process is:

```text
48-bit MAC
     |
     ↓
Split MAC
     |
     ↓
Insert FFFE
     |
     ↓
Invert U/L bit
     |
     ↓
64-bit Interface Identifier
```

---

# 13. Why a 64-bit Interface Identifier

IPv6 commonly uses a 64-bit Interface Identifier in a `/64` subnet.

However, Ethernet MAC addresses are:

```text
48 bits
```

Therefore, a standard method is required to convert:

```text
48-bit MAC
        ↓
64-bit IID
```

That standard is:

```text
EUI-64
```

---

# 14. What EUI-64 Solves

One important use of EUI-64 is automatic address generation.

The notes connect this with:

```text
SLAAC
```

Stateless Address Autoconfiguration allows a device to automatically generate an IPv6 address without requiring manual configuration of the complete address.

Example:

```text
Prefix:

2001:db8:abcd:1234::/64
```

MAC:

```text
78:2B:CB:AC:08:67
```

Modified EUI-64:

```text
7A2B:CBFF:FEAC:0867
```

IPv6 address:

```text
2001:db8:abcd:1234:7A2B:CBFF:FEAC:0867
```

Conceptually:

```text
IPv6 Prefix
     +
MAC Address
     |
     ↓
Modified EUI-64
     |
     ↓
IPv6 Interface Identifier
     |
     ↓
IPv6 Address
```

---

# 15. EUI-64 Conversion

The three main steps are:

```text
1. Split the MAC address in half.
2. Insert FFFE.
3. Invert the U/L bit.
```

---

## Example

MAC:

```text
78:2B:CB:AC:08:67
```

Split:

```text
78:2B:CB | AC:08:67
```

Insert:

```text
FFFE
```

Result:

```text
78:2B:CB:FF:FE:AC:08:67
```

Invert the U/L bit:

```text
78 → 7A
```

Final Interface Identifier:

```text
7A2B:CBFF:FEAC:0867
```

---

## Other EUI-64 Examples from the Notes

```text
782B CB FF | FEAC 0867
        ↓
7A2B:CBFF:FEAC:0867
```

```text
0200 4C FF | FE 4F 4F50
```

```text
0050 56FF FEC0 0001
```

```text
00FF 6BFF FEA6 F456
```

```text
90AB FF6D FE6B 98AE
```

---

# 16. Why Invert the 7th Bit

The first byte of a MAC address contains the:

```text
U/L bit
```

The U/L bit indicates whether the address is:

```text
Universal
```

or:

```text
Locally administered
```

During Modified EUI-64 conversion, the U/L bit is inverted.

---

## Example

Suppose the first byte is:

```text
78
```

In binary:

```text
01111000
```

The relevant U/L bit is inverted.

The result becomes:

```text
7A
```

Therefore:

```text
78 → 7A
```

This bit inversion is an important part of Modified EUI-64.

---

# 17. IPv6 Address Types

The major IPv6 address types include:

```text
Unicast
Multicast
Anycast
```

Important unicast/special addresses include:

```text
Global Unicast
Unique Local
Link-Local
Loopback
Unspecified
```

---

# 18. Global Unicast Addresses

Global Unicast addresses are globally routable IPv6 addresses.

The range covered in these notes is:

```text
2000::/3
```

This covers addresses beginning from:

```text
2000::
```

through:

```text
3FFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF
```

Global Unicast addresses can be routed across the Internet.

---

## Typical Structure

A typical Global Unicast address can be viewed as:

```text
Global Routing Prefix
        +
Subnet ID
        +
Interface Identifier
```

Example:

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

Conceptually:

```text
2001:DB8:8B00 | 0001 | 0000:0000:0000:0001
 Global Prefix   Subnet      Interface ID
```

---

# 19. Unique Local Addresses

Unique Local Addresses are used for internal/private IPv6 networks.

The range is:

```text
FC00::/7
```

In practice, Unique Local Addresses commonly begin with:

```text
FD
```

They are not intended to be routed across the public Internet.

---

## Example

```text
FD00:1234:5678:1::1/64
```

These addresses can be freely used inside internal networks without public Internet registration.

---

# 20. Link-Local Addresses

Link-local addresses are used for communication on the local link.

The range is:

```text
FE80::/10
```

They are not routed across different IPv6 networks.

---

## Automatically Generated

A link-local address can automatically be configured when IPv6 is enabled on an interface.

For example:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 enable
```

The router automatically generates a link-local address.

---

## Link-Local Example

```text
FE80::EF8:22FF:FE56:A600
```

---

## Link-Local Uses

Link-local addresses are important for:

- Neighbor Discovery Protocol
- SLAAC
- Router Discovery
- Routing protocol neighbour relationships
- Link-local next-hops

---

## Link-Local vs Global Unicast

```text
Link-Local:

FE80::/10
     ↓
Local network only
     ↓
Not routed over Internet
```

```text
Global Unicast:

2000::/3
     ↓
Globally routable
     ↓
Can be used across the Internet
```

---

# 21. Multicast Addresses

IPv6 does not use broadcast.

Instead, IPv6 uses multicast for one-to-many communication.

IPv6 multicast addresses begin with:

```text
FF
```

The multicast range is:

```text
FF00::/8
```

---

## Communication Types

### Unicast

```text
One → One
```

### Multicast

```text
One → Many
```

### Broadcast

```text
One → All
```

IPv6:

```text
No Broadcast
```

Instead:

```text
Multicast
```

is used for many one-to-many functions.

---

# 22. Multicast Address Scopes

Important IPv6 multicast scopes include:

```text
FF01 → Interface-local
FF02 → Link-local
FF05 → Site-local
FF08 → Organization-local
FF0E → Global
```

---

## Interface-Local

```text
FF01
```

The traffic remains within the local device.

---

## Link-Local

```text
FF02
```

The multicast traffic stays on the local link.

Routers do not forward it to another link.

---

## Site-Local

```text
FF05
```

The traffic can be forwarded within a site.

---

## Organization-Local

```text
FF08
```

The scope can cover an organisation.

---

## Global

```text
FF0E
```

Global multicast scope can be routed globally.

---

# 23. IPv6 Multicast Groups

IPv6 devices can join multicast groups.

For example:

```text
All Nodes
FF02::1
```

and:

```text
All Routers
FF02::2
```

The notes show routers joining these multicast groups by default.

Conceptually:

```text
                 Multicast Group
                       |
          +------------+------------+
          |            |            |
         R1           R2           R3
          \            |           /
           \           |          /
             Members of Group
```

---

## All Nodes

```text
FF02::1
```

Represents all IPv6 nodes on the local link.

---

## All Routers

```text
FF02::2
```

Represents all IPv6 routers on the local link.

---

# 24. Anycast Addresses

Anycast is:

```text
One-to-one-of-many
```

Multiple devices can use the same IPv6 address.

Routing determines which destination is reached.

Example:

```text
                  R1
                 /
                /
Host -------- Destination
                \
                 \
                  R2
```

R1 and R2 can advertise the same anycast address.

The routing table determines which router is the appropriate destination.

---

## Important Anycast Point

IPv6 does not have a dedicated address range for Anycast.

A normal unicast address can be configured as an anycast address.

---

# 25. Other IPv6 Addresses

## Unspecified Address

```text
::
```

Full form:

```text
0:0:0:0:0:0:0:0
```

Prefix:

```text
::/128
```

It represents an unspecified IPv6 address.

---

## Loopback Address

```text
::1
```

Prefix:

```text
::1/128
```

It is used to test the local IPv6 protocol stack.

IPv4 equivalent:

```text
127.0.0.1
```

---

## IPv6 Default Route

```text
::/0
```

This represents all IPv6 destinations when a more-specific route is not available.

---

# 26. IPv6 Header vs IPv4 Header

IPv6 has a redesigned base header compared with IPv4.

The IPv6 base header has a fixed size of:

```text
40 bytes
```

The IPv4 header can vary in size because IPv4 includes optional header fields.

---

## Important IPv6 Header Fields

The IPv6 base header contains:

```text
Version
Traffic Class
Flow Label
Payload Length
Next Header
Hop Limit
Source Address
Destination Address
```

Conceptually:

```text
+-------------------------------+
| Version | Traffic Class       |
+-------------------------------+
|          Flow Label           |
+-------------------------------+
|       Payload Length          |
+-------------------------------+
| Next Header | Hop Limit      |
+-------------------------------+
|                               |
|       Source Address          |
|          128 bits             |
|                               |
+-------------------------------+
|                               |
|     Destination Address       |
|          128 bits             |
|                               |
+-------------------------------+
```

---

# 27. IPv6 Header Fields

The IPv6 header contains several important fields that identify how the packet should be processed.

```text
IPv6 Header
 |
 +-- Version
 +-- Traffic Class
 +-- Flow Label
 +-- Payload Length
 +-- Next Header
 +-- Hop Limit
 +-- Source Address
 +-- Destination Address
```

---

# 28. Version

The Version field is:

```text
4 bits
```

For IPv6, the value is:

```text
0110
```

which represents:

```text
6
```

Therefore:

```text
IPv6 Version = 6
```

IPv4 uses:

```text
0100
```

which represents:

```text
4
```

---

# 29. Traffic Class

The Traffic Class field is:

```text
8 bits
```

It is used for traffic classification and Quality of Service (QoS).

It can help routers identify and treat traffic differently according to its requirements.

Conceptually:

```text
Traffic Class
      |
      +-- Traffic classification
      |
      +-- QoS treatment
```

---

# 30. Flow Label

The Flow Label field is:

```text
20 bits
```

It can be used to identify packets belonging to the same traffic flow.

This allows network devices to recognise related packets and apply consistent handling.

Conceptually:

```text
Flow
 |
 +-- Packet 1
 +-- Packet 2
 +-- Packet 3
 +-- Packet 4
```

The Flow Label can identify the packets as belonging to the same flow.

---

# 31. Payload Length

The Payload Length field is:

```text
16 bits
```

It indicates the length of the IPv6 payload.

The payload includes information following the fixed IPv6 base header.

The IPv6 base header itself is:

```text
40 bytes
```

---

# 32. Next Header

The Next Header field is:

```text
8 bits
```

It identifies what comes after the IPv6 base header.

It can identify:

```text
Transport-layer protocol
```

such as:

```text
TCP
UDP
```

or an IPv6 extension header.

Conceptually:

```text
IPv6 Header
     |
     ↓
Next Header
     |
     +-- TCP
     |
     +-- UDP
     |
     +-- Extension Header
```

This field replaces the role of the IPv4 Protocol field and also supports IPv6 extension headers.

---

# 33. Hop Limit

The Hop Limit field is:

```text
8 bits
```

It prevents IPv6 packets from circulating indefinitely.

Each router that forwards the packet decreases the Hop Limit by:

```text
1
```

When the Hop Limit reaches:

```text
0
```

the packet is discarded.

This is similar to the IPv4:

```text
TTL — Time To Live
```

field.

---

## Example

Suppose:

```text
Hop Limit = 64
```

After one router:

```text
64 → 63
```

After another router:

```text
63 → 62
```

and so on.

---

# 34. Source and Destination Addresses

IPv6 uses:

```text
128-bit Source Address
```

and:

```text
128-bit Destination Address
```

These are the largest fields in the IPv6 base header.

Example:

```text
Source:

2001:DB8:1::10
```

Destination:

```text
2001:DB8:2::20
```

The source identifies the sender.

The destination identifies the intended receiver.

---

# 35. Solicited-Node Multicast Address

Solicited-node multicast addresses are an important part of IPv6 Neighbor Discovery.

They are used by:

```text
NDP
```

for functions such as address resolution.

The standard solicited-node multicast prefix is:

```text
FF02::1:FF00:0/104
```

Every IPv6 unicast address automatically maps to a solicited-node multicast address.

The last:

```text
24 bits
```

of the IPv6 unicast address are appended to the solicited-node multicast prefix.

---

## Example

Suppose the IPv6 address ends with:

```text
...:36:8500
```

The corresponding solicited-node multicast address can be:

```text
FF02::1:FF36:8500
```

Conceptually:

```text
Solicited-Node Prefix
        +
Last 24 bits of IPv6 address
        |
        ↓
Solicited-Node Multicast Address
```

---

# 36. Solicited-Node Multicast Address CLI

The notes show examples such as:

```text
FF02::1:FF36:8500
```

This is a solicited-node multicast address.

The base prefix is:

```text
FF02::1:FF00:0/104
```

The final 24 bits are taken from the corresponding IPv6 unicast address.

---

## Why Is This Useful?

Instead of sending a broadcast to every device, IPv6 can send the Neighbor Solicitation to the specific multicast group associated with the target IPv6 address.

This is more efficient than IPv4 ARP broadcast behaviour.

---

# 37. Neighbor Discovery Protocol

Neighbor Discovery Protocol is:

```text
NDP
```

It is a major IPv6 protocol used for discovering and communicating with neighbouring devices.

NDP replaces several functions that were traditionally performed by IPv4 ARP.

Important NDP messages include:

```text
Neighbor Solicitation (NS)
Neighbor Advertisement (NA)
Router Solicitation (RS)
Router Advertisement (RA)
```

---

## NDP Functions

NDP supports functions such as:

```text
Neighbor discovery
Address resolution
Router discovery
SLAAC
Duplicate Address Detection
```

---

## NDP and ARP

IPv4:

```text
ARP Request
      ↓
Broadcast
```

IPv6:

```text
Neighbor Solicitation
      ↓
Multicast
```

Therefore, IPv6 does not use ARP.

---

# 38. Neighbor Solicitation

Neighbor Solicitation is:

```text
NS
```

It is used by IPv6 devices to discover information about neighbouring devices.

One important use is discovering the link-layer/MAC address associated with an IPv6 address.

---

## IPv4 Comparison

IPv4 uses:

```text
ARP Request
```

which is broadcast.

IPv6 uses:

```text
Neighbor Solicitation
```

which is multicast.

Conceptually:

```text
IPv4:

Host
 |
 | ARP Broadcast
 +--------------------> Network
                         |
                         +-- All devices receive it


IPv6:

Host
 |
 | Neighbor Solicitation
 | Multicast
 ↓
Solicited-Node Group
 |
 +-- Relevant device
```

The multicast approach is more targeted than a broadcast.

---

# 39. Neighbor Advertisement

Neighbor Advertisement is:

```text
NA
```

It is used to provide information about a neighbour.

It is commonly compared with the:

```text
ARP Reply
```

in IPv4.

Conceptually:

```text
R1
 |
 | Neighbor Solicitation
 ↓
R2
 |
 | Neighbor Advertisement
 ↓
R1
```

The Neighbor Advertisement provides the information needed by R1 to communicate with R2 at Layer 2.

---

## Simple Comparison

```text
IPv4

ARP Request
     ↓
ARP Reply


IPv6

Neighbor Solicitation
     ↓
Neighbor Advertisement
```

---

# 40. IPv6 Neighbor Table

IPv6 does not use an ARP table.

Instead, IPv6 devices maintain an:

```text
IPv6 Neighbor Table
```

The table contains information about neighbouring IPv6 devices.

Conceptually:

```text
IPv6 Device
     |
     ↓
Neighbor Table
     |
     +-- IPv6 Address
     +-- Link-layer information
     +-- Neighbor state
```

All IPv6 devices use NDP and maintain neighbour information.

---

# 41. SLAAC

SLAAC stands for:

> **Stateless Address Autoconfiguration**

SLAAC allows an IPv6 host to automatically configure an IPv6 address.

A major part of SLAAC is:

```text
Router Advertisement
```

The router provides information about the IPv6 network prefix.

The host can then generate its own address.

---

## Router Discovery

IPv6 uses:

```text
Router Solicitation (RS)
```

and:

```text
Router Advertisement (RA)
```

messages.

Conceptually:

```text
Host
 |
 | Router Solicitation
 ↓
Router
 |
 | Router Advertisement
 ↓
Host
 |
 +-- Learns IPv6 network information
 |
 +-- Configures IPv6 address
```

---

## SLAAC Process

A simplified process is:

```text
1. Host joins the IPv6 network.
2. Host uses NDP.
3. Host discovers router information.
4. Router sends Router Advertisement.
5. Host learns the IPv6 prefix.
6. Host generates an Interface Identifier.
7. Host creates an IPv6 address.
8. Host performs Duplicate Address Detection.
```

---

## Link-Local and Global Address Example

The notes show:

```text
FE80::EF8:22FF:FE56:A600
```

and:

```text
2001:DB8::EF8:22FF:FE56:A600
```

The first is a:

```text
Link-Local address
```

while the second is a:

```text
Global Unicast address
```

---

## Link-Local vs Global Unicast

| Feature | Link-Local | Global Unicast |
|---|---|---|
| Example | `FE80::...` | `2001:DB8::...` |
| Scope | Local link | Global |
| Internet routable | No | Yes |
| NDP | Yes | Yes |
| SLAAC | Used | Can be generated |
| Router discovery | Yes | Yes |

---

# 42. Duplicate Address Detection

Duplicate Address Detection is:

```text
DAD
```

It is used to check whether an IPv6 address is already in use before a device begins using it.

---

## DAD Process

A device sends a:

```text
Neighbor Solicitation
```

to the solicited-node multicast address associated with the IPv6 address it wants to use.

Conceptually:

```text
Host wants:

2001:DB8::10

        |
        ↓
Calculate solicited-node multicast address
        |
        ↓
Send Neighbor Solicitation
        |
        ↓
Does another device respond?
       / \
     Yes  No
      |    |
      |    +-- Address appears unique
      |
      +-- Duplicate detected
```

If no response is received, the host assumes the address is unique and can use it.

---

# 43. IPv6 Static Routing

IPv6 supports static routes.

Static routes can be configured manually by a network administrator.

The basic Cisco IOS command is:

```text
ipv6 route
```

A static route can specify:

```text
Destination prefix
Prefix length
Next-hop address
Exit interface
```

---

## Basic Syntax

```text
ipv6 route <destination-prefix> <prefix-length> <next-hop>
```

Example:

```text
R1(config)# ipv6 route 2001:db8:2::/64 2001:db8:12::2
```

This tells R1 how to reach:

```text
2001:DB8:2::/64
```

using:

```text
2001:DB8:12::2
```

as the next-hop.

---

## IPv6 Default Static Route

The IPv6 default route is:

```text
::/0
```

Example:

```text
R1(config)# ipv6 route ::/0 2001:db8:12::2
```

This means:

```text
If no more-specific IPv6 route exists,
send the traffic to the specified next-hop.
```

---

# 44. Link-Local Next-Hops

IPv6 static routes can use link-local addresses as next-hops.

This is particularly useful when the next-hop router is directly connected.

For example:

```text
R1
 |
 | FE80::2
 |
R2
```

R2's link-local address can be used as the next-hop.

Because link-local addresses are only meaningful on a specific interface/link, Cisco may need the outgoing interface specified as well.

---

## Fully Specified Static Route

A fully specified IPv6 static route identifies:

```text
Exit interface
+
Next-hop address
```

Example:

```text
R1(config)# ipv6 route 2001:db8:2::/64 g0/1 FE80::2
```

This tells the router:

```text
Destination:
2001:DB8:2::/64

Exit interface:
G0/1

Next-hop:
FE80::2
```

---

## Three Common Static Route Concepts

The notes identify:

```text
Directly attached
Recursive
Fully specified
```

### Directly Attached

The route specifies an exit interface.

```text
Destination
    |
    ↓
Exit Interface
```

### Recursive

The route specifies a next-hop address.

```text
Destination
    |
    ↓
Next-Hop
    |
    ↓
Router determines exit interface
```

### Fully Specified

The route specifies both:

```text
Next-Hop
+
Exit Interface
```

Conceptually:

```text
Fully Specified

Destination
     |
     +---- Next-Hop
     |
     +---- Exit Interface
```

---

# IPv6 Routing Example

Consider:

```text
LAN 1
2001:DB8:1::/64
      |
      |
     R1
      |
      | 2001:DB8:12::/64
      |
     R2
      |
      |
LAN 2
2001:DB8:2::/64
```

R1 needs a route to:

```text
2001:DB8:2::/64
```

A recursive static route could be:

```text
R1(config)# ipv6 route 2001:db8:2::/64 2001:db8:12::2
```

If R2 uses a link-local address:

```text
FE80::2
```

a fully specified route can be configured:

```text
R1(config)# ipv6 route 2001:db8:2::/64 g0/1 FE80::2
```

---

# NDP Message Summary

| Message | Purpose |
|---|---|
| NS | Neighbor Solicitation |
| NA | Neighbor Advertisement |
| RS | Router Solicitation |
| RA | Router Advertisement |

---

## Neighbor Solicitation

Used for:

```text
Neighbor discovery
Address resolution
Duplicate Address Detection
```

---

## Neighbor Advertisement

Used to respond to Neighbor Solicitation and provide neighbour information.

---

## Router Solicitation

A host can send an RS to request router information.

---

## Router Advertisement

A router sends an RA to advertise:

- Router presence
- IPv6 network information
- Prefix information
- Information used by SLAAC

The all-nodes multicast address:

```text
FF02::1
```

is used for messages intended for all IPv6 nodes on the local link.

---

# IPv6 Addressing and NDP Relationship

The overall process can be visualised as:

```text
                   IPv6 Network
                        |
                        |
                    IPv6 Router
                        |
                  Router Advertisement
                        |
                        ↓
                     Host
                        |
                Learns IPv6 Prefix
                        |
                        ↓
                  Creates Address
                        |
                        ↓
                       DAD
                        |
              +---------+---------+
              |                   |
        Duplicate?            Unique?
              |                   |
             Yes                  No
              |                   |
          Address                Use
          cannot be              address
          used
```

---

# IPv6 Neighbor Discovery Overview

```text
                 NDP
                  |
       +----------+----------+
       |          |          |
      NS         NA         RS/RA
       |          |          |
       |          |          +-- Router Discovery
       |          |
       |          +-- Neighbor information
       |
       +-- Neighbor discovery
       +-- Address resolution
       +-- DAD
```

---

# IPv6 Header Quick Reference

| Field | Size | Main Purpose |
|---|---:|---|
| Version | 4 bits | Identifies IPv6 |
| Traffic Class | 8 bits | Traffic/QoS handling |
| Flow Label | 20 bits | Identifies a traffic flow |
| Payload Length | 16 bits | Length of payload |
| Next Header | 8 bits | Next protocol/header |
| Hop Limit | 8 bits | Limits router hops |
| Source Address | 128 bits | Sender |
| Destination Address | 128 bits | Receiver |

IPv6 base header size:

```text
40 bytes
```

---

# IPv6 Special Addresses Quick Reference

| Address | Meaning |
|---|---|
| `::/128` | Unspecified |
| `::1/128` | Loopback |
| `::/0` | Default route |
| `2000::/3` | Global Unicast |
| `FC00::/7` | Unique Local |
| `FE80::/10` | Link-Local |
| `FF00::/8` | Multicast |
| `FF02::1` | All Nodes |
| `FF02::2` | All Routers |
| `FF02::1:FF00:0/104` | Solicited-node multicast base prefix |

---

# IPv6 Address Type Cheat Sheet

```text
Global Unicast
2000::/3
      ↓
Public / Internet

Unique Local
FC00::/7
      ↓
Private / Internal

Link-Local
FE80::/10
      ↓
Local link only

Multicast
FF00::/8
      ↓
One-to-many

Anycast
      ↓
One-to-one-of-many

Unspecified
::/128
      ↓
No specific address

Loopback
::1/128
      ↓
Local device
```

---

# IPv6 Configuration Cheat Sheet

## Enable IPv6 Routing

```text
R1(config)# ipv6 unicast-routing
```

## Configure IPv6 Address

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1::1/64
R1(config-if)# no shutdown
```

## Enable IPv6 Automatically

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 enable
```

## Configure EUI-64

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1::/64 eui-64
```

## Configure Anycast

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1::99/128 anycast
```

## Verify IPv6

```text
show ipv6 interface
```

```text
show ipv6 interface brief
```

```text
show ipv6 route
```

---

# IPv6 Static Route Cheat Sheet

## Recursive Static Route

```text
R1(config)# ipv6 route 2001:db8:2::/64 2001:db8:12::2
```

```text
Destination
     |
     ↓
Next-Hop
     |
     ↓
Router determines exit interface
```

---

## Fully Specified Static Route

```text
R1(config)# ipv6 route 2001:db8:2::/64 g0/1 FE80::2
```

```text
Destination
     |
     +---- Exit Interface
     |
     +---- Next-Hop
```

---

## Default Static Route

```text
R1(config)# ipv6 route ::/0 2001:db8:12::2
```

---

# IPv6 Address Generation Summary

IPv6 addresses can be generated/configured in several ways.

```text
                 IPv6 Address
                      |
        +-------------+-------------+
        |             |             |
      Manual        EUI-64        SLAAC
        |             |             |
    Administrator   MAC-based    Router
    configures      IID           Advertisement
    address                       |
                                  ↓
                              Prefix learned
                                  |
                                  ↓
                              IID generated
                                  |
                                  ↓
                                DAD
```

---

# Link-Local vs Global Unicast

```text
LINK-LOCAL

FE80::/10
     |
     +-- Local link
     +-- NDP
     +-- SLAAC
     +-- Router discovery
     +-- Not Internet-routable
```

```text
GLOBAL UNICAST

2000::/3
     |
     +-- Globally routable
     +-- Internet
     +-- Assigned IPv6 prefix
```

---

# IPv4 ARP vs IPv6 NDP

| IPv4 | IPv6 |
|---|---|
| ARP | NDP |
| ARP Request | Neighbor Solicitation |
| ARP Reply | Neighbor Advertisement |
| Broadcast | Multicast |
| ARP Table | Neighbor Table |
| Router discovery mechanisms differ | Router Solicitation / Advertisement |

---

# IPv6 Neighbor Discovery Flow

A simplified neighbour discovery process:

```text
Host A
  |
  | Neighbor Solicitation
  | Multicast
  ↓
Host B
  |
  | Neighbor Advertisement
  ↓
Host A
  |
  +-- Learns neighbour information
  |
  +-- Stores information
      in IPv6 Neighbor Table
```

---

# SLAAC Flow

```text
Host
 |
 | Router Solicitation
 ↓
Router
 |
 | Router Advertisement
 ↓
Host
 |
 +-- Learns IPv6 Prefix
 |
 +-- Generates Interface Identifier
 |
 +-- Creates IPv6 Address
 |
 +-- Performs DAD
 |
 ↓
IPv6 Address Ready
```

---

# DAD Flow

```text
Host wants to configure:

2001:DB8::10
       |
       ↓
Generate solicited-node multicast address
       |
       ↓
Send Neighbor Solicitation
       |
       ↓
Any response?
     /   \
   Yes    No
    |      |
 Duplicate  Address
 detected   appears unique
```

---

# IPv6 Multicast Scope Cheat Sheet

```text
FF01
 ↓
Interface-local

FF02
 ↓
Link-local

FF05
 ↓
Site-local

FF08
 ↓
Organization-local

FF0E
 ↓
Global
```

---

# IPv6 EUI-64 Cheat Sheet

```text
MAC Address

78:2B:CB:AC:08:67
        |
        ↓
Split

78:2B:CB | AC:08:67
        |
        ↓
Insert FFFE

78:2B:CB:FF:FE:AC:08:67
        |
        ↓
Invert U/L bit

7A:2B:CB:FF:FE:AC:08:67
        |
        ↓
Group into IPv6 hextets

7A2B:CBFF:FEAC:0867
```

---

# IPv6 Exam Revision

Before the CCNA exam, I should be able to explain the following without referring to notes.

## Addressing

- [ ] IPv4 uses 32 bits
- [ ] IPv6 uses 128 bits
- [ ] IPv6 uses hexadecimal
- [ ] IPv6 has 8 hextets
- [ ] Each hextet represents 16 bits
- [ ] Understand `/64`
- [ ] Understand `/48`
- [ ] Understand different IPv6 prefix lengths

## Address Representation

- [ ] Convert binary to hexadecimal
- [ ] Convert hexadecimal to binary
- [ ] Remove leading zeros
- [ ] Use `::` correctly
- [ ] Expand `::`
- [ ] Remember `::` can only be used once

## Address Types

- [ ] Global Unicast
- [ ] Unique Local
- [ ] Link-Local
- [ ] Multicast
- [ ] Anycast
- [ ] Loopback
- [ ] Unspecified

## EUI-64

- [ ] Explain why EUI-64 exists
- [ ] Convert a 48-bit MAC into a 64-bit IID
- [ ] Insert `FFFE`
- [ ] Invert the U/L bit
- [ ] Understand how EUI-64 can be used with SLAAC

## Multicast

- [ ] Know `FF00::/8`
- [ ] Know `FF02::1`
- [ ] Know `FF02::2`
- [ ] Understand multicast scopes
- [ ] Understand why IPv6 does not use broadcast
- [ ] Understand solicited-node multicast

## IPv6 Header

- [ ] Version
- [ ] Traffic Class
- [ ] Flow Label
- [ ] Payload Length
- [ ] Next Header
- [ ] Hop Limit
- [ ] Source Address
- [ ] Destination Address
- [ ] Know that the base IPv6 header is 40 bytes

## NDP

- [ ] Understand Neighbor Discovery Protocol
- [ ] Understand Neighbor Solicitation
- [ ] Understand Neighbor Advertisement
- [ ] Understand Router Solicitation
- [ ] Understand Router Advertisement
- [ ] Understand the IPv6 Neighbor Table
- [ ] Know that IPv6 does not use ARP

## SLAAC

- [ ] Know what SLAAC means
- [ ] Understand Router Advertisement
- [ ] Understand how a host learns the prefix
- [ ] Understand Interface Identifier generation
- [ ] Understand DAD

## Routing

- [ ] Configure IPv6 static routes
- [ ] Understand recursive static routes
- [ ] Understand directly attached static routes
- [ ] Understand fully specified static routes
- [ ] Understand link-local next-hops
- [ ] Know the IPv6 default route `::/0`

---

# CCNA-Style Questions

## Question 1

How many bits are in an IPv6 address?

```text
128 bits
```

---

## Question 2

How many hextets are in a full IPv6 address?

```text
8
```

---

## Question 3

How many bits are represented by one IPv6 hextet?

```text
16 bits
```

---

## Question 4

Can `::` be used twice in one IPv6 address?

```text
No
```

It can only be used once.

---

## Question 5

What is the IPv6 loopback address?

```text
::1
```

---

## Question 6

What is the IPv6 unspecified address?

```text
::
```

or:

```text
::/128
```

---

## Question 7

What is the IPv6 default route?

```text
::/0
```

---

## Question 8

What is the Global Unicast range covered in these notes?

```text
2000::/3
```

---

## Question 9

What is the Unique Local range?

```text
FC00::/7
```

Practical addresses commonly begin with:

```text
FD
```

---

## Question 10

What is the Link-Local range?

```text
FE80::/10
```

---

## Question 11

What is the IPv6 multicast range?

```text
FF00::/8
```

---

## Question 12

What is:

```text
FF02::1
```

?

Answer:

```text
All IPv6 Nodes
```

---

## Question 13

What is:

```text
FF02::2
```

?

Answer:

```text
All IPv6 Routers
```

---

## Question 14

Does IPv6 use broadcast?

```text
No
```

IPv6 uses multicast for one-to-many communication.

---

## Question 15

What protocol replaces ARP in IPv6?

```text
Neighbor Discovery Protocol (NDP)
```

---

## Question 16

What replaces an ARP Request?

```text
Neighbor Solicitation (NS)
```

---

## Question 17

What is the IPv6 equivalent of an ARP Reply?

```text
Neighbor Advertisement (NA)
```

---

## Question 18

What table replaces the IPv4 ARP table?

```text
IPv6 Neighbor Table
```

---

## Question 19

What does SLAAC stand for?

```text
Stateless Address Autoconfiguration
```

---

## Question 20

What messages are associated with router discovery?

```text
Router Solicitation (RS)
Router Advertisement (RA)
```

---

## Question 21

What does DAD stand for?

```text
Duplicate Address Detection
```

---

## Question 22

What message is used during DAD?

```text
Neighbor Solicitation
```

The message is sent to the appropriate solicited-node multicast address.

---

## Question 23

What is the base solicited-node multicast prefix?

```text
FF02::1:FF00:0/104
```

The last 24 bits of the IPv6 unicast address are appended to this prefix.

---

## Question 24

What is the IPv6 base header size?

```text
40 bytes
```

---

## Question 25

How large is the IPv6 Version field?

```text
4 bits
```

---

## Question 26

How large is the IPv6 Traffic Class field?

```text
8 bits
```

---

## Question 27

How large is the Flow Label?

```text
20 bits
```

---

## Question 28

How large is the Payload Length field?

```text
16 bits
```

---

## Question 29

How large is the Next Header field?

```text
8 bits
```

---

## Question 30

How large is the Hop Limit field?

```text
8 bits
```

---

## Question 31

What IPv6 header field performs a similar function to IPv4 TTL?

```text
Hop Limit
```

---

## Question 32

What command enables IPv6 routing on a Cisco router?

```text
R1(config)# ipv6 unicast-routing
```

---

## Question 33

What command automatically enables IPv6 on an interface and generates a link-local address?

```text
R1(config-if)# ipv6 enable
```

---

## Question 34

What keyword is used to configure Modified EUI-64?

```text
eui-64
```

Example:

```text
R1(config-if)# ipv6 address 2001:db8:1::/64 eui-64
```

---

## Question 35

What are the steps of Modified EUI-64?

```text
1. Split the MAC address in half.
2. Insert FFFE.
3. Invert the U/L bit.
```

---

## Question 36

What is a recursive IPv6 static route?

A static route where the router is given the:

```text
Next-hop IPv6 address
```

and must determine the outgoing interface.

---

## Question 37

What is a fully specified IPv6 static route?

A route specifying:

```text
Exit interface
+
Next-hop address
```

Example:

```text
ipv6 route 2001:db8:2::/64 g0/1 FE80::2
```

---

# Important IPv6 Memory Map

```text
                         IPv6
                          |
        +-----------------+------------------+
        |                 |                  |
    Addressing        Address Types       Protocols
        |                 |                  |
   128 bits          Global Unicast        NDP
   8 hextets         Unique Local           |
   Hexadecimal       Link-Local             +-- NS
        |             Multicast              +-- NA
        |             Anycast                +-- RS
        |             Loopback               +-- RA
        |             Unspecified
        |
        +--------------------------+
        |
      EUI-64
        |
        +-- Split MAC
        |
        +-- Insert FFFE
        |
        +-- Invert U/L bit
        |
        +-- 64-bit IID
        |
        +--------------------------+
        |
       SLAAC
        |
        +-- RS
        +-- RA
        +-- Prefix
        +-- IID
        +-- DAD
        |
        +--------------------------+
        |
      Routing
        |
        +-- Static Routes
        +-- Recursive
        +-- Directly Attached
        +-- Fully Specified
        +-- Link-Local Next-Hop
```

---

# Final IPv6 Cheat Sheet

```text
IPv6
    ↓
128 bits
    ↓
8 hextets
    ↓
16 bits per hextet
    ↓
Hexadecimal
```

### Shortening

```text
Remove leading zeros
        +
Replace consecutive zero hextets with ::
        +
:: only once
```

### Common Address Types

```text
2000::/3
    ↓
Global Unicast

FC00::/7
    ↓
Unique Local

FE80::/10
    ↓
Link-Local

FF00::/8
    ↓
Multicast

::1/128
    ↓
Loopback

::/128
    ↓
Unspecified

::/0
    ↓
Default Route
```

### Important Multicast

```text
FF02::1
    ↓
All Nodes

FF02::2
    ↓
All Routers
```

### Solicited-Node Multicast

```text
FF02::1:FF00:0/104
    +
Last 24 bits
    ↓
Solicited-Node Multicast Address
```

### EUI-64

```text
48-bit MAC
    ↓
Split
    ↓
Insert FFFE
    ↓
Invert U/L bit
    ↓
64-bit IID
```

### NDP

```text
NDP
 |
 +-- NS → Neighbor Solicitation
 |
 +-- NA → Neighbor Advertisement
 |
 +-- RS → Router Solicitation
 |
 +-- RA → Router Advertisement
```

### SLAAC

```text
RS
 ↓
RA
 ↓
Learn Prefix
 ↓
Generate IID
 ↓
DAD
 ↓
IPv6 Address
```

### Static Routing

```text
Directly Attached
        |
Recursive
        |
Fully Specified
        |
Link-Local Next-Hop
```

---

# Final CCNA IPv6 Checklist

Before considering IPv6 complete, I should be able to:

- [ ] Explain why IPv6 was introduced
- [ ] Explain 32-bit IPv4 vs 128-bit IPv6
- [ ] Explain hexadecimal notation
- [ ] Convert binary to hexadecimal
- [ ] Convert hexadecimal to binary
- [ ] Identify IPv6 hextets
- [ ] Shorten IPv6 addresses
- [ ] Expand IPv6 addresses
- [ ] Correctly use `::`
- [ ] Calculate IPv6 prefixes
- [ ] Understand `/48`
- [ ] Understand `/56`
- [ ] Understand `/64`
- [ ] Configure IPv6 addresses on Cisco routers
- [ ] Enable `ipv6 unicast-routing`
- [ ] Configure link-local addressing
- [ ] Configure EUI-64
- [ ] Calculate Modified EUI-64
- [ ] Explain the U/L bit
- [ ] Identify Global Unicast addresses
- [ ] Identify Unique Local addresses
- [ ] Identify Link-Local addresses
- [ ] Identify Multicast addresses
- [ ] Identify Anycast
- [ ] Identify Loopback
- [ ] Identify Unspecified address
- [ ] Identify the IPv6 default route
- [ ] Understand the 40-byte IPv6 header
- [ ] Explain every IPv6 header field
- [ ] Understand Next Header
- [ ] Understand Hop Limit
- [ ] Understand solicited-node multicast
- [ ] Understand NDP
- [ ] Explain Neighbor Solicitation
- [ ] Explain Neighbor Advertisement
- [ ] Explain Router Solicitation
- [ ] Explain Router Advertisement
- [ ] Understand the IPv6 Neighbor Table
- [ ] Explain SLAAC
- [ ] Explain DAD
- [ ] Configure IPv6 static routes
- [ ] Understand recursive static routes
- [ ] Understand directly attached static routes
- [ ] Understand fully specified static routes
- [ ] Understand link-local next-hops
- [ ] Troubleshoot basic IPv6 connectivity

---

# End of IPv6 Notes

This README documents my CCNA IPv6 study material, including IPv6 addressing, address representation, EUI-64, IPv6 address types, multicast, the IPv6 header, Neighbor Discovery Protocol, SLAAC, DAD, and IPv6 static routing.
