# IPv4 Subnetting and VLSM

This section documents my understanding and practical application of **IPv4 subnetting, CIDR notation, and Variable Length Subnet Masking (VLSM)**.

Subnetting allows a larger IP network to be divided into smaller logical networks. This helps improve address utilisation, control broadcast domains, and design networks according to actual host requirements.

VLSM extends this concept by allowing different subnet sizes to be created from the same address space.

---

## Topics Covered

- IPv4 address structure
- Network and host portions
- Subnet masks
- CIDR notation
- Network addresses
- Broadcast addresses
- Usable host ranges
- Calculating required host bits
- Calculating subnet sizes
- Fixed Length Subnet Masking (FLSM)
- Variable Length Subnet Masking (VLSM)
- Designing subnets based on host requirements
- VLSM allocation from largest to smallest
- Cisco network addressing
- Subnetting verification
- Hands-on VLSM network design

---

## Why Subnetting Matters

Consider the network:

```text
192.168.1.0/24
```

A `/24` provides 256 total IPv4 addresses.

Rather than using the entire `/24` as one network, subnetting allows the address space to be divided into smaller networks.

For example:

```text
                    192.168.1.0/24
                           |
              +------------+------------+
              |            |            |
              v            v            v
           Subnet A     Subnet B     Subnet C
             Sales          HR       Engineering
```

Each subnet becomes its own Layer 3 network and can be assigned according to the number of hosts required.

> **Key takeaway:** Subnetting is not simply an exam calculation. It is a network design technique used to divide address space efficiently and create appropriate Layer 3 network boundaries.
>
> ---

## IPv4 Address Structure

An IPv4 address contains **32 bits** divided into four groups called **octets**.

For example:

```text
192.168.1.10
```

Each octet contains 8 bits:

```text
192       168       1         10
 |         |        |          |
8 bits    8 bits   8 bits     8 bits

8 + 8 + 8 + 8 = 32 bits
```

In binary:

```text
192.168.1.10

11000000.10101000.00000001.00001010
```

Each bit position in an octet has a decimal value:

```text
128   64   32   16   8   4   2   1
 |     |    |    |   |   |   |   |
2^7   2^6  2^5  2^4 2^3 2^2 2^1 2^0
```

For example, decimal `192` is:

```text
128 + 64 = 192

128 64 32 16 8 4 2 1
 1   1  0  0 0 0 0 0

11000000 = 192
```

Understanding these bit values becomes important when calculating subnet masks and network boundaries.

---

## Network Bits and Host Bits

An IPv4 address contains two logical portions:

```text
[ Network Portion ][ Host Portion ]
```

The **network portion** identifies the subnet.

The **host portion** identifies an individual device within that subnet.

The subnet mask determines where the network portion ends and the host portion begins.

---

## Subnet Masks

Consider this subnet mask:

```text
255.255.255.0
```

In binary:

```text
11111111.11111111.11111111.00000000
```

A binary `1` represents a **network bit**, while a binary `0` represents a **host bit**.

Therefore:

```text
11111111.11111111.11111111.00000000
<--------- 24 ---------><-- 8 -->
       Network Bits      Host Bits
```

This mask can therefore be written using CIDR notation as:

```text
/24
```

---

## CIDR Notation

**CIDR (Classless Inter-Domain Routing)** notation represents the number of network bits in the subnet mask.

For example:

| CIDR | Subnet Mask | Host Bits |
|---|---|---:|
| `/24` | `255.255.255.0` | 8 |
| `/25` | `255.255.255.128` | 7 |
| `/26` | `255.255.255.192` | 6 |
| `/27` | `255.255.255.224` | 5 |
| `/28` | `255.255.255.240` | 4 |
| `/29` | `255.255.255.248` | 3 |
| `/30` | `255.255.255.252` | 2 |

For example, `/27` means:

```text
27 Network Bits
5 Host Bits
```

because:

```text
32 - 27 = 5 host bits
```

The last octet of a `/27` mask is:

```text
11100000
```

Converting it to decimal:

```text
128 + 64 + 32 = 224
```

Therefore:

```text
/27 = 255.255.255.224
```

> **Key takeaway:** A CIDR prefix such as `/27` is not something I need to blindly memorise. It tells me exactly how many of the 32 IPv4 bits belong to the network portion.
>
> ---

## Calculating Hosts in a Subnet

Once the CIDR prefix is known, I can determine how many bits remain for host addressing.

The basic relationship is:

```text
Host Bits = 32 - CIDR Prefix
```

The number of total addresses is:

```text
Total Addresses = 2^Host Bits
```

For traditional IPv4 LAN subnetting, two addresses are normally unavailable for host assignment:

- The **network address**
- The **broadcast address**

Therefore:

```text
Usable Hosts = 2^Host Bits - 2
```

---

## Example: Calculating a /27 Network

Consider:

```text
192.168.1.128/27
```

A `/27` contains:

```text
32 - 27 = 5 host bits
```

Therefore:

```text
2^5 = 32 total addresses
```

For a traditional IPv4 LAN subnet:

```text
32 - 2 = 30 usable host addresses
```

So a `/27` provides:

| Property | Value |
|---|---|
| CIDR Prefix | `/27` |
| Subnet Mask | `255.255.255.224` |
| Host Bits | `5` |
| Total Addresses | `32` |
| Usable Hosts | `30` |

---

## Finding the Block Size

Another useful subnetting technique is calculating the **block size**.

For `/27`:

```text
Subnet Mask = 255.255.255.224
```

The interesting octet is `224`.

```text
256 - 224 = 32
```

Therefore, the subnet boundaries increase in blocks of **32**:

```text
192.168.1.0
192.168.1.32
192.168.1.64
192.168.1.96
192.168.1.128
192.168.1.160
192.168.1.192
192.168.1.224
```

---

## Network, Host Range and Broadcast Address

For:

```text
192.168.1.128/27
```

the next subnet begins at:

```text
192.168.1.160
```

Therefore, the current subnet ends one address before that:

```text
192.168.1.159
```

The complete subnet is:

```text
Network Address:     192.168.1.128
First Usable Host:   192.168.1.129
Last Usable Host:    192.168.1.158
Broadcast Address:   192.168.1.159
Next Network:        192.168.1.160
```

Visually:

```text
192.168.1.128                                    192.168.1.159
      |                                                 |
      v                                                 v
+---------+---------------------------------------+-----------+
| Network |             Usable Hosts              | Broadcast |
+---------+---------------------------------------+-----------+
   .128              .129  →  .158                    .159
```

> **Key takeaway:** Once I know the block size, I can identify the network boundaries. From those boundaries, I can determine the network address, usable host range, and broadcast address.


---

## Choosing a Subnet Based on Host Requirements

In real network design, I may not be given the subnet prefix directly.

Instead, I may be given a requirement such as:

```text
Sales Department requires 25 hosts.
```

I then need to determine the smallest subnet that can support those hosts.

The formula is:

```text
Usable Hosts = 2^h - 2
```

where:

```text
h = number of host bits
```

---

## Example: Sales Requires 25 Hosts

Start testing the number of host bits:

```text
2^4 - 2 = 14 usable hosts
```

14 addresses are not enough for 25 hosts.

Try 5 host bits:

```text
2^5 - 2 = 30 usable hosts
```

30 usable addresses are enough.

Therefore:

```text
Host Bits = 5
```

IPv4 contains 32 bits, so:

```text
32 - 5 = 27 network bits
```

Therefore, Sales requires:

```text
/27
```

which corresponds to:

```text
255.255.255.224
```

So:

```text
25 hosts
   ↓
Need at least 25 usable addresses
   ↓
2^5 - 2 = 30
   ↓
5 host bits
   ↓
32 - 5 = /27
   ↓
255.255.255.224
```

---

## Common Host Capacities

| Prefix | Host Bits | Total Addresses | Usable Hosts |
|---|---:|---:|---:|
| `/25` | 7 | 128 | 126 |
| `/26` | 6 | 64 | 62 |
| `/27` | 5 | 32 | 30 |
| `/28` | 4 | 16 | 14 |
| `/29` | 3 | 8 | 6 |
| `/30` | 2 | 4 | 2 |

This table makes it easier to estimate the required prefix, but understanding the calculation is more important than simply memorising the values.

---

## Choosing the Smallest Suitable Subnet

When designing a subnet, I choose the **smallest subnet that still satisfies the host requirement**.

For example:

```text
Requirement: 25 hosts
```

A `/28` provides:

```text
14 usable hosts ❌
```

A `/27` provides:

```text
30 usable hosts ✅
```

A `/26` provides:

```text
62 usable hosts ✅
```

Although `/26` would work, it allocates significantly more addresses than required.

Therefore:

```text
25 hosts → /27
```

is the more efficient choice.

> **Key takeaway:** In VLSM, I allocate enough address space to satisfy the requirement without unnecessarily consuming addresses that could be used by another subnet.


---

## Variable Length Subnet Masking (VLSM)

**VLSM (Variable Length Subnet Masking)** allows multiple subnet sizes to be created from the same parent network.

Instead of giving every department an identical subnet size, VLSM allows each network to receive an address block based on its actual host requirements.

For example, assume I have:

```text
192.168.1.0/24
```

and the following requirements:

| Network | Host Requirement |
|---|---:|
| Engineering | 100 hosts |
| Sales | 25 hosts |
| HR | 10 hosts |
| Point-to-Point Link | 2 hosts |

Giving every network the same subnet size would waste IPv4 addresses.

With VLSM, I can allocate a different prefix to each network.

---

## VLSM Rule: Allocate Largest Networks First

When designing a VLSM addressing plan, I arrange the requirements from **largest to smallest**.

```text
100 hosts
25 hosts
10 hosts
2 hosts
```

This is important because the largest subnet requires the largest continuous block of addresses.

I then determine the smallest suitable subnet for each requirement.

| Requirement | Calculation | Prefix | Usable Hosts |
|---:|---|---|---:|
| 100 hosts | `2^7 - 2 = 126` | `/25` | 126 |
| 25 hosts | `2^5 - 2 = 30` | `/27` | 30 |
| 10 hosts | `2^4 - 2 = 14` | `/28` | 14 |
| 2 hosts | `2^2 - 2 = 2` | `/30` | 2 |

---

## Step 1 - Engineering Network

Engineering requires:

```text
100 hosts
```

Seven host bits provide:

```text
2^7 - 2 = 126 usable hosts
```

Therefore:

```text
32 - 7 = /25
```

Starting from the beginning of `192.168.1.0/24`:

```text
Network:        192.168.1.0/25
Subnet Mask:    255.255.255.128
First Host:     192.168.1.1
Last Host:      192.168.1.126
Broadcast:      192.168.1.127
```

The next available address is:

```text
192.168.1.128
```

---

## Step 2 - Sales Network

Sales requires:

```text
25 hosts
```

Five host bits provide:

```text
2^5 - 2 = 30 usable hosts
```

Therefore Sales requires `/27`.

Starting from the next available address:

```text
Network:        192.168.1.128/27
Subnet Mask:    255.255.255.224
First Host:     192.168.1.129
Last Host:      192.168.1.158
Broadcast:      192.168.1.159
```

The next available address becomes:

```text
192.168.1.160
```

---

## Step 3 - HR Network

HR requires:

```text
10 hosts
```

Four host bits provide:

```text
2^4 - 2 = 14 usable hosts
```

Therefore HR requires `/28`.

```text
Network:        192.168.1.160/28
Subnet Mask:    255.255.255.240
First Host:     192.168.1.161
Last Host:      192.168.1.174
Broadcast:      192.168.1.175
```

The next available address is:

```text
192.168.1.176
```

---

## Step 4 - Point-to-Point Network

A traditional point-to-point IPv4 subnet requiring two usable addresses can use a `/30`.

```text
2^2 - 2 = 2 usable hosts
```

Using the next available block:

```text
Network:        192.168.1.176/30
Subnet Mask:    255.255.255.252
First Host:     192.168.1.177
Last Host:      192.168.1.178
Broadcast:      192.168.1.179
```

This could be used for a router-to-router connection:

```text
R2                               R4
192.168.1.177/30       192.168.1.178/30
       |                       |
       +-----------------------+
          192.168.1.176/30
```

---

## Final VLSM Addressing Plan

The parent network:

```text
192.168.1.0/24
```

has now been divided into differently sized subnets:

| Purpose | Network | Prefix | Usable Range | Broadcast |
|---|---|---|---|---|
| Engineering | `192.168.1.0` | `/25` | `.1 - .126` | `.127` |
| Sales | `192.168.1.128` | `/27` | `.129 - .158` | `.159` |
| HR | `192.168.1.160` | `/28` | `.161 - .174` | `.175` |
| R2-R4 Link | `192.168.1.176` | `/30` | `.177 - .178` | `.179` |

Visually:

```text
192.168.1.0/24
|
+-- 192.168.1.0/25
|      Engineering
|      .0 - .127
|
+-- 192.168.1.128/27
|      Sales
|      .128 - .159
|
+-- 192.168.1.160/28
|      HR
|      .160 - .175
|
+-- 192.168.1.176/30
       R2-R4 Transit
       .176 - .179
```

Notice that the subnet ranges **never overlap**.

The next unused address after these allocations is:

```text
192.168.1.180
```

That address can then become the starting point for another correctly aligned subnet if additional networks are required.

> **Key takeaway:** My VLSM workflow is: sort host requirements from largest to smallest, determine the smallest suitable prefix, allocate the subnet, identify its broadcast address, and continue from the next available valid network boundary.


---

## Subnetting Mistakes and Troubleshooting

Subnetting mistakes can cause Cisco IOS to reject an IP address even when the subnet mask itself appears correct.

One error I encountered while configuring a `/30` point-to-point network was:

```cisco
Router(config-if)# ip address 192.168.3.3 255.255.255.252
Bad mask /30 for address 192.168.3.3
```

At first, the address `192.168.3.3` may appear to be a valid host address.

However, with a `/30` subnet mask, it is actually a **broadcast address**.

---

## Why 192.168.3.3/30 Is Invalid

A `/30` subnet uses:

```text
255.255.255.252
```

The block size is:

```text
256 - 252 = 4
```

Therefore, `/30` networks increase in blocks of four:

```text
192.168.3.0/30
192.168.3.4/30
192.168.3.8/30
192.168.3.12/30
192.168.3.16/30
...
```

For the first subnet:

```text
192.168.3.0/30
```

the addresses are:

| Address | Purpose |
|---|---|
| `192.168.3.0` | Network address |
| `192.168.3.1` | Usable host |
| `192.168.3.2` | Usable host |
| `192.168.3.3` | Broadcast address |

Therefore:

```text
192.168.3.3/30
```

cannot normally be assigned to a router interface because `.3` identifies the broadcast address of that subnet.

Cisco IOS correctly rejects the configuration:

```text
Bad mask /30 for address 192.168.3.3
```

---

## Correct /30 Configuration

For the network:

```text
192.168.3.0/30
```

the two router interfaces could use:

```text
Router 1 = 192.168.3.1/30
Router 2 = 192.168.3.2/30
```

For example:

```cisco
R1(config)# interface Serial0/1/0
R1(config-if)# ip address 192.168.3.1 255.255.255.252
R1(config-if)# no shutdown
```

And on the other router:

```cisco
R2(config)# interface Serial0/1/0
R2(config-if)# ip address 192.168.3.2 255.255.255.252
R2(config-if)# no shutdown
```

---

## Recognising /30 Networks Quickly

Because `/30` has a block size of four, the network addresses occur at multiples of four:

```text
.0
.4
.8
.12
.16
.20
.24
.28
...
```

For each traditional `/30` subnet:

```text
Network     = First address
Host 1      = Network + 1
Host 2      = Network + 2
Broadcast   = Network + 3
Next subnet = Network + 4
```

Example:

```text
192.168.3.8/30

.8   = Network
.9   = Host
.10  = Host
.11  = Broadcast
.12  = Next network
```

---

## Common Subnetting Mistakes

### Assigning the Network Address to a Host

For:

```text
192.168.1.128/27
```

this address cannot normally be assigned to a host:

```text
192.168.1.128
```

because it identifies the subnet itself.

### Assigning the Broadcast Address

For the same `/27`:

```text
192.168.1.159
```

is the broadcast address and cannot normally be assigned to an interface as a host address.

### Using the Wrong Subnet Mask

Two interfaces may appear to have similar IP addresses but still interpret the network boundaries differently if their subnet masks do not match.

### Creating Overlapping VLSM Subnets

Every VLSM allocation must occupy its own unique address range.

For example:

```text
192.168.1.128/27 = .128 - .159
```

The next subnet cannot begin at `.150` because that address is already inside the Sales subnet.

---

## My Troubleshooting Method

When Cisco rejects an address or connectivity fails, I check:

1. What is the CIDR prefix?
2. How many addresses are in the block?
3. What is the block size?
4. What is the network address?
5. What is the broadcast address?
6. What is the usable host range?
7. Does the proposed IP fall inside that usable range?
8. Does this subnet overlap with another subnet?

> **Lesson learned:** An IP address can look like a normal host address in decimal notation but still represent a network or broadcast address once the subnet mask is applied.


## My VLSM Planning

The following addressing plan was developed while designing my
enterprise Packet Tracer topology.

Starting network:

`192.168.1.0/24`

The subnets were allocated from the largest host requirement to
the smallest.

![My VLSM addressing calculations](images/vlsm-addressing-plan.png)











