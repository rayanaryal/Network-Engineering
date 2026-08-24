# Interfaces and Cables

> Notes covering Ethernet, network protocols and standards, bits and bytes, Ethernet cabling, UTP cables, fibre-optic cabling, cable standards, Auto MDI-X, and key quiz concepts.

---

# 1. Ethernet

## 1.1 What Is Ethernet?

**Ethernet** is a collection of network protocols and standards.

For this topic, the main focus is on the **types of cabling defined by Ethernet standards**.

Ethernet standards define how networking technologies should operate and communicate consistently.

A major purpose of networking protocols and standards is to provide a common way for networking devices and technologies to communicate.

---

# 2. Network Protocols and Standards

Networking devices need agreed rules and standards to communicate.

Protocols and standards define things such as:

* How devices communicate
* How information is transmitted
* How devices interpret transmitted information
* Physical characteristics of network connections
* Transmission speeds
* Cable types and limitations

Standards allow networking equipment from different manufacturers to work together.

For example, Ethernet standards define specific cable technologies and speeds.

---

# 3. Bits and Bytes

Computers transmit data using **bits**.

A bit can have one of two values:

```text
0
1
```

### 1 Byte

```text
1 byte = 8 bits
```

Example:

```text
01100111
```

The example above contains 8 bits, therefore it represents one byte.

---

# 4. How Bits Are Transmitted

Data is transmitted **one bit at a time** across the physical connection.

A network device does not physically send an entire byte simultaneously across the cable.

Instead, the bits are transmitted sequentially.

Conceptually:

```text
Byte
01100111
   ↓
Bits
0 → 1 → 1 → 0 → 0 → 1 → 1 → 1
```

The neighboring device receives the transmitted bits and reconstructs the data.

---

# 5. Network Speed

Network speed is measured in:

> **bits per second**

Common units include:

```text
Kbps
Mbps
Gbps
Tbps
```

The important point is that networking speeds are normally expressed in **bits per second**, not bytes per second.

---

## 5.1 Common Bit Units

| Unit           |                  Value |
| -------------- | ---------------------: |
| 1 kilobit (Kb) |             1,000 bits |
| 1 megabit (Mb) |         1,000,000 bits |
| 1 gigabit (Gb) |     1,000,000,000 bits |
| 1 terabit (Tb) | 1,000,000,000,000 bits |

Larger units continue using powers of 1,000.

---

# 6. Ethernet Standards

Ethernet standards are defined by the:

> **IEEE 802.3 standard**

IEEE stands for:

> **Institute of Electrical and Electronics Engineers**

The Ethernet standard was defined in **1983**.

The IEEE 802.3 family contains different Ethernet standards for different speeds and physical technologies.

---

# 7. Ethernet Standards — Copper

The important copper Ethernet standards covered in this topic are:

| Ethernet                | IEEE Standard | Informal Name | Maximum Length |
| ----------------------- | ------------- | ------------- | -------------: |
| 10 Mbps Ethernet        | 802.3i        | 10BASE-T      |          100 m |
| 100 Mbps Fast Ethernet  | 802.3u        | 100BASE-T     |          100 m |
| 1 Gbps Gigabit Ethernet | 802.3ab       | 1000BASE-T    |          100 m |
| 10 Gbps 10 Gig Ethernet | 802.3an       | 10GBASE-T     |          100 m |

---

# 8. Understanding Ethernet Names

Ethernet names contain useful information.

For example:

```text
1000BASE-T
```

can be broken down into:

```text
1000
  ↓
Speed

BASE
  ↓
Baseband signalling

T
  ↓
Twisted pair
```

### BASE

**BASE** refers to:

> Baseband signalling

### T

**T** refers to:

> Twisted pair

Therefore:

```text
1000BASE-T
```

means a 1000 Mbps Ethernet technology using baseband signalling over twisted-pair cabling.

---

# 9. UTP Cables

UTP stands for:

> **Unshielded Twisted Pair**

UTP is one of the most common types of copper Ethernet cabling.

The wires are twisted into pairs.

The twisting helps protect the signal from:

> **EMI — Electromagnetic Interference**

---

# 10. UTP Cable Structure

A UTP Ethernet cable contains multiple pairs of copper wires.

Each pair consists of two wires twisted together.

The twisting helps reduce interference between the wires and from external electromagnetic sources.

---

# 11. Number of Wire Pairs

Different Ethernet standards use different numbers of wire pairs.

### 10BASE-T

Uses:

```text
2 pairs
4 wires
```

### 100BASE-T

Uses:

```text
2 pairs
4 wires
```

### 1000BASE-T

Uses:

```text
4 pairs
8 wires
```

### 10GBASE-T

Uses:

```text
4 pairs
8 wires
```

### Quick memory

```text
10 / 100 Mbps
     ↓
2 pairs

1000 / 10G
     ↓
4 pairs
```

---

# 12. Full-Duplex Ethernet

For 10BASE-T and 100BASE-T, separate wire pairs are used for transmitting and receiving.

This allows:

> **Full-duplex communication**

A device can transmit and receive at the same time.

Conceptually:

```text
Device A                         Device B

Transmit  ───────────────────→  Receive

Receive   ←───────────────────  Transmit
```

This allows simultaneous two-way communication.

---

# 13. RJ45 Ethernet Connections

UTP Ethernet cables use **RJ45 connectors**.

The connector contains 8 pins:

```text
1  2  3  4  5  6  7  8
```

For traditional 10/100 Mbps Ethernet, the important transmit and receive pins are:

```text
Pins 1 and 2
Pins 3 and 6
```

The device's transmit and receive pin assignments determine whether a straight-through or crossover cable is required in traditional Ethernet connections.

---

# 14. Straight-Through Cable

In a **straight-through cable**, the same pins connect to the same pins.

Conceptually:

```text
1 ───────── 1
2 ───────── 2
3 ───────── 3
6 ───────── 6
```

The transmit pair on one side connects to the corresponding receive/transmit arrangement on the other side depending on the device type.

Straight-through cabling is traditionally used when connecting devices with different transmit/receive pin assignments.

Examples include:

```text
PC → Switch
Router → Switch
```

---

# 15. Crossover Cable

A **crossover cable** crosses the transmit and receive pairs.

Conceptually:

```text
1 ───────── 3
2 ───────── 6

3 ───────── 1
6 ───────── 2
```

This allows two devices that use the same transmit and receive pin assignments to communicate.

A traditional example is:

```text
Router → Router
```

where both routers transmit on the same pins.

Without the crossover, the transmit pins on one router would connect to the transmit pins on the other router.

---

# 16. Traditional Cable Selection

The source material identifies the following traditional relationships:

| Connection      | Traditional Cable |
| --------------- | ----------------- |
| PC → Switch     | Straight-through  |
| Router → Switch | Straight-through  |
| Router → Router | Crossover         |
| PC → PC         | Crossover         |
| Switch → Switch | Crossover         |

The key concept is not simply memorising the cable type.

Instead, understand:

> **The transmit pair on one device must connect to the receive pair on the other device.**

---

# 17. Auto MDI-X

Modern Ethernet interfaces can use:

> **Auto MDI-X**

Auto MDI-X allows a device to automatically determine which RJ45 pin pairs should be used for transmitting and receiving.

This means the device can automatically adjust its transmit/receive configuration.

As a result, devices with Auto MDI-X can generally operate normally regardless of whether a straight-through or crossover cable is used.

### Key idea

> **Auto MDI-X automatically adjusts the transmit and receive pin configuration.**

---

# 18. Why Auto MDI-X Matters

Consider two identical switches.

Traditionally:

```text
Switch → Switch
```

would require a crossover cable.

However, if both switches support Auto MDI-X:

```text
Switch → Switch
       ↓
Straight-through cable
       ↓
Auto MDI-X
       ↓
Normal operation
```

The devices automatically adjust their transmit and receive pin usage.

This is why modern Ethernet networks are much less dependent on manually selecting straight-through versus crossover cables.

---

# 19. Fibre-Optic Connections

Fibre-optic cabling transmits data using **light** rather than electrical signals.

Fibre is commonly used when:

* Longer distances are required
* Higher-performance connections are required
* Resistance to electromagnetic interference is important

Fibre connections commonly use **SFP transceivers**.

---

# 20. SFP Transceiver

SFP stands for:

> **Small Form-Factor Pluggable**

An SFP is a removable transceiver module used with compatible networking equipment.

The SFP provides the interface between the networking device and the physical fibre connection.

---

# 21. Fibre-Optic Cable Structure

A fibre-optic cable contains several layers.

The source identifies four important parts:

```text
1. Fiberglass core
2. Cladding
3. Protective buffer
4. Outer jacket
```

### 1. Fiberglass Core

The core is the central part of the fibre.

Light travels through the core.

### 2. Cladding

The cladding surrounds the core.

It reflects light back into the core.

### 3. Protective Buffer

The buffer provides additional physical protection around the fibre.

### 4. Outer Jacket

The outer jacket protects the cable as a whole.

---

# 22. Single-Mode Fibre

Single-mode fibre has a **narrower core** than multimode fibre.

The source describes single-mode fibre as allowing light to enter at a single angle, or mode.

It uses:

> **Laser-based SFP transmitters**

### Characteristics

* Narrower core
* Single mode
* Laser-based transmission
* Longer maximum cable distances
* More expensive than multimode fibre

---

# 23. Multimode Fibre

Multimode fibre has a **wider core** than single-mode fibre.

The wider core allows multiple angles, or modes, of light to enter the fibre.

It uses:

> **LED-based SFP transmitters**

### Characteristics

* Wider core
* Multiple modes of light
* LED-based SFP transmitters
* Longer distances than UTP
* Shorter distances than single-mode fibre
* Cheaper than single-mode fibre

---

# 24. Single-Mode vs Multimode

| Feature     | Multimode       | Single-mode           |
| ----------- | --------------- | --------------------- |
| Core        | Wider           | Narrower              |
| Light modes | Multiple        | Single                |
| Transmitter | LED-based       | Laser-based           |
| Distance    | Longer than UTP | Longer than multimode |
| Cost        | Cheaper         | More expensive        |

### Easy mental model

```text
Multimode
   ↓
Wider core
   ↓
Multiple light modes
   ↓
Shorter fibre distances
   ↓
Cheaper

Single-mode
   ↓
Narrower core
   ↓
Single light mode
   ↓
Longer distances
   ↓
More expensive
```

---

# 25. Fibre-Optic Standards

Important fibre Ethernet standards covered in the material include:

| Informal Name | IEEE Standard |   Speed | Cable Type               |     Maximum Length |
| ------------- | ------------- | ------: | ------------------------ | -----------------: |
| 1000BASE-LX   | 802.3z        |  1 Gbps | Multimode or Single-mode | 550 m MM / 5 km SM |
| 10GBASE-SR    | 802.3ae       | 10 Gbps | Multimode                |              400 m |
| 10GBASE-LR    | 802.3ae       | 10 Gbps | Single-mode              |              10 km |
| 10GBASE-ER    | 802.3ae       | 10 Gbps | Single-mode              |              30 km |

---

# 26. UTP vs Fibre-Optic

| Feature                 | UTP                                    | Fibre-Optic                               |
| ----------------------- | -------------------------------------- | ----------------------------------------- |
| Cost                    | Lower                                  | Higher                                    |
| Maximum distance        | Shorter, approximately 100 m           | Longer                                    |
| EMI                     | Can be vulnerable                      | Not vulnerable                            |
| Connector/interface     | RJ45                                   | SFP/transceiver                           |
| Physical medium         | Copper                                 | Fibre/light                               |
| Security characteristic | Emits a faint signal outside the cable | Does not emit a signal outside the cable  |
| SFP cost                | Not applicable to standard RJ45 UTP    | SFP ports/transceivers are more expensive |

---

# 27. Electromagnetic Interference

UTP cables can be vulnerable to:

> **EMI — Electromagnetic Interference**

Fibre-optic cables do not have the same vulnerability because they transmit information using light rather than electrical signals.

Therefore:

```text
UTP
 ↓
Electrical signal
 ↓
Can be affected by EMI

Fibre
 ↓
Light
 ↓
No vulnerability to EMI
```

---

# 28. Fibre Security Consideration

The source also identifies a security difference.

UTP cables emit a faint signal outside the cable, which means the signal could potentially be copied.

Fibre-optic cables do not emit a signal outside the cable in the same way.

Therefore, the source identifies fibre as having an advantage in this particular physical-security characteristic.

---

# 29. Choosing Between UTP and Fibre

### Use UTP when:

* The distance is relatively short
* Lower cost is important
* Connecting end hosts to switches
* Standard RJ45 connections are appropriate

Typical example:

```text
PC ─── UTP ─── Switch
```

### Use multimode fibre when:

* A longer distance than UTP is required
* Cost should be lower than single-mode fibre
* The required distance fits within multimode limits

### Use single-mode fibre when:

* Very long distances are required
* The connection exceeds multimode capability
* Longer fibre links are required despite higher cost

---

# 30. Important Cable Decision Examples

## Example 1 — Same Office Floor

A company needs to connect many end hosts to a switch in a wiring cabinet on the same office floor.

Best choice:

> **UTP**

Reason:

Switches commonly provide many RJ45 ports for end hosts, and end hosts commonly have RJ45 network interfaces.

---

## Example 2 — 150 Metres Between Buildings

A company needs to connect switches in two buildings approximately 150 metres apart and wants to keep costs down.

Best choice from the quiz:

> **Multimode fibre**

Reason:

The distance is beyond the typical 100 m UTP limit, while multimode fibre provides longer cable distances at lower cost than single-mode fibre.

---

## Example 3 — 3 Kilometres Between Offices

A company needs to connect two offices approximately 3 km apart and wants to keep costs down.

Best choice:

> **Single-mode fibre**

Reason:

UTP cannot cover the required distance, and the distance exceeds the multimode option presented in the material.

---

# 31. Key Quiz Questions

## Question 1

### Scenario

Two old routers are connected together with a UTP cable, but data is not successfully sent and received.

What could be the problem?

**Answer:**

> They are connected with a straight-through cable.

A crossover cable would likely fix the issue.

Why?

Both routers transmit data on the same pins:

```text
1 and 2
```

Therefore, the transmit pins on one router need to connect to the receive pins on the other router:

```text
Router A                    Router B

TX 1,2 ────────╲  ╱────── RX 3,6
RX 3,6 ────────╱  ╲────── TX 1,2
```

Modern devices with Auto MDI-X do not have this same limitation.

---

# 32. Quiz Question 2

### Scenario

Two switches are located in separate buildings approximately 150 metres apart.

The company wants to keep costs down.

Options:

```text
A. UTP
B. Single-mode fibre
C. Multimode fibre
```

**Answer:**

> **Multimode fibre**

The typical UTP distance is approximately 100 metres, so UTP is insufficient for the 150 metre connection.

---

# 33. Quiz Question 3

### Scenario

Two offices are approximately 3 kilometres apart.

The company wants to keep costs down.

Options:

```text
A. UTP
B. Single-mode fibre
C. Multimode fibre
```

**Answer:**

> **Single-mode fibre**

The required distance is beyond UTP capability and exceeds the multimode distance considered in the question.

---

# 34. Quiz Question 4

### Scenario

A switch has:

```text
10/100/1000BASE-T ports
Ports are Auto-MDI-X
```

You connect it to an identical switch using a straight-through cable.

What happens?

Options:

```text
A. They operate normally.
B. They operate at a reduced speed.
C. They cannot communicate.
```

**Answer:**

> **A. They operate normally.**

Because the ports support **Auto MDI-X**, the devices automatically adjust their transmit and receive pin configuration.

---

# 35. Quiz Question 5

### Scenario

A company needs to connect many end hosts to a switch located in a wiring cabinet on the same office floor.

Options:

```text
A. UTP
B. Single-mode fibre
C. Multimode fibre
```

**Answer:**

> **A. UTP**

UTP is the standard choice for wired connections to switches in this scenario.

Switches commonly have many RJ45 ports for end-host connections, and end hosts commonly have RJ45 ports on their network interface cards.

---

# 36. Flashcard Revision

The source material also includes a flashcard-style quiz section.

Important answers to remember:

### 10GBASE-LR maximum cable length

```text
10 km
```

### FastEthernet router receive pins

```text
3 and 6
```

### 10BASE-T wire pairs

```text
2 pairs
```

### IEEE standard for 100 Mbps Ethernet

```text
802.3u
```

### IEEE standard for 1 Gbps Gigabit Ethernet

```text
802.3ab
```

### IEEE standard for 10 Gbps 10GBASE-T

```text
802.3an
```

### IEEE standard associated with 10GBASE-SR/LR/ER

```text
802.3ae
```

### Feature that automatically adjusts RJ45 transmit/receive pin pairs

```text
Auto MDI-X
```

---

# 37. Ethernet Standard Memory Table

A useful revision table from the material:

|    Speed | Technology | IEEE    |
| -------: | ---------- | ------- |
|  10 Mbps | 10BASE-T   | 802.3i  |
| 100 Mbps | 100BASE-T  | 802.3u  |
|   1 Gbps | 1000BASE-T | 802.3ab |
|  10 Gbps | 10GBASE-T  | 802.3an |

### Memory sequence

```text
10
100
1000
10G
```

Corresponding IEEE standards:

```text
802.3i
802.3u
802.3ab
802.3an
```

The source also includes the memory trick:

> **I You to A(BN)**

Use it as a quick mnemonic for remembering the Ethernet standards sequence.

---

# 38. Fibre Standard Memory

Important fibre technologies:

```text
1000BASE-LX
        ↓
1 Gbps
        ↓
MM or SM

10GBASE-SR
        ↓
10 Gbps
        ↓
Multimode
        ↓
400 m

10GBASE-LR
        ↓
10 Gbps
        ↓
Single-mode
        ↓
10 km

10GBASE-ER
        ↓
10 Gbps
        ↓
Single-mode
        ↓
30 km
```

---

# 39. Most Important Concepts

For practical networking and CCNA study, the most important concepts from this topic are:

### Ethernet

* Ethernet is a collection of network protocols and standards.
* Ethernet standards are defined by IEEE 802.3.

### Bits

* Network data is transmitted as bits.
* `1 byte = 8 bits`.
* Network speeds are measured in bits per second.

### Copper Ethernet

* UTP means Unshielded Twisted Pair.
* UTP uses twisted copper wire pairs.
* Twisting helps protect against EMI.
* 10BASE-T and 100BASE-T use 2 pairs.
* 1000BASE-T and 10GBASE-T use 4 pairs.
* RJ45 connectors are used with UTP Ethernet.

### Cable types

* Straight-through cables traditionally connect devices with different transmit/receive pin arrangements.
* Crossover cables traditionally connect similar device types.
* Auto MDI-X automatically adjusts transmit/receive pin assignments.

### Fibre

* Fibre uses light instead of electrical signalling.
* Fibre has a core, cladding, buffer and outer jacket.
* Multimode has a wider core and multiple modes.
* Single-mode has a narrower core and a single mode.
* Single-mode supports longer distances but costs more.
* Multimode is cheaper but supports shorter distances than single-mode.
* Fibre is not vulnerable to EMI.

---

# 40. Final Quick-Revision Sheet

```text
ETHERNET
│
├── IEEE 802.3
│
├── Bits
│   └── 1 byte = 8 bits
│
├── Speed
│   ├── Kbps
│   ├── Mbps
│   ├── Gbps
│   └── Tbps
│
├── UTP
│   ├── Unshielded Twisted Pair
│   ├── RJ45
│   ├── 10BASE-T → 2 pairs
│   ├── 100BASE-T → 2 pairs
│   ├── 1000BASE-T → 4 pairs
│   └── 10GBASE-T → 4 pairs
│
├── Cable types
│   ├── Straight-through
│   ├── Crossover
│   └── Auto MDI-X
│
└── Fibre
    ├── Multimode
    │   ├── Wider core
    │   ├── Multiple modes
    │   ├── LED-based SFP
    │   └── Cheaper
    │
    └── Single-mode
        ├── Narrower core
        ├── Single mode
        ├── Laser-based SFP
        ├── Longer distance
        └── More expensive
```

---

# 41. Numbers to Memorise

| Concept                                          | Number / Answer |
| ------------------------------------------------ | --------------- |
| Bits in 1 byte                                   | **8**           |
| 10BASE-T speed                                   | **10 Mbps**     |
| 100BASE-T speed                                  | **100 Mbps**    |
| 1000BASE-T speed                                 | **1 Gbps**      |
| 10GBASE-T speed                                  | **10 Gbps**     |
| Typical copper Ethernet maximum in this material | **100 m**       |
| 10BASE-T pairs                                   | **2**           |
| 100BASE-T pairs                                  | **2**           |
| 1000BASE-T pairs                                 | **4**           |
| 10GBASE-T pairs                                  | **4**           |
| 10GBASE-LR maximum                               | **10 km**       |
| 10GBASE-ER maximum                               | **30 km**       |
| 10GBASE-SR maximum                               | **400 m**       |
| 1000BASE-LX MM maximum                           | **550 m**       |
| 1000BASE-LX SM maximum                           | **5 km**        |
| FastEthernet router receive pins                 | **3 and 6**     |
| Auto-adjustment feature                          | **Auto MDI-X**  |

---

# 42. Practical Troubleshooting Connection

These concepts connect directly to Cisco network troubleshooting.

When a link is not working, think about:

```text
Physical Layer
      ↓
Is the cable correct?
      ↓
Is the interface physically up?
      ↓
Is the correct cable type being used?
      ↓
Are the interfaces compatible?
      ↓
Is Auto MDI-X available?
      ↓
Is the required distance within the cable's limit?
      ↓
Could EMI be affecting copper?
      ↓
Would fibre be more appropriate?
```

Then move upward into:

```text
Layer 2
   ↓
VLAN / switching / STP
   ↓
Layer 3
   ↓
IP addressing / routing
```

Understanding the physical medium first prevents higher-layer troubleshooting from being performed on a link that is physically unsuitable.

---

# 43. Final Takeaways

The biggest lessons from this topic are:

1. **Ethernet is a collection of networking protocols and standards.**
2. **IEEE 802.3 defines Ethernet standards.**
3. Network data is transmitted as **bits**.
4. **8 bits = 1 byte**.
5. Network speed is measured in **bits per second**.
6. UTP means **Unshielded Twisted Pair**.
7. Twisted pairs help reduce the effects of **EMI**.
8. **10BASE-T and 100BASE-T use 2 pairs**.
9. **1000BASE-T and 10GBASE-T use 4 pairs**.
10. Traditional Ethernet cable selection depends on the transmit/receive pin arrangement.
11. **Auto MDI-X** allows compatible devices to automatically adjust transmit/receive pairs.
12. Fibre-optic cabling uses **light** instead of electrical signals.
13. Fibre consists of a **core, cladding, protective buffer and outer jacket**.
14. **Multimode** has a wider core and supports multiple light modes.
15. **Single-mode** has a narrower core and supports a single mode.
16. Single-mode generally supports longer distances but is more expensive.
17. Fibre is not vulnerable to EMI in the same way copper UTP is.
18. **10GBASE-LR supports up to 10 km** in the material.
19. Cable selection should consider **speed, distance, cost, EMI and physical interface requirements**.
20. Understanding cables and interfaces is the foundation for troubleshooting higher-level networking problems.

> **Before troubleshooting VLANs, STP, routing or DHCP, always make sure the physical connection and interface technology make sense first.**
