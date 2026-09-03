# IPv4 and IPv4 Header

This section contains my study notes on **IPv4 addressing, routing fundamentals, IPv4 address classes, binary conversion, network and broadcast addresses, Cisco interface status, and the IPv4 packet header**.

---

# Part 1 — IPv4 Addressing

## 1. Introduction to Routing

Routing is the process of determining how packets travel from a source network to a destination network.

The **Network Layer (Layer 3)** of the OSI model provides:

- Connectivity between end hosts on different networks
- Logical addressing using IP addresses
- Path selection between source and destination networks

Routers operate primarily at **OSI Layer 3 — Network Layer**.

Example:

    PC1
     |
    SW1
     |
    Router
     |
    SW2
     |
    PC2

If PC1 and PC2 are located on different IP networks, the router provides Layer 3 connectivity between them.

---

# 2. IPv4 Addresses

IPv4 stands for:

**Internet Protocol Version 4**

An IPv4 address:

- Is **32 bits** long
- Contains **4 bytes**
- Is divided into **four 8-bit octets**
- Is normally represented using **dotted-decimal notation**

Example:

    192.168.1.254

Each octet contains 8 bits:

    192       168       1       254
    8 bits    8 bits    8 bits   8 bits

Therefore:

    8 + 8 + 8 + 8 = 32 bits

Binary representation:

    192.168.1.254

    11000000.10101000.00000001.11111110

---

# 3. Decimal and Hexadecimal

## Decimal

Decimal is base 10.

It uses the digits:

    0 1 2 3 4 5 6 7 8 9

Example:

    3294

can be represented using powers of 10:

    3 × 1000
    2 × 100
    9 × 10
    4 × 1

Therefore:

    3000 + 200 + 90 + 4 = 3294

---

## Hexadecimal

Hexadecimal is base 16.

It uses:

    0 1 2 3 4 5 6 7 8 9 A B C D E F

The hexadecimal values are:

    A = 10
    B = 11
    C = 12
    D = 13
    E = 14
    F = 15

Example:

    CDE

can be calculated as:

    C × 256
    D × 16
    E × 1

Since:

    C = 12
    D = 13
    E = 14

Therefore:

    12 × 256 + 13 × 16 + 14
    = 3072 + 208 + 14
    = 3294

---

# 4. Binary — Base 2

Binary is base 2.

It uses only:

    0
    1

An IPv4 octet contains 8 binary bits.

The positional values of an 8-bit binary number are:

    128  64  32  16  8  4  2  1

Example:

    192

Binary:

    11000000

Calculation:

    1 × 128
    1 × 64
    0 × 32
    0 × 16
    0 × 8
    0 × 4
    0 × 2
    0 × 1

Therefore:

    128 + 64 = 192

---

## Example — 168

Binary:

    10101000

Calculation:

    1 × 128
    0 × 64
    1 × 32
    0 × 16
    1 × 8
    0 × 4
    0 × 2
    0 × 1

Therefore:

    128 + 32 + 8 = 168

---

## Example — 254

Binary:

    11111110

Calculation:

    128 + 64 + 32 + 16 + 8 + 4 + 2

    = 254

Therefore:

    254 = 11111110

---

# 5. Binary to Decimal Conversion

To convert binary to decimal, use the positional values:

    128 64 32 16 8 4 2 1

For every bit that is `1`, add the corresponding positional value.

Example:

    11101110

Calculation:

    128 + 64 + 32 + 8 + 4 + 2

    = 238

Another example:

    01110110

Calculation:

    64 + 32 + 16 + 4 + 2

    = 118

---

# 6. Decimal to Binary Conversion

To convert decimal to binary, determine which powers of 2 can be used.

The available values for an IPv4 octet are:

    128 64 32 16 8 4 2 1

Example:

    221

Start with 128:

    221 - 128 = 93

Then 64:

    93 - 64 = 29

Then 16:

    29 - 16 = 13

Then 8:

    13 - 8 = 5

Then 4:

    5 - 4 = 1

Then 1:

    1 - 1 = 0

Therefore:

    221 = 11011101

---

# 7. IPv4 Address Structure

An IPv4 address contains:

- Network portion
- Host portion

The subnet mask/prefix length determines how many bits belong to the network portion and how many belong to the host portion.

Example:

    192.168.1.254/24

The `/24` means:

    24 bits = network portion
    8 bits  = host portion

Binary:

    11000000.10101000.00000001.11111110
    <--------- Network ---------><Host>

---

# 8. IPv4 Address Classes

IPv4 addresses were traditionally divided into five classes.

| Class | First Octet Range | Binary Prefix | Typical Prefix |
|-------|-------------------|---------------|----------------|
| A | 1–126 | 0xxxxxxx | /8 |
| B | 128–191 | 10xxxxxx | /16 |
| C | 192–223 | 110xxxxx | /24 |
| D | 224–239 | 1110xxxx | Multicast |
| E | 240–255 | 1111xxxx | Experimental/Reserved |

Note:

    127.x.x.x

is reserved for loopback addresses.

---

# 9. Class A, B and C Examples

## Class A

Example:

    12.128.251.23/8

Default classful prefix:

    /8

Subnet mask:

    255.0.0.0

---

## Class B

Example:

    154.78.111.32/16

Default classful prefix:

    /16

Subnet mask:

    255.255.0.0

---

## Class C

Example:

    192.168.1.254/24

Default classful prefix:

    /24

Subnet mask:

    255.255.255.0

---

# 10. Classful Address Information

## Class A

Leading bits:

    0

Network bits:

    8

Host bits:

    24

Number of possible networks:

    2^7 = 128

Number of addresses per network:

    2^24 = 16,777,216

---

## Class B

Leading bits:

    10

Network bits:

    16

Host bits:

    16

Number of possible networks:

    2^14 = 16,384

Number of addresses per network:

    2^16 = 65,536

---

## Class C

Leading bits:

    110

Network bits:

    24

Host bits:

    8

Number of possible networks:

    2^21 = 2,097,152

Number of addresses per network:

    2^8 = 256

---

# 11. Subnet Masks

Common classful subnet masks:

| Class | Prefix | Subnet Mask |
|-------|--------|-------------|
| A | /8 | 255.0.0.0 |
| B | /16 | 255.255.0.0 |
| C | /24 | 255.255.255.0 |

Binary representations:

### /8

    11111111.00000000.00000000.00000000

### /16

    11111111.11111111.00000000.00000000

### /24

    11111111.11111111.11111111.00000000

---

# 12. Loopback Addresses

The IPv4 loopback range is:

    127.0.0.0 – 127.255.255.255

The most commonly used loopback address is:

    127.0.0.1

Loopback addresses are used to test the local device's network stack.

For example:

    ping 127.0.0.1

This tests the local TCP/IP stack without requiring communication with another device.

---

# 13. Network Address

The **network address** identifies the network itself.

The host portion of the address is:

    All 0s

Therefore, the network address **cannot be assigned to a host**.

Example:

    192.168.1.0/24

Network address:

    192.168.1.0

Binary host portion:

    00000000

Therefore:

    192.168.1.0

is the network address.

---

# 14. Broadcast Address

The **broadcast address** is used to communicate with all hosts within a subnet.

The host portion is:

    All 1s

The broadcast address **cannot be assigned to a host**.

Example:

    192.168.1.0/24

Broadcast address:

    192.168.1.255

Binary host portion:

    11111111

Therefore:

    192.168.1.255

is the broadcast address.

---

# 15. First and Last Usable Addresses

For a normal IPv4 subnet:

- Network address = host bits all 0
- Broadcast address = host bits all 1
- First usable address = network address + 1
- Last usable address = broadcast address - 1

Example:

    172.16.0.0/16

Network address:

    172.16.0.0

Broadcast address:

    172.16.255.255

First usable address:

    172.16.0.1

Last usable address:

    172.16.255.254

---

# 16. Maximum Number of Hosts

The formula for the maximum number of usable hosts is:

    2^n - 2

where:

    n = number of host bits

The two addresses excluded are:

    Network address
    Broadcast address

---

## Example — /24

A `/24` network has:

    32 - 24 = 8 host bits

Therefore:

    2^8 - 2
    = 256 - 2
    = 254 usable hosts

---

## Example — /16

A `/16` network has:

    32 - 16 = 16 host bits

Therefore:

    2^16 - 2
    = 65,536 - 2
    = 65,534 usable hosts

---

## Example — /8

A `/8` network has:

    32 - 8 = 24 host bits

Therefore:

    2^24 - 2
    = 16,777,216 - 2
    = 16,777,214 usable hosts

---

# 17. IPv4 Address Calculation Examples

## Example 1

Given:

    43.109.23.12/8

Network address:

    43.0.0.0

Maximum hosts:

    16,777,214

Broadcast address:

    43.255.255.255

First usable address:

    43.0.0.1

Last usable address:

    43.255.255.254

---

## Example 2

Given:

    129.221.23.13/16

Network address:

    129.221.0.0

Maximum hosts:

    65,534

Broadcast address:

    129.221.255.255

First usable address:

    129.221.0.1

Last usable address:

    129.221.255.254

---

## Example 3

Given:

    209.211.3.22/24

Network address:

    209.211.3.0

Maximum hosts:

    254

Broadcast address:

    209.211.3.255

First usable address:

    209.211.3.1

Last usable address:

    209.211.3.254

---

# 18. Cisco Router Interface Status

Cisco router interfaces are **administratively down by default**.

This means the interface is disabled with the `shutdown` command until it is enabled.

Example command:

    Router(config)# interface gigabitEthernet0/0
    Router(config-if)# no shutdown

The command:

    no shutdown

enables the interface.

---

## `show ip interface brief`

The following command provides a quick summary of router interface status:

    Router# show ip interface brief

Important columns include:

- Interface
- IP-Address
- Status
- Protocol

Example:

    Interface              IP-Address      Status                Protocol
    GigabitEthernet0/0     unassigned      administratively down  down

`administratively down` means the interface has been manually disabled.

---

# 19. Interface Description

Interface descriptions can be configured to document what an interface connects to.

Example:

    R1(config)# interface g0/0
    R1(config-if)# description ## to SW1 ##

The configured descriptions can be viewed using:

    R1# show interfaces description

This is useful for network documentation and troubleshooting.

---

# Part 2 — IPv4 Header

# 20. IPv4 Packet Structure

An IPv4 packet contains an IPv4 header followed by the Layer 4 Protocol Data Unit.

The IPv4 header contains information required for the packet to be delivered correctly through an IP network.

The main IPv4 header fields covered in this study are:

1. Version
2. Internet Header Length (IHL)
3. DSCP
4. ECN
5. Total Length
6. Identification
7. Flags
8. Fragment Offset
9. Time to Live (TTL)
10. Protocol
11. Header Checksum
12. Source IP Address
13. Destination IP Address
14. Options

---

# 21. IPv4 Header Format

The IPv4 header is normally at least:

    20 bytes

and can be as large as:

    60 bytes

The IPv4 address fields are each:

    32 bits

The IPv4 header contains fields that provide information about:

- Version
- Header length
- Quality of Service
- Congestion notification
- Packet size
- Fragmentation
- Lifetime/hop count
- Encapsulated protocol
- Error checking
- Source address
- Destination address
- Optional information

---

# 22. Version Field

Length:

    4 bits

The Version field identifies which version of IP is being used.

For IPv4:

    Version = 4

Binary:

    0100

For comparison, IPv6 uses:

    Version = 6

Binary:

    0110

Therefore, when analysing an IPv4 packet, the Version field contains:

    0100

---

# 23. Internet Header Length — IHL

Length:

    4 bits

IHL stands for:

**Internet Header Length**

The IHL field identifies the length of the IPv4 header.

The value is measured in:

    4-byte increments

The minimum value is:

    5

Therefore:

    5 × 4 bytes = 20 bytes

The maximum value is:

    15

Therefore:

    15 × 4 bytes = 60 bytes

So:

    Minimum IPv4 header = 20 bytes
    Maximum IPv4 header = 60 bytes

If:

    IHL = 5

then:

    5 × 4 = 20 bytes

If IHL is greater than 5, IPv4 Options are present.

---

# 24. DSCP Field

DSCP stands for:

**Differentiated Services Code Point**

Length:

    6 bits

DSCP is used for:

**QoS — Quality of Service**

It can be used to prioritize traffic, particularly delay-sensitive traffic such as:

- Voice
- Video
- Streaming traffic

The purpose is to help network devices treat different types of traffic according to their requirements.

---

# 25. ECN Field

ECN stands for:

**Explicit Congestion Notification**

Length:

    2 bits

ECN provides an end-to-end mechanism for notifying endpoints about network congestion without necessarily dropping packets.

ECN requires support from:

- Both endpoints
- The underlying network infrastructure

---

# 26. Total Length Field

Length:

    16 bits

The Total Length field indicates the total size of the IPv4 packet.

It includes:

    IPv4 Header + Encapsulated Layer 4 Segment/Data

The value is measured in:

    Bytes

Unlike IHL, Total Length is not measured in 4-byte increments.

Minimum value:

    20 bytes

This represents an IPv4 packet containing only the minimum IPv4 header.

Maximum value:

    65,535 bytes

This is the maximum value possible with a 16-bit field.

Therefore:

    2^16 - 1 = 65,535

---

# 27. Identification Field

Length:

    16 bits

The Identification field is used when IPv4 packets are fragmented.

If a packet is too large to pass through a network link because it exceeds the MTU, it may be fragmented.

All fragments belonging to the same original IPv4 packet contain the same Identification value.

This allows the receiving host to determine which fragments belong to the same original packet.

---

# 28. MTU — Maximum Transmission Unit

MTU stands for:

**Maximum Transmission Unit**

It represents the maximum packet size that can normally be transmitted across a particular link without fragmentation.

A common Ethernet MTU is:

    1500 bytes

If an IPv4 packet is larger than the supported MTU and fragmentation is allowed, the packet can be fragmented.

The receiving host can then reassemble the fragments into the original packet.

---

# 29. Flags Field

Length:

    3 bits

The Flags field controls and identifies IPv4 fragmentation.

The three bits are:

    Bit 0 — Reserved
    Bit 1 — Don't Fragment (DF)
    Bit 2 — More Fragments (MF)

---

## Reserved Bit

Bit 0 is:

    Always 0

It is reserved.

---

## Don't Fragment — DF

The DF bit indicates whether the packet should be fragmented.

If:

    DF = 1

the packet must not be fragmented.

---

## More Fragments — MF

The MF bit indicates whether additional fragments follow.

If:

    MF = 1

there are more fragments after the current fragment.

If:

    MF = 0

the current fragment is the final fragment.

An unfragmented packet also has:

    MF = 0

---

# 30. Fragment Offset Field

Length:

    13 bits

The Fragment Offset field indicates the position of a fragment within the original unfragmented IPv4 packet.

It allows the receiving host to correctly reassemble fragments.

This is important because fragments may arrive:

- At different times
- Through different paths
- Out of order

The Fragment Offset allows the receiving host to place each fragment in its correct position.

---

# 31. IPv4 Fragmentation

When an IPv4 packet is larger than the MTU of the next network link, fragmentation may occur if fragmentation is permitted.

For fragmented packets:

- All fragments have their own IPv4 header
- All fragments belonging to the same original packet have the same Identification value
- Fragment Offset identifies the position of each fragment
- MF indicates whether more fragments follow
- The final fragment has MF = 0

Example concept:

    Original IPv4 Packet
            |
            v
        Fragment 1
        Fragment 2
        Fragment 3
        Fragment 4
            |
            v
    Receiving Host
            |
            v
      Reassembled Packet

---

# 32. Time To Live — TTL

Length:

    8 bits

TTL stands for:

**Time To Live**

TTL is used to prevent packets from travelling indefinitely through routing loops.

In practice, TTL operates as a:

**Hop Count**

Each time an IPv4 packet passes through a router:

    TTL = TTL - 1

When a router receives a packet with TTL reaching zero, the router drops the packet.

Therefore TTL helps prevent infinite routing loops.

---

## Example

Suppose a packet starts with:

    TTL = 64

After passing through one router:

    TTL = 63

After another router:

    TTL = 62

After another router:

    TTL = 61

This continues until the TTL reaches zero.

---

# 33. Protocol Field

Length:

    8 bits

The Protocol field identifies the Layer 4 protocol contained inside the IPv4 packet.

Examples:

| Protocol Number | Protocol |
|-----------------|----------|
| 1 | ICMP |
| 6 | TCP |
| 17 | UDP |
| 89 | OSPF |

Therefore:

    Protocol = 6

means the IPv4 packet contains TCP.

    Protocol = 17

means the IPv4 packet contains UDP.

    Protocol = 1

means the IPv4 packet contains ICMP.

    Protocol = 89

means the IPv4 packet contains OSPF.

---

# 34. Header Checksum

Length:

    16 bits

The Header Checksum is used to check the IPv4 header for errors.

When a router receives an IPv4 packet, it calculates the checksum of the IPv4 header and compares it with the checksum contained in the packet.

If the values do not match, the packet is considered corrupted and can be dropped.

Important:

The checksum applies to the:

    IPv4 Header

not the entire packet payload.

---

# 35. Source IP Address

Length:

    32 bits

The Source IP Address identifies the sender of the IPv4 packet.

Example:

    Source: 192.168.1.1

This means the packet originated from:

    192.168.1.1

---

# 36. Destination IP Address

Length:

    32 bits

The Destination IP Address identifies the intended receiver of the IPv4 packet.

Example:

    Destination: 192.168.1.2

This means the packet is intended for:

    192.168.1.2

---

# 37. Source and Destination Together

Example:

    Source:      192.168.1.1
    Destination: 192.168.1.2

The IPv4 header therefore tells the network:

    Who sent the packet?
            |
            v
    192.168.1.1

    Who should receive the packet?
            |
            v
    192.168.1.2

Routers use the destination IP address when making Layer 3 forwarding decisions.

---

# 38. Options Field

The IPv4 Options field is:

    Variable length

It can occupy:

    0–320 bits

The Options field is rarely used.

The presence of Options is indicated by the IHL field.

If:

    IHL = 5

there are no IPv4 Options.

If:

    IHL > 5

IPv4 Options are present.

---

## IPv4 Option Structure

An IPv4 option can contain fields such as:

| Field | Size | Description |
|-------|------|-------------|
| Copied | 1 bit | Indicates whether the option should be copied into all fragments |
| Option Class | 2 bits | General category of the option |
| Option Number | 5 bits | Specifies the option |
| Option Length | 8 bits | Indicates the size of the entire option |
| Option Data | Variable | Option-specific information |

Option classes include categories such as:

    Control
    Debugging and measurement

Some values are reserved.

---

# 39. IPv4 Header — Quick Reference

| Field | Size | Purpose |
|-------|------|---------|
| Version | 4 bits | Identifies IPv4 or IPv6 version |
| IHL | 4 bits | Identifies IPv4 header length |
| DSCP | 6 bits | QoS and traffic prioritisation |
| ECN | 2 bits | Explicit congestion notification |
| Total Length | 16 bits | Total IPv4 packet size |
| Identification | 16 bits | Identifies fragments belonging to the same packet |
| Flags | 3 bits | Controls fragmentation |
| Fragment Offset | 13 bits | Identifies fragment position |
| TTL | 8 bits | Prevents infinite routing loops |
| Protocol | 8 bits | Identifies encapsulated Layer 4 protocol |
| Header Checksum | 16 bits | Checks IPv4 header for errors |
| Source IP | 32 bits | Sender's IPv4 address |
| Destination IP | 32 bits | Receiver's IPv4 address |
| Options | Variable | Optional IPv4 header information |

---

# 40. Important IPv4 Header Values to Remember

## Version

    IPv4 = 4
    Binary = 0100

---

## IHL

    Minimum = 5
    Minimum header size = 20 bytes

    Maximum = 15
    Maximum header size = 60 bytes

---

## Total Length

    Minimum = 20 bytes
    Maximum = 65,535 bytes

---

## Protocol Numbers

    ICMP = 1
    TCP  = 6
    UDP  = 17
    OSPF = 89

---

## IPv4 Address Size

    32 bits
    4 bytes

---

## Source and Destination Fields

    32 bits each

---

# 41. Wireshark IPv4 Packet Capture

Wireshark can be used to inspect the fields of an IPv4 packet.

Example packet:

    Source:      192.168.1.1
    Destination: 192.168.1.2

Example IPv4 header information:

    Version: 4
    Header Length: 20 bytes
    Total Length: 100
    Identification: 5
    Flags: 0
    Fragment Offset: 0
    Time to Live: 255
    Protocol: ICMP (1)
    Source: 192.168.1.1
    Destination: 192.168.1.2

This allows the theoretical IPv4 header fields to be observed in an actual packet capture.

---

# 42. Reading an IPv4 Packet in Wireshark

When inspecting an IPv4 packet, useful fields to check include:

    Version
    Header Length
    DSCP
    ECN
    Total Length
    Identification
    Flags
    Fragment Offset
    TTL
    Protocol
    Header Checksum
    Source Address
    Destination Address

For example, if Wireshark reports:

    Protocol: ICMP (1)

the IPv4 packet is carrying ICMP.

If Wireshark reports:

    Protocol: TCP (6)

the IPv4 packet is carrying TCP.

If Wireshark reports:

    Protocol: UDP (17)

the IPv4 packet is carrying UDP.

---

# 43. IPv4 Fragmentation in Wireshark

Fragmentation can also be observed in Wireshark.

A fragmented packet may show information such as:

    Fragmented IP protocol
    Fragment Offset
    Identification
    Reassembled in another packet

The Identification value can be used to associate fragments with the same original IPv4 packet.

The Fragment Offset identifies where each fragment belongs.

The final fragment has:

    MF = 0

while preceding fragments have:

    MF = 1

---

# 44. IPv4 Troubleshooting Mindset

When troubleshooting IPv4 connectivity, it is useful to work through the network logically.

A basic approach is:

    Physical connectivity
            ↓
    Interface status
            ↓
    IP address
            ↓
    Subnet mask / prefix
            ↓
    Network address
            ↓
    Default gateway
            ↓
    ARP / Layer 2 resolution
            ↓
    Routing table
            ↓
    Destination network
            ↓
    End-to-end connectivity

Useful Cisco commands include:

    show ip interface brief

    show interfaces description

    show ip route

    show running-config

---

# 45. Key IPv4 Concepts I Learned

The main concepts covered in this study were:

- IPv4 is a 32-bit Layer 3 addressing protocol.
- IPv4 addresses contain four 8-bit octets.
- Binary is fundamental to understanding IPv4 addressing.
- IPv4 addresses contain network and host portions.
- Prefix length determines the network and host portions.
- Network addresses have host bits set to all 0s.
- Broadcast addresses have host bits set to all 1s.
- Network and broadcast addresses cannot normally be assigned to hosts.
- Usable host addresses are between the network and broadcast addresses.
- Maximum usable hosts can be calculated using `2^n - 2`.
- Traditional IPv4 addressing uses Classes A, B, C, D and E.
- 127.0.0.0/8 is used for loopback.
- Routers operate at Layer 3.
- Cisco router interfaces are administratively down by default.
- The IPv4 header contains information required for packet delivery.
- TTL prevents packets from circulating indefinitely.
- The Protocol field identifies the encapsulated Layer 4 protocol.
- Identification, Flags and Fragment Offset are used for fragmentation.
- The Header Checksum is used to detect errors in the IPv4 header.
- Source and Destination IP addresses identify the endpoints of the IPv4 packet.
- IHL determines the length of the IPv4 header.
- DSCP is associated with QoS.
- ECN provides congestion notification.
- Wireshark can be used to inspect IPv4 header fields in real packets.

---

# 46. Important Numbers to Memorise

| Concept | Value |
|---------|-------|
| IPv4 address size | 32 bits |
| IPv4 octets | 4 |
| Bits per octet | 8 |
| IPv4 header minimum | 20 bytes |
| IPv4 header maximum | 60 bytes |
| IHL minimum | 5 |
| IHL maximum | 15 |
| IPv4 maximum packet size | 65,535 bytes |
| IPv4 source address | 32 bits |
| IPv4 destination address | 32 bits |
| Version | 4 |
| ICMP | 1 |
| TCP | 6 |
| UDP | 17 |
| OSPF | 89 |
| IPv4 loopback range | 127.0.0.0/8 |
| Common Ethernet MTU | 1500 bytes |

---

# 47. Quiz Questions

## Question 1

Which bit will be set to `1` on all IPv4 packet fragments except the last fragment?

Answer:

    More Fragments (MF) bit

The MF bit is:

    MF = 1

when additional fragments follow.

The final fragment has:

    MF = 0

---

## Question 2

PC4 has:

    129.221.23.13/16

Find:

    Network address
    Maximum number of hosts
    Broadcast address
    First usable address
    Last usable address

Answer:

    Network address:
    129.221.0.0

    Maximum hosts:
    65,534

    Broadcast:
    129.221.255.255

    First usable:
    129.221.0.1

    Last usable:
    129.221.255.254

---

## Question 3

PC8 has:

    209.211.3.22/24

Find:

    Network address
    Maximum number of hosts
    Broadcast address
    First usable address
    Last usable address

Answer:

    Network address:
    209.211.3.0

    Maximum hosts:
    254

    Broadcast:
    209.211.3.255

    First usable:
    209.211.3.1

    Last usable:
    209.211.3.254

---

# 48. Final Summary

IPv4 provides logical Layer 3 addressing and enables routers to forward packets between different networks.

Understanding IPv4 requires a strong understanding of:

    Binary
    Decimal
    Subnet masks
    Prefix lengths
    Network addresses
    Broadcast addresses
    Host addresses
    Routing
    IPv4 packet structure
    IPv4 header fields

The IPv4 header provides the information required to process and forward IPv4 packets.

The most important fields to understand are:

    Version
    IHL
    DSCP
    ECN
    Total Length
    Identification
    Flags
    Fragment Offset
    TTL
    Protocol
    Header Checksum
    Source IP Address
    Destination IP Address
    Options

A strong understanding of these concepts provides the foundation for more advanced networking topics such as:

    VLSM
    CIDR
    Routing protocols
    NAT
    ACLs
    VLANs
    Inter-VLAN routing
    Network troubleshooting
    Packet analysis
