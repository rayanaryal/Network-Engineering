# IPv6

This section covers **IPv6 (Internet Protocol version 6)** and the IPv6 topics required for CCNA preparation.

The notes cover:

- IPv6 addressing
- IPv6 address types
- Hexadecimal and binary conversion
- IPv6 address structure
- IPv6 address shortening and expansion
- IPv6 prefixes
- Global Unicast Addresses
- Unique Local Addresses
- Link-Local Addresses
- Multicast
- Multicast scopes and groups
- Anycast
- Modified EUI-64
- Configuring IPv6 addresses on Cisco routers
- IPv6 routing
- Other IPv6 addresses
- CCNA-style IPv6 questions

---

# Table of Contents

1. [Exam Topics](#1-exam-topics)
2. [Things We Will Be Covering](#2-things-we-will-be-covering)
3. [What About IPv5](#3-what-about-ipv5)
4. [Hexadecimal](#4-hexadecimal)
5. [Binary to Hexadecimal](#5-binary-to-hexadecimal)
6. [Hexadecimal to Binary](#6-hexadecimal-to-binary)
7. [Why IPv6](#7-why-ipv6)
8. [IPv6 Basics](#8-ipv6-basics)
9. [Shortening IPv6 Addresses](#9-shortening-ipv6-addresses)
10. [Expanding Shortened IPv6 Addresses](#10-expanding-shortened-ipv6-addresses)
11. [Finding the IPv6 Prefix](#11-finding-the-ipv6-prefix)
12. [Finding IPv6 Prefixes with Different Prefix Lengths](#12-finding-ipv6-prefixes-with-different-prefix-lengths)
13. [Configuring IPv6 Addresses on a Router](#13-configuring-ipv6-addresses-on-a-router)
14. [Modified EUI-64](#14-modified-eui-64)
15. [EUI-64 Examples](#15-eui-64-examples)
16. [Configuring IPv6 Addresses with EUI-64](#16-configuring-ipv6-addresses-with-eui-64)
17. [Why Is the 7th Bit Inverted](#17-why-is-the-7th-bit-inverted)
18. [Global Unicast Addresses](#18-global-unicast-addresses)
19. [Unique Local Addresses](#19-unique-local-addresses)
20. [Link-Local Addresses](#20-link-local-addresses)
21. [Multicast Addresses](#21-multicast-addresses)
22. [Multicast Address Scopes](#22-multicast-address-scopes)
23. [Multicast Groups](#23-multicast-groups)
24. [Anycast Addresses](#24-anycast-addresses)
25. [Anycast Address Configuration](#25-anycast-address-configuration)
26. [Other IPv6 Addresses](#26-other-ipv6-addresses)
27. [CCNA IPv6 Quiz and Revision](#27-ccna-ipv6-quiz-and-revision)

---

# 1. Exam Topics

The main IPv6-related CCNA topics covered in these notes are:

### Configure and Verify IPv6 Addressing and Prefixes

Understanding how to:

- Configure IPv6 addresses
- Identify IPv6 prefixes
- Understand the structure of IPv6 addresses
- Verify IPv6 addressing

### Configure and Verify IPv6 Static Routing

IPv6 routing topics include:

- Default routes
- Network routes
- Host routes
- Floating static routes

### Compare IPv6 Address Types

Important IPv6 address types include:

- Global Unicast
- Unique Local
- Link-Local
- Multicast
- Anycast
- Other special IPv6 addresses

---

# 2. Things We Will Be Covering

The IPv6 study material is divided into two major parts.

## Part 1

The first part covers:

- Hexadecimal
- Why IPv6 was introduced
- IPv6 basics
- Configuring IPv6 addresses
- IPv6 prefixes

## Part 2

The second part covers:

- Continued IPv6 address configuration
- Modified EUI-64
- IPv6 address types
- Global Unicast
- Unique Local
- Link-Local
- Multicast
- Anycast
- Other IPv6 addresses

A simplified view:

```text
IPv6
 |
 +-- Hexadecimal
 |
 +-- Why IPv6?
 |
 +-- IPv6 Addressing
 |     |
 |     +-- Shortening
 |     +-- Expanding
 |     +-- Prefixes
 |
 +-- Configuration
 |     |
 |     +-- Manual IPv6 address
 |     +-- EUI-64
 |
 +-- IPv6 Address Types
       |
       +-- Global Unicast
       +-- Unique Local
       +-- Link-Local
       +-- Multicast
       +-- Anycast
       +-- Other
```

---

# 3. What About IPv5?

IPv5 was never actually introduced as the public successor to IPv4.

An **Internet Stream Protocol** was developed in the late 1970s.

It was never introduced for public use, but it used:

```text
5
```

as the value in the IP header's Version field.

Therefore, when the successor to IPv4 was developed, it was named:

```text
IPv6
```

rather than IPv5.

---

# 4. Hexadecimal

IPv6 uses **hexadecimal notation**.

Hexadecimal is:

```text
Base 16
```

and is commonly represented with:

```text
0x
```

The hexadecimal digits are:

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

The letters represent decimal values:

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

Digits:
0
1
```

Example:

```text
0b10
```

This is:

```text
Decimal 2
```

---

### Decimal

```text
Base 10

Digits:

0 1 2 3 4 5 6 7 8 9
```

---

### Hexadecimal

```text
Base 16

Digits:

0 1 2 3 4 5 6 7 8 9 A B C D E F
```

For example:

```text
Hexadecimal 10
```

means:

```text
Decimal 16
```

This is different from:

```text
Binary 10 = Decimal 2
```

---

# 5. Binary to Hexadecimal

Each hexadecimal digit represents exactly **4 binary bits**.

Therefore, to convert binary to hexadecimal:

1. Split the binary number into groups of 4 bits.
2. Convert each 4-bit group into hexadecimal.
3. Combine the hexadecimal digits.

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

Convert each group:

```text
1101 = 13 = D
1011 = 11 = B
```

Therefore:

```text
11011011 = DB
```

or:

```text
0b11011011 = 0xDB
```

---

## Another Example

Convert:

```text
00101111
```

to hexadecimal.

Split:

```text
0010 1111
```

Convert:

```text
0010 = 2
1111 = F
```

Therefore:

```text
00101111 = 0x2F
```

---

## Important Conversion Table

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

# 6. Hexadecimal to Binary

The reverse process is also important.

Each hexadecimal digit represents **4 binary bits**.

To convert hexadecimal to binary:

1. Split the hexadecimal number into individual digits.
2. Convert each hexadecimal digit into its 4-bit binary equivalent.
3. Combine the binary groups.

---

## Example

Convert:

```text
EC
```

to binary.

Split:

```text
E C
```

Convert:

```text
E = 14 = 1110
C = 12 = 1100
```

Therefore:

```text
EC = 11101100
```

or:

```text
0xEC = 0b11101100
```

---

## Another Example

Convert:

```text
D7
```

to binary.

```text
D = 13 = 1101
7 = 7  = 0111
```

Therefore:

```text
D7 = 11010111
```

---

# 7. Why IPv6?

The main reason for IPv6 is:

> **There are not enough IPv4 addresses.**

IPv4 uses:

```text
32 bits
```

which provides:

```text
2^32
```

possible addresses.

That is:

```text
4,294,967,296
```

IPv4 addresses.

When IPv4 was originally designed, the creators could not predict how large the Internet would become.

Several techniques were developed to conserve IPv4 address space:

```text
VLSM
Private IPv4 addresses
NAT
```

These helped extend the useful life of IPv4.

However, they are not the long-term solution to IPv4 address exhaustion.

The long-term solution is:

```text
IPv6
```

---

## IPv4 Address Allocation

IPv4 address assignments are controlled by:

> **IANA — Internet Assigned Numbers Authority**

IANA distributes IPv4 address space to:

> **RIRs — Regional Internet Registries**

The RIRs then assign address space to organisations that require it.

Examples of RIRs include:

```text
ARIN
RIPE NCC
APNIC
AFRINIC
LACNIC
```

The notes highlight historical IPv4 exhaustion events, including:

```text
24 September 2015
ARIN declared exhaustion of its IPv4 address pool.
```

and:

```text
21 August 2020
LACNIC announced its final IPv4 allocation.
```

---

## IPv6 Address Space

An IPv6 address is:

```text
128 bits
```

compared with:

```text
IPv4 = 32 bits
IPv6 = 128 bits
```

IPv6 therefore provides an enormous number of possible addresses:

```text
340,282,366,920,938,463,463,374,607,431,768,211,456
```

possible IPv6 addresses.

---

## IPv6 Address Example

An IPv6 address is normally written using hexadecimal.

Example:

```text
4201:0DB8:5917:EABD:6562:17EA:C92D:59BD/64
```

An IPv6 address contains:

```text
8 hexadecimal groups
```

Each group is called a:

> **Hextet**

Each hextet contains:

```text
4 hexadecimal digits
```

Therefore:

```text
8 hextets × 16 bits = 128 bits
```

---

# 8. IPv6 Basics

The basic structure of an IPv6 address can be represented as:

```text
128 bits
┌─────────────────────────────────────────────────────────────┐
│                         IPv6 Address                        │
└─────────────────────────────────────────────────────────────┘
```

A `/64` IPv6 address can commonly be divided into:

```text
64-bit Prefix
        +
64-bit Interface Identifier
```

For example:

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

Conceptually:

```text
2001:DB8:8B00:0001 | 0000:0000:0000:0001
        Prefix       | Interface Identifier
          64 bits    |      64 bits
```

The exact structure depends on the IPv6 address type and prefix length.

---

# 9. Shortening IPv6 Addresses

IPv6 addresses can be shortened to make them easier to read.

There are two major rules.

---

## Rule 1 — Remove Leading Zeros

Leading zeros in each hextet can be removed.

For example:

```text
0001 → 1
```

```text
0DB8 → DB8
```

Example:

```text
2001:0DB8:0000:0000:20A1:0020:0080:34BD
```

can become:

```text
2001:DB8:0:0:20A1:20:80:34BD
```

---

## Rule 2 — Consecutive Zero Hextets Can Become `::`

One sequence of consecutive all-zero hextets can be replaced by:

```text
::
```

Example:

```text
2001:DB8:0000:0000:0000:0000:0080:34BD
```

can become:

```text
2001:DB8::80:34BD
```

---

## Important Rule for `::`

The double colon:

```text
::
```

can only be used **once** in an IPv6 address.

Do not use it more than once because the receiver would not know how many zero hextets each `::` represents.

---

## Example

Full address:

```text
2001:DB8:0000:0000:20A1:0020:0080:34BD
```

Remove leading zeros:

```text
2001:DB8:0:0:20A1:20:80:34BD
```

Compress consecutive zero hextets:

```text
2001:DB8::20A1:20:80:34BD
```

---

## Practice Examples

The notes include examples such as:

```text
2000:AB78:20:1BF:ED89::1

FE80::2:0:0:FBE8

AE89:2100:1AC:F0::20F

2001:DB8:8B00:1000:2:BC0:D07:99

2001:DB8::1000
```

Remember:

```text
Leading zeros → remove them

Consecutive zero hextets → replace with ::
```

but:

```text
:: can only appear once
```

---

# 10. Expanding Shortened IPv6 Addresses

When expanding an IPv6 address, reverse the shortening process.

There are two main steps.

---

## Step 1 — Add Leading Zeros

Every hextet must contain four hexadecimal characters.

Example:

```text
FE80:2:0:0:FBE8
```

First add leading zeros:

```text
FE80:0002:0000:0000:FBE8
```

---

## Step 2 — Expand `::`

If `::` is present, replace it with enough:

```text
0000
```

hextets to produce exactly **8 hextets**.

---

## Example

Shortened:

```text
FE80::2:0:0:FBE8
```

We already have:

```text
FE80
2
0
0
FBE8
```

That is:

```text
5 hextets
```

IPv6 requires:

```text
8 hextets
```

Therefore `::` represents:

```text
3 hextets of zeros
```

Expanded:

```text
FE80:0000:0000:0000:0002:0000:0000:FBE8
```

---

## Practice Examples

Expand:

```text
FE80::2:0:0:FBE8
```

Answer:

```text
FE80:0000:0000:0000:0002:0000:0000:FBE8
```

Expand:

```text
2001:DB8:1:B23:2309::C1
```

Answer:

```text
2001:0DB8:0001:0B23:2309:0000:0000:00C1
```

Expand:

```text
FD00::1000:0689:9000:0CDF
```

Answer:

```text
FD00:0000:0000:0000:1000:0689:9000:0CDF
```

Expand:

```text
FF02::2
```

Answer:

```text
FF02:0000:0000:0000:0000:0000:0000:0002
```

Expand:

```text
::1
```

Answer:

```text
0000:0000:0000:0000:0000:0000:0000:0001
```

---

# 11. Finding the IPv6 Prefix

The prefix identifies the network portion of the IPv6 address.

A common enterprise IPv6 allocation is:

```text
/48
```

while IPv6 LAN subnets commonly use:

```text
/64
```

This means an enterprise receiving a `/48` and creating `/64` subnets has:

```text
64 - 48 = 16 bits
```

available for creating subnet identifiers.

The remaining:

```text
64 bits
```

form the Interface Identifier in a typical `/64` subnet.

---

## Example

Consider:

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

Conceptually:

```text
2001:DB8:8B00 | 0001 | 0000:0000:0000:0001
      |           |             |
      |           |             |
 Global Routing  Subnet       Interface
    Prefix       ID           Identifier
```

For a `/64`:

```text
2001:DB8:8B00:0001::
```

is the prefix.

Written as a network prefix:

```text
2001:DB8:8B00:1::/64
```

---

## `/48` Allocation

If an enterprise receives:

```text
2001:DB8:8B00::/48
```

and uses:

```text
/64
```

subnets, the fourth hextet can be used to identify different subnets.

For example:

```text
2001:DB8:8B00:1::/64
2001:DB8:8B00:2::/64
2001:DB8:8B00:3::/64
2001:DB8:8B00:4::/64
```

---

# 12. Finding IPv6 Prefixes with Different Prefix Lengths

The prefix does not always have to be `/64`.

The notes include examples using:

```text
/56
/63
/62
/71
/93
```

The important concept is:

> **The prefix length tells us exactly how many bits belong to the network prefix.**

---

## Example — `/56`

Given:

```text
300D:00F2:0B34:2100:0000:0000:1200:0001/56
```

The first:

```text
56 bits
```

belong to the prefix.

The resulting prefix is:

```text
300D:F2:B34:2100::/56
```

---

## Example — `/93`

Given:

```text
2001:DB8:8B00:0001:FB89:2178:0020:2011/93
```

The prefix contains the first:

```text
93 bits
```

The important thing to remember is that prefix lengths do not always end exactly on a 16-bit hextet boundary.

---

## Example Prefixes

The notes include examples such as:

```text
FE80::/10

2001:DB8:1:B23::/64

2001:DB8:BAD:CAFE:1200::/71

2001:DB8:0:FEEC::0/62

2001:DB8:9BAD:BABE::00/63
```

---

## Prefix Calculation Method

When finding a prefix:

```text
1. Write the full IPv6 address.
2. Identify the prefix length.
3. Count the required number of bits.
4. Keep the prefix bits.
5. Set host/interface bits to zero.
6. Write the result using valid IPv6 notation.
```

---

# 13. Configuring IPv6 Addresses on a Router

IPv6 addresses can be configured manually on Cisco routers.

A router must also be enabled to perform IPv6 routing.

---

## Enable IPv6 Routing

Use:

```text
R1(config)# ipv6 unicast-routing
```

This enables the router to perform IPv6 routing.

Important:

```text
R1(config)# ipv6 unicast-routing
```

is a **global configuration command**.

It is not entered under the interface.

---

## Configure an IPv6 Address

Enter the interface:

```text
R1(config)# interface gigabitEthernet 0/0
```

Configure an IPv6 address:

```text
R1(config-if)# ipv6 address 2001:db8:0:1::1/64
```

Enable the interface:

```text
R1(config-if)# no shutdown
```

Example:

```text
R1(config)# ipv6 unicast-routing

R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:0:1::1/64

R1(config-if)# no shutdown
```

---

## Example Topology

```text
                 IPv6 Network

       LAN 1                         LAN 2
2001:DB8:0:1::/64             2001:DB8:0:2::/64
       |                              |
       |                              |
      G0/0                          G0/1
       \                              /
        \                            /
                 R1
```

Possible configuration:

```text
R1(config)# ipv6 unicast-routing

R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:0:1::1/64
R1(config-if)# no shutdown

R1(config)# interface g0/1
R1(config-if)# ipv6 address 2001:db8:0:2::1/64
R1(config-if)# no shutdown
```

---

## Verify IPv6 Addresses

A useful command is:

```text
show ipv6 interface
```

You can also use:

```text
show ipv6 interface brief
```

to get a concise view of IPv6-enabled interfaces and addresses.

---

# 14. Modified EUI-64

EUI-64 is a method used to generate a **64-bit Interface Identifier** from a **48-bit MAC address**.

The document explains why this is necessary:

```text
IPv6 Interface Identifier = 64 bits

MAC Address = 48 bits
```

Therefore, a standard method is required to convert:

```text
48-bit MAC
      ↓
64-bit Interface Identifier
```

That method is:

> **Modified EUI-64**

---

## Why 64-bit IID?

IPv6 commonly uses a:

```text
64-bit Interface Identifier
```

for a `/64` subnet.

A traditional Ethernet MAC address is:

```text
48 bits
```

Therefore:

```text
48-bit MAC
     ↓
Modified EUI-64
     ↓
64-bit Interface Identifier
```

---

## What Does EUI Stand For?

EUI means:

> **Extended Unique Identifier**

Modified EUI-64 is a method of converting a 48-bit MAC address into a 64-bit Interface Identifier.

The Interface Identifier can then form the host/interface portion of an IPv6 address.

---

# 15. EUI-64 Examples

The Modified EUI-64 conversion process has three major steps.

---

## Step 1 — Divide the MAC Address in Half

Example MAC:

```text
1234:5678:90AB
```

Divide it:

```text
1234:56 | 78:90AB
```

---

## Step 2 — Insert `FFFE`

Insert:

```text
FFFE
```

between the two halves.

```text
1234:56FF:FE78:90AB
```

---

## Step 3 — Invert the 7th Bit

The first byte is modified by inverting the Universal/Local bit.

Example:

```text
MAC
↓
EUI-64
↓
Invert U/L bit
```

This produces the final 64-bit Interface Identifier.

---

## Complete Process

```text
48-bit MAC

AA:BB:CC:DD:EE:FF
       |
       | Split in half
       ↓
AA:BB:CC | DD:EE:FF
       |
       | Insert FFFE
       ↓
AA:BB:CC:FF:FE:DD:EE:FF
       |
       | Invert U/L bit
       ↓
Modified EUI-64 Interface ID
```

---

## Example From the Notes

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

Invert the U/L bit of the first byte:

```text
78 → 7A
```

Therefore:

```text
7A:2B:CB:FF:FE:AC:08:67
```

As IPv6 hextets:

```text
7A2B:CBFF:FEAC:0867
```

---

# 16. Configuring IPv6 Addresses with EUI-64

Cisco IOS can automatically generate the Interface Identifier using EUI-64.

The configuration uses:

```text
eui-64
```

Example:

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:abcd:1234::/64 eui-64
```

The router uses the interface MAC address to generate the 64-bit Interface Identifier.

---

## Example

Prefix:

```text
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

Final IPv6 address:

```text
2001:db8:abcd:1234:7A2B:CBFF:FEAC:0867
```

---

## Why Use EUI-64?

One reason is automatic address generation.

The notes connect this with:

> **SLAAC — Stateless Address Autoconfiguration**

With EUI-64, a device can generate its Interface Identifier from its MAC address without requiring manual host configuration for the Interface ID.

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
IPv6 Address
```

---

## EUI-64 Practice Examples

The document contains examples including:

```text
78:2B:CB:AC:08:67
```

```text
00:50:56:C0:00:01
```

and other MAC addresses.

The process is always:

```text
1. Split MAC address
2. Insert FFFE
3. Invert U/L bit
4. Use result as 64-bit Interface Identifier
```

---

# 17. Why Is the 7th Bit Inverted?

This is an important EUI-64 concept.

MAC addresses can be divided into two categories:

### UAA — Universally Administered Address

A MAC address assigned to a device by the manufacturer.

### LAA — Locally Administered Address

A MAC address manually assigned or locally configured by an administrator.

---

## U/L Bit

The 7th bit of the MAC address is called the:

> **U/L bit — Universal/Local bit**

For the MAC address:

```text
U/L bit = 0
```

means:

```text
Universally Administered Address (UAA)
```

while:

```text
U/L bit = 1
```

means:

```text
Locally Administered Address (LAA)
```

---

## Modified EUI-64 Reverses the Meaning

When creating a Modified EUI-64 Interface Identifier, the U/L bit is inverted.

Therefore, in the EUI-64 Interface Identifier:

```text
U/L bit = 0
```

indicates the original MAC was an:

```text
LAA
```

and:

```text
U/L bit = 1
```

indicates the original MAC was a:

```text
UAA
```

---

## Easy Memory

```text
MAC Address

0 → Universal
1 → Local
```

After Modified EUI-64:

```text
EUI-64

0 → Original MAC was Local
1 → Original MAC was Universal
```

---

# 18. Global Unicast Addresses

Global Unicast IPv6 addresses are public addresses that can be used over the Internet.

They are intended to be globally unique.

The original Global Unicast range was defined as:

```text
2000::/3
```

This covers addresses beginning in the range:

```text
2000::
through
3FFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF
```

The notes also describe Global Unicast addresses as addresses that are not reserved for another purpose.

---

## Global Unicast Structure

A typical Global Unicast address can be divided into:

```text
48-bit Global Routing Prefix
        +
16-bit Subnet Identifier
        +
64-bit Interface Identifier
```

Example:

```text
2001:DB8:8B00:0001:0000:0000:0000:0001/64
```

Conceptually:

```text
2001:DB8:8B00 | 0001 | 0000:0000:0000:0001
      |           |              |
      |           |              |
 Global Routing  Subnet       Interface
    Prefix        ID          Identifier
```

---

## Global Routing Prefix

The Global Routing Prefix is assigned by the ISP.

---

## Subnet Identifier

The enterprise can use the Subnet Identifier to create different IPv6 subnets.

---

## Interface Identifier

The Interface Identifier identifies the interface/host portion of the address.

---

# 19. Unique Local Addresses

Unique Local IPv6 addresses are private IPv6 addresses.

They:

- Cannot be used over the public Internet
- Do not require registration
- Can be used freely inside internal networks
- Are not routed over the Internet

---

## Unique Local Address Range

The notes identify:

```text
FC00::/7
```

However, the standard requires the 8th bit to be set to `1`, meaning practical Unique Local Addresses begin with:

```text
FD
```

Therefore, you will commonly see:

```text
FD00::/8
```

---

## Example

```text
FDA5:93AC:8A8F:0001:0000:0000:0000:0001/64
```

A Unique Local address contains:

```text
Global ID
+
Subnet ID
+
Interface ID
```

---

## Unique Local Address Structure

Conceptually:

```text
7-bit prefix + L bit
        +
40-bit Global ID
        +
16-bit Subnet ID
        +
64-bit Interface ID
```

The Global ID should be generated in a way that helps avoid address overlap, particularly if organisations later merge.

---

## Easy Memory

```text
Global Unicast
     ↓
Public / Internet

Unique Local
     ↓
Private / Internal
```

---

# 20. Link-Local Addresses

Link-Local IPv6 addresses are automatically generated on IPv6-enabled interfaces.

They are used for communication within the local link/subnet.

The address block is:

```text
FE80::/10
```

The standard requires the bits after the `/10` prefix to be zero for the link-local prefix, so normal link-local addresses begin with:

```text
FE80
```

---

## Enable IPv6 on an Interface

Cisco IOS can automatically generate a link-local address when IPv6 is enabled on an interface.

Command:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 enable
```

This enables IPv6 on the interface and automatically generates a link-local address.

---

## Link-Local Addresses Are Not Routed

Link-local addresses are intended for communication on the local link.

Routers do not route packets using a link-local destination across different subnets.

Conceptually:

```text
LAN 1
 |
 | FE80::/10
 |
 R1
 X
 |
 | cannot route link-local destination
 |
LAN 2
```

---

## Common Uses of Link-Local Addresses

The notes identify several important uses.

### Routing Protocol Peerings

For example:

```text
OSPFv3
```

can use link-local addresses for neighbour adjacencies.

---

### Next-Hop Addresses

Link-local addresses can be used as next-hop addresses for IPv6 static routes.

---

### Neighbor Discovery Protocol

IPv6 uses:

> **NDP — Neighbor Discovery Protocol**

NDP replaces the role that ARP performs in IPv4.

Link-local addresses are important to NDP operation.

---

## Easy Memory

```text
FE80::/10
     ↓
Link-Local
     ↓
Local link only
     ↓
Not routed across subnets
```

---

# 21. Multicast Addresses

IPv6 uses multicast extensively.

The three basic communication models are:

```text
Unicast
Multicast
Broadcast
```

---

## Unicast

Unicast is:

> One-to-one

```text
Source
  |
  +-----------------> Destination
```

One source communicates with one destination.

---

## Broadcast

Broadcast is:

> One-to-all

```text
             +---- Host
             |
Source ------+---- Host
             |
             +---- Host
```

However:

> **IPv6 does not use broadcast addresses.**

There is no IPv6 broadcast address.

---

## Multicast

Multicast is:

> One-to-many

```text
             +---- Host A
             |
Source ------+---- Host B
             |
             +---- Host C
```

Only devices that have joined the specific multicast group receive the multicast traffic.

---

## IPv6 Multicast Range

IPv6 multicast addresses use:

```text
FF00::/8
```

Therefore, IPv6 multicast addresses begin with:

```text
FF
```

---

## Easy Memory

```text
Unicast
1 → 1

Broadcast
1 → All

Multicast
1 → Many
```

IPv6:

```text
No Broadcast
Use Multicast instead
```

---

# 22. Multicast Address Scopes

IPv6 multicast addresses contain a scope value that indicates how far the multicast traffic can travel.

The important scopes from the notes are:

| Scope | Meaning |
|---|---|
| `FF01` | Interface-local / Node-local |
| `FF02` | Link-local |
| `FF05` | Site-local |
| `FF08` | Organization-local |
| `FF0E` | Global |

---

## Interface-Local — `FF01`

The packet does not leave the local device.

It can be used for communication with services within the local device.

```text
Device
 |
 +-- FF01
     |
     +-- Stays inside device
```

---

## Link-Local — `FF02`

The packet remains within the local subnet/link.

Routers do not forward the multicast traffic between subnets.

```text
LAN
 |
 +-- Host
 +-- Host
 +-- Host

FF02
 ↓
Local link
```

---

## Site-Local — `FF05`

The packet can be forwarded by routers but should remain within a single physical location.

It should not be forwarded across a WAN.

---

## Organization-Local — `FF08`

This has a wider scope than site-local.

It can be used within an entire organisation.

---

## Global — `FF0E`

Global scope has no defined local boundary and can potentially be routed over the Internet.

---

## Easy Scope Memory

```text
FF01 → Interface-local
FF02 → Link-local
FF05 → Site-local
FF08 → Organization-local
FF0E → Global
```

---

# 23. Multicast Groups

IPv6 multicast groups allow hosts and routers to join specific multicast groups.

A device can join a multicast group and receive traffic sent to that group.

For example:

```text
                 Multicast Group
                       |
              +--------+--------+
              |        |        |
             R1       R2       R3
              \        |       /
               \       |      /
                Joined Members
```

The document also illustrates multicast groups joined by a router interface.

Important concepts include:

```text
All Nodes multicast group
All Routers multicast group
```

---

## All Nodes

The IPv6 all-nodes multicast group is:

```text
FF02::1
```

It represents all IPv6 nodes on the local link.

---

## All Routers

The IPv6 all-routers multicast group is:

```text
FF02::2
```

It represents all IPv6 routers on the local link.

---

## Important

Because IPv6 does not use broadcast:

```text
IPv6
   |
   +-- No broadcast
   |
   +-- Uses multicast groups
```

---

# 24. Anycast Addresses

Anycast is an IPv6 communication method that can be described as:

> **One-to-one-of-many**

Multiple routers can be configured with the same IPv6 address.

They advertise that address through a routing protocol.

When a host sends traffic to that destination address, routing determines which router is the nearest/most appropriate destination based on the routing metric.

---

## Anycast Example

Imagine three routers:

```text
                 R1
              10 hops
                /
               /
Host ---------- Destination
               \
                \
              R2
              5 hops
               
                \
                 R3
                12 hops
```

All three routers use the same IPv6 anycast address:

```text
2001:db8:1::99
```

The routing system determines the closest/most appropriate router.

If R2 has the best route:

```text
Host
 |
 | 2001:db8:1::99
 |
 ↓
R2
```

The traffic reaches R2.

---

## Important Anycast Point

There is:

> **No specific IPv6 address range reserved for Anycast.**

A normal unicast address can be used as an anycast address.

For example:

```text
Global Unicast
```

or:

```text
Unique Local
```

can be used.

The address is configured as an anycast address on the interface.

---

# 25. Anycast Address Configuration

A Cisco router can configure an IPv6 address as anycast by using:

```text
anycast
```

Example:

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:1::99/128 anycast
```

The important part is:

```text
ipv6 address
```

followed by the IPv6 address and:

```text
anycast
```

---

## Anycast Concept

```text
          Same IPv6 Address
          2001:DB8:1::99
                  |
        +---------+---------+
        |         |         |
       R1        R2        R3
        |         |         |
        +---------+---------+
                  |
          Routing determines
          nearest destination
```

---

# 26. Other IPv6 Addresses

There are other special IPv6 addresses that are important to understand.

---

## Unspecified Address

The IPv6 unspecified address is:

```text
::
```

or:

```text
0:0:0:0:0:0:0:0
```

It is written as:

```text
::/128
```

It can be used when a device does not yet know its own IPv6 address.

It is similar conceptually to the IPv4 unspecified address:

```text
0.0.0.0
```

---

## IPv6 Default Route

The IPv6 default route is:

```text
::/0
```

This means:

```text
All IPv6 destinations
```

unless a more specific route exists.

Conceptually:

```text
::/0
 |
 +---- Default route
```

---

## Loopback Address

The IPv6 loopback address is:

```text
::1
```

with prefix length:

```text
/128
```

Therefore:

```text
::1/128
```

It is used to test the local protocol stack.

Traffic sent to:

```text
::1
```

is processed by the local device and is not sent to another device.

---

## IPv4 Equivalent

IPv6:

```text
::1
```

IPv4:

```text
127.0.0.0/8
```

The commonly used IPv4 loopback address is:

```text
127.0.0.1
```

---

# IPv6 Address Types — Quick Summary

```text
IPv6 Address Types

                    IPv6
                      |
       +--------------+--------------+
       |              |              |
    Unicast        Multicast       Anycast
       |
   +---+---+
   |   |   |
  GUA ULA Link-Local
```

---

## Global Unicast

```text
Public
Internet-routable
2000::/3
```

---

## Unique Local

```text
Private
Internal networks
FC00::/7
Practical addresses commonly begin with FD
```

---

## Link-Local

```text
FE80::/10
Local link only
Not routed
Automatically generated when IPv6 is enabled
```

---

## Multicast

```text
FF00::/8
One-to-many
IPv6 does not use broadcast
```

---

## Anycast

```text
One-to-one-of-many
Multiple devices use the same address
Routing selects the nearest/appropriate destination
```

---

## Unspecified

```text
::/128
```

---

## Loopback

```text
::1/128
```

---

# IPv6 Address Type Cheat Sheet

| Address Type | Prefix / Address | Purpose |
|---|---|---|
| Global Unicast | `2000::/3` | Public / Internet |
| Unique Local | `FC00::/7` | Private / internal |
| Link-Local | `FE80::/10` | Local link |
| Multicast | `FF00::/8` | One-to-many |
| Unspecified | `::/128` | No address yet |
| Loopback | `::1/128` | Local device testing |
| Anycast | No dedicated range | One-to-one-of-many |

---

# IPv6 Configuration Cheat Sheet

## Enable IPv6 Routing

```text
R1(config)# ipv6 unicast-routing
```

---

## Configure a Normal IPv6 Address

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:1:1::1/64

R1(config-if)# no shutdown
```

---

## Enable IPv6 and Automatically Generate Link-Local

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 enable
```

This automatically generates a link-local IPv6 address.

---

## Configure EUI-64

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:1:1::/64 eui-64
```

---

## Configure Anycast

```text
R1(config)# interface g0/0

R1(config-if)# ipv6 address 2001:db8:1::99/128 anycast
```

---

# IPv6 Verification Commands

Useful Cisco IOS commands include:

```text
show ipv6 interface
```

```text
show ipv6 interface brief
```

```text
show ipv6 route
```

These commands can be used to verify:

```text
IPv6 addresses
Interface status
IPv6 routing information
```

---

# IPv6 Address Shortening — Quick Revision

Remember these two rules:

```text
RULE 1
Remove leading zeros from each hextet.
```

Example:

```text
0DB8 → DB8
```

and:

```text
RULE 2
Replace one sequence of consecutive zero hextets with ::
```

Example:

```text
2001:DB8:0:0:0:0:1:1
```

becomes:

```text
2001:DB8::1:1
```

Important:

```text
:: can only be used once.
```

---

# IPv6 Expansion — Quick Revision

When expanding:

```text
1. Add leading zeros.
2. Expand ::
3. Make exactly 8 hextets.
4. Each hextet must contain 4 hexadecimal digits.
```

Example:

```text
2001:DB8::1
```

becomes:

```text
2001:0DB8:0000:0000:0000:0000:0000:0001
```

---

# Modified EUI-64 — Quick Revision

Remember:

```text
48-bit MAC
     |
     ↓
Split MAC in half
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

Example:

```text
78:2B:CB:AC:08:67
```

Split:

```text
78:2B:CB | AC:08:67
```

Insert FFFE:

```text
78:2B:CB:FF:FE:AC:08:67
```

Invert U/L bit:

```text
78 → 7A
```

Final IID:

```text
7A2B:CBFF:FEAC:0867
```

---

# IPv6 Multicast — Quick Revision

IPv6 does not use broadcast.

Instead:

```text
IPv6
 ↓
Multicast
```

Important multicast addresses:

```text
FF02::1
```

All IPv6 nodes on the local link.

```text
FF02::2
```

All IPv6 routers on the local link.

---

# IPv6 Multicast Scopes — Quick Revision

```text
FF01 → Interface-local
FF02 → Link-local
FF05 → Site-local
FF08 → Organization-local
FF0E → Global
```

---

# 27. CCNA IPv6 Quiz and Revision

The original notes contain several CCNA-style questions.

Use the following questions as a revision checklist.

---

## Question 1 — EUI-64

R1's G0/1 interface has the MAC address:

```text
60:24:4F:A3:0B:01
```

What IPv6 address will be generated after configuring:

```text
R1(config-if)# ipv6 address 2001:db8:0:1::/64 eui-64
```

### Method

Start with:

```text
60:24:4F:A3:0B:01
```

Split:

```text
60:24:4F | A3:0B:01
```

Insert:

```text
FFFE
```

```text
60:24:4F:FF:FE:A3:0B:01
```

Invert the U/L bit.

The first byte:

```text
60
```

becomes:

```text
62
```

Therefore the Interface Identifier becomes:

```text
6224:4FFF:FEA3:0B01
```

Final address:

```text
2001:DB8:0:1:6224:4FFF:FEA3:0B01
```

---

# Question 2 — Global ID

Which portion is the Global ID in a Unique Local IPv6 address such as:

```text
FD89:3B12:3794:0020:0800:0000:2347:0001/64
```

Remember the basic ULA structure:

```text
Prefix
+
Global ID
+
Subnet ID
+
Interface ID
```

The Global ID is the portion following the ULA prefix and before the Subnet ID.

---

# Question 3 — Multicast

R3 sends an IPv6 multicast message to all other routers on the local subnet.

Which destination address represents the all-routers multicast group?

```text
FF02::2
```

Remember:

```text
FF02::1 → All Nodes
FF02::2 → All Routers
```

---

# Question 4 — IPv6 Broadcast

Does IPv6 have a broadcast address?

```text
No
```

IPv6 does not use broadcast.

Instead, IPv6 uses:

```text
Multicast
```

for one-to-many communication.

---

# Question 5 — Link-Local

Which IPv6 address range is used for link-local addresses?

```text
FE80::/10
```

Remember:

```text
FE80 → Link-Local
```

Link-local addresses are not routed between subnets.

---

# Question 6 — Unique Local

Which address range is associated with Unique Local IPv6 addresses?

```text
FC00::/7
```

Practical Unique Local addresses commonly begin with:

```text
FD
```

They are used for internal/private networks.

---

# Question 7 — Global Unicast

Which range was originally defined for Global Unicast IPv6 addresses?

```text
2000::/3
```

These addresses are public and can be used over the Internet.

---

# Question 8 — Loopback

What is the IPv6 loopback address?

```text
::1
```

Prefix:

```text
::1/128
```

IPv4 equivalent:

```text
127.0.0.1
```

---

# Question 9 — Unspecified Address

What is the IPv6 unspecified address?

```text
::
```

Prefix:

```text
::/128
```

IPv4 equivalent:

```text
0.0.0.0
```

---

# Question 10 — Default Route

What is the IPv6 default route?

```text
::/0
```

This represents all IPv6 destinations when no more-specific route exists.

---

# Question 11 — Enable IPv6 Routing

Which Cisco IOS command enables IPv6 routing?

Correct command:

```text
R1(config)# ipv6 unicast-routing
```

Notice that it is entered in:

```text
Global configuration mode
```

not interface configuration mode.

---

# Question 12 — EUI-64

What are the three main steps of Modified EUI-64?

```text
1. Split the 48-bit MAC address in half.
2. Insert FFFE between the halves.
3. Invert the U/L bit.
```

---

# Question 13 — IPv6 Address Size

How many bits are in an IPv6 address?

```text
128 bits
```

How many bits are in an IPv4 address?

```text
32 bits
```

---

# Question 14 — IPv6 Hextets

How many hexadecimal groups/hextets are in a full IPv6 address?

```text
8
```

How many bits are represented by each hextet?

```text
16 bits
```

Therefore:

```text
8 × 16 = 128 bits
```

---

# Question 15 — IPv6 Compression

Can `::` be used more than once in an IPv6 address?

```text
No
```

It can only represent one consecutive sequence of zero hextets.

---

# Question 16 — IPv6 Multicast

What is the IPv6 multicast range?

```text
FF00::/8
```

---

# Question 17 — Anycast

What is Anycast?

```text
One-to-one-of-many
```

Multiple devices can use the same IPv6 address, and routing directs the traffic to the nearest/most appropriate destination.

---

# Question 18 — Anycast Address Range

Does IPv6 have a dedicated Anycast address range?

```text
No
```

A regular unicast address can be configured as an anycast address.

Example:

```text
R1(config-if)# ipv6 address 2001:db8:1::99/128 anycast
```

---

# Final IPv6 Cheat Sheet

```text
IPv6
|
+-- Address Size
|     |
|     +-- 128 bits
|
+-- Hexadecimal
|     |
|     +-- Base 16
|     +-- 0-9
|     +-- A-F
|
+-- Address Structure
|     |
|     +-- 8 hextets
|     +-- 16 bits per hextet
|
+-- Shortening
|     |
|     +-- Remove leading zeros
|     +-- :: replaces consecutive zero hextets
|     +-- :: can only be used once
|
+-- Prefix
|     |
|     +-- Common LAN prefix = /64
|     +-- Enterprise allocation commonly = /48
|
+-- Address Types
      |
      +-- Global Unicast
      |     2000::/3
      |
      +-- Unique Local
      |     FC00::/7
      |     Commonly FD...
      |
      +-- Link-Local
      |     FE80::/10
      |
      +-- Multicast
      |     FF00::/8
      |
      +-- Anycast
      |     No dedicated range
      |
      +-- Unspecified
      |     ::/128
      |
      +-- Loopback
            ::1/128
```

---

# IPv6 Address Types — Memorise This

```text
2000::/3
    ↓
Global Unicast
    ↓
Public / Internet


FC00::/7
    ↓
Unique Local
    ↓
Private / Internal


FE80::/10
    ↓
Link-Local
    ↓
Local link only


FF00::/8
    ↓
Multicast
    ↓
One-to-many


::
    ↓
Unspecified


::1
    ↓
Loopback
```

---

# IPv6 Multicast — Memorise This

```text
FF01 → Interface-local
FF02 → Link-local
FF05 → Site-local
FF08 → Organization-local
FF0E → Global
```

Important groups:

```text
FF02::1 → All Nodes
FF02::2 → All Routers
```

---

# IPv6 Configuration — Memorise This

Enable IPv6 routing:

```text
R1(config)# ipv6 unicast-routing
```

Configure IPv6 manually:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1:1::1/64
R1(config-if)# no shutdown
```

Enable IPv6 and automatically generate a link-local address:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 enable
```

Use EUI-64:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1:1::/64 eui-64
```

Configure Anycast:

```text
R1(config)# interface g0/0
R1(config-if)# ipv6 address 2001:db8:1::99/128 anycast
```

Verify:

```text
show ipv6 interface
show ipv6 interface brief
show ipv6 route
```

---

# IPv6 vs IPv4 — Key Differences

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address size | 32 bits | 128 bits |
| Notation | Decimal | Hexadecimal |
| Broadcast | Yes | No |
| Multicast | Supported | Heavily used |
| Address exhaustion | Major limitation | Vast address space |
| Address discovery | ARP | NDP |
| Loopback | `127.0.0.1` | `::1` |
| Unspecified | `0.0.0.0` | `::` |
| Default route | `0.0.0.0/0` | `::/0` |
| Link-local | `169.254.0.0/16` | `FE80::/10` |

---

# Final CCNA IPv6 Memory Map

```text
                         IPv6
                          |
        +-----------------+------------------+
        |                 |                  |
    Addressing        Address Types       Routing
        |                 |                  |
    128 bits         Global Unicast     IPv6 Static
    8 hextets        Unique Local       Routes
    Hexadecimal      Link-Local
                     Multicast
                     Anycast
                     Other
        |
        +--------------------------+
        |                          |
    Shortening                  Prefix
        |                          |
    Remove 0s                  /48
    Use ::                    /56
    Once only                 /64
                               etc.
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
```

---

# Final CCNA IPv6 Checklist

Before the CCNA exam, make sure you can confidently:

- [ ] Explain why IPv6 was introduced
- [ ] Explain the difference between IPv4 and IPv6 address sizes
- [ ] Convert binary to hexadecimal
- [ ] Convert hexadecimal to binary
- [ ] Identify the 8 hextets in an IPv6 address
- [ ] Shorten IPv6 addresses
- [ ] Expand shortened IPv6 addresses
- [ ] Explain why `::` can only be used once
- [ ] Calculate IPv6 prefixes
- [ ] Understand `/48`, `/56`, `/64` and other prefix lengths
- [ ] Configure IPv6 addresses on Cisco routers
- [ ] Enable IPv6 routing with `ipv6 unicast-routing`
- [ ] Configure IPv6 using EUI-64
- [ ] Perform Modified EUI-64 conversion
- [ ] Explain why the U/L bit is inverted
- [ ] Identify Global Unicast addresses
- [ ] Identify Unique Local addresses
- [ ] Identify Link-Local addresses
- [ ] Explain why IPv6 does not use broadcast
- [ ] Identify IPv6 multicast addresses
- [ ] Understand multicast scopes
- [ ] Remember `FF02::1` — All Nodes
- [ ] Remember `FF02::2` — All Routers
- [ ] Explain Anycast
- [ ] Configure an Anycast address
- [ ] Identify `::/128` — Unspecified
- [ ] Identify `::1/128` — Loopback
- [ ] Identify `::/0` — IPv6 Default Route
- [ ] Verify IPv6 configuration using Cisco IOS commands

---

# Final IPv6 Exam Memory

```text
IPv6 = 128 bits

8 Hextets
↓
Each Hextet = 16 bits

Hexadecimal
↓
0-9 + A-F

Shortening
↓
Remove leading zeros
↓
Use :: for consecutive zero hextets
↓
:: only once

Common /64
↓
64-bit Prefix
+
64-bit Interface ID

Modified EUI-64
↓
48-bit MAC
↓
Split
↓
Insert FFFE
↓
Invert U/L bit
↓
64-bit IID

Global Unicast
↓
2000::/3

Unique Local
↓
FC00::/7
↓
Commonly FD...

Link-Local
↓
FE80::/10

Multicast
↓
FF00::/8

All Nodes
↓
FF02::1

All Routers
↓
FF02::2

Unspecified
↓
::/128

Loopback
↓
::1/128

Default Route
↓
::/0

IPv6 Routing
↓
ipv6 unicast-routing
```

---

# End of IPv6 Notes
