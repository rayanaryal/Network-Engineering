# OSI Model & TCP/IP Suite

> Networking models provide a structured way to categorize networking protocols and standards.

---

## 1. What Is a Networking Model?

Both **OSI** and **TCP/IP** are networking models.

A networking model categorizes and provides a structure for:

* Networking protocols
* Networking standards
* Different functions involved in network communication

Without standardization, different systems and networking technologies would have difficulty communicating consistently.

A networking model provides a common structure that helps engineers understand how networking functions are organized.

---

# 2. OSI Model

## 2.1 What Is the OSI Model?

**OSI** stands for:

> **Open Systems Interconnection**

The OSI model is a **conceptual model** that categorizes and standardizes the different functions involved in network communication.

It was created by the:

> **International Organization for Standardization (ISO)**

The OSI model divides networking functions into **7 layers**.

### The 7 OSI Layers

| Layer | Name         | Main Function                                    |
| ----: | ------------ | ------------------------------------------------ |
|     7 | Application  | Network services closest to the end user         |
|     6 | Presentation | Data translation and formatting                  |
|     5 | Session      | Establishes, manages and terminates sessions     |
|     4 | Transport    | Host-to-host communication and segmentation      |
|     3 | Network      | Logical addressing and path selection            |
|     2 | Data Link    | Node-to-node connectivity and Layer 2 addressing |
|     1 | Physical     | Transmission of bits over the physical medium    |

The layers work together to make network communication possible.

---

# 3. OSI Layer 7 — Application Layer

The **Application Layer** is the layer closest to the end user.

It interacts with software applications such as:

* Web browsers
* Other network applications

Examples of Layer 7 protocols include:

* **HTTP**
* **HTTPS**

### Functions of the Application Layer

The source identifies functions including:

* Identifying communication partners
* Synchronizing communication
* Providing network-related functions to applications

The Application Layer is where network applications interact with the networking model.

---

# 4. OSI Layer 6 — Presentation Layer

The **Presentation Layer** is responsible for translating data into an appropriate format.

Data at the Application Layer is in an application-specific format.

Before data is sent across a network, it may need to be translated into another format.

### Main responsibilities

The Presentation Layer can:

* Translate between application and network formats
* Encrypt data before it is sent
* Decrypt data when it is received
* Translate between different application-layer formats

### Key idea

> **Presentation Layer = data translation and formatting**

---

# 5. OSI Layer 5 — Session Layer

The **Session Layer** controls dialogues, or sessions, between communicating hosts.

It:

* Establishes connections
* Manages connections
* Terminates connections

For example, a session can exist between:

* A local application such as a web browser
* A remote application such as YouTube

### Key idea

> **Session Layer = establishes, manages and terminates communication sessions**

---

# 6. Upper Layers — Layers 7, 6 and 5

The top three layers are commonly referred to as the **Upper Layers**:

```text
Layer 7 — Application
Layer 6 — Presentation
Layer 5 — Session
```

Network engineers do not usually work directly with all of the detailed functions of these upper layers.

Application developers commonly work with these layers when connecting applications over networks.

---

# 7. Encapsulation

When data is sent through the network stack, each layer performs its function and passes the information to the next layer.

This process is called:

> **Encapsulation**

During encapsulation, headers are added as data moves down through the OSI layers.

Simplified process:

```text
Application
     ↓
Presentation
     ↓
Session
     ↓
Transport
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

Each layer prepares the information for the layer below it.

---

# 8. Adjacent-Layer Interaction

Encapsulation and de-encapsulation are examples of **Adjacent-Layer Interaction**.

This means that neighboring layers interact with each other as information moves through the protocol stack.

For example:

```text
Application
     ↓
Presentation
     ↓
Session
     ↓
Transport
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

Each layer communicates with the layer immediately above or below it.

---

# 9. Same-Layer Interaction

There is also **Same-Layer Interaction**.

Same-layer interaction allows corresponding layers on communicating systems to perform their respective functions.

For example:

```text
Host A                         Host B

Application  ←────────────→  Application
Presentation ←────────────→  Presentation
Session      ←────────────→  Session
Transport    ←────────────→  Transport
Network      ←────────────→  Network
Data Link    ←────────────→  Data Link
Physical     ←────────────→  Physical
```

The actual data moves down the layers on the sending host, across the network, and then up the layers on the receiving host.

---

# 10. De-encapsulation

The reverse process is called:

> **De-encapsulation**

When the receiving device receives the data, information is processed as it moves upward through the OSI model.

Simplified:

```text
Physical
    ↓
Data Link
    ↓
Network
    ↓
Transport
    ↓
Session
    ↓
Presentation
    ↓
Application
```

During this process, headers added during encapsulation are processed and removed at the appropriate layers.

---

# 11. OSI Layer 4 — Transport Layer

The **Transport Layer** provides communication between end hosts.

Its functions include:

* Host-to-host communication
* Segmenting data
* Reassembling data
* Breaking large pieces of data into smaller segments

If the data being sent is large enough, it can be divided into smaller parts.

Each part receives the appropriate Transport Layer information before being passed to the Network Layer.

### Example

```text
Large Data
    ↓
Segmentation
    ↓
Segment 1
Segment 2
Segment 3
Segment 4
```

The smaller segments can be transmitted more easily across the network.

### Key idea

> **Transport Layer = host-to-host communication + segmentation/reassembly**

---

# 12. OSI Layer 3 — Network Layer

The **Network Layer** provides connectivity between end hosts on different networks.

This means it allows communication beyond the local LAN.

### Main functions

The Network Layer provides:

* **Logical addressing**
* **IP addresses**
* **Path selection**
* Connectivity between different networks

### Router

Routers operate at:

> **Layer 3**

Routers use Layer 3 information to determine where packets should be forwarded.

### Key idea

> **Network Layer = IP addressing + path selection + connectivity between networks**

---

# 13. OSI Layer 2 — Data Link Layer

The **Data Link Layer** provides **node-to-node connectivity and data transfer**.

Examples include:

```text
PC → Switch
Switch → Router
Router → Router
```

The Data Link Layer defines how data is formatted for transmission over a physical medium.

Examples of physical media include:

* Copper UTP cables

### Main functions

The Data Link Layer:

* Provides node-to-node connectivity
* Defines data formatting for transmission
* Detects and possibly corrects Physical Layer errors
* Uses Layer 2 addressing
* Separates Layer 2 addressing from Layer 3 addressing

### Switches

Switches operate at:

> **Layer 2**

### Key idea

> **Data Link Layer = node-to-node communication + Layer 2 addressing**

---

# 14. OSI Layer 1 — Physical Layer

The **Physical Layer** defines the physical characteristics of the medium used to transfer data between devices.

Examples include:

* Voltage levels
* Maximum transmission distances
* Physical connectors
* Cable specifications
* Pin layouts

Digital bits are converted into physical signals.

For wired connections, this involves electrical signals.

For wireless connections, radio signals are used.

### Key idea

> **Physical Layer = physical transmission of bits**

The Physical Layer deals with the actual physical infrastructure used to carry network signals.

---

# 15. OSI Encapsulation Process

As data moves down the OSI model, additional information is added.

Simplified:

```text
Layer 7
Application
     ↓
Data

Layer 6
Presentation
     ↓
Data

Layer 5
Session
     ↓
Data

Layer 4
Transport
     ↓
Segment

Layer 3
Network
     ↓
Packet

Layer 2
Data Link
     ↓
Frame

Layer 1
Physical
     ↓
Bits
```

---

# 16. Protocol Data Units (PDUs)

**PDU** stands for:

> **Protocol Data Unit**

Different layers use different names for the data being processed.

|  OSI Layer | PDU     |
| ---------: | ------- |
| Layers 7–5 | Data    |
|    Layer 4 | Segment |
|    Layer 3 | Packet  |
|    Layer 2 | Frame   |
|    Layer 1 | Bit     |

### Easy sequence

```text
Data
  ↓
Segment
  ↓
Packet
  ↓
Frame
  ↓
Bits
```

This is one of the most important sequences to remember for networking.

---

# 17. OSI Layer Acronym

A common mnemonic for remembering the OSI layers is:

> **Please Do Not Throw Sausage Pizza Away**

From Layer 7 down to Layer 1:

```text
7 — Application
6 — Presentation
5 — Session
4 — Transport
3 — Network
2 — Data Link
1 — Physical
```

Another mnemonic can be remembered from Layer 1 upward:

> **Please Do Not Throw Sausage Pizza Away**

depending on the chosen ordering convention.

The important part is knowing the actual layer names and their functions rather than relying only on the mnemonic.

---

# 18. Important Devices by OSI Layer

From the material:

### Layer 3 — Network

**Router**

Routers use Layer 3 information such as IP addresses and path-selection information.

### Layer 2 — Data Link

**Switch**

Switches operate at Layer 2 and use Layer 2 addressing.

### Layer 1 — Physical

Physical networking components include:

* Cables
* Connectors
* Physical interfaces
* Electrical/radio signaling

---

# 19. OSI Model — Quick Reference

| Layer | Name         | Important Concept                           |
| ----: | ------------ | ------------------------------------------- |
|     7 | Application  | Network applications/services               |
|     6 | Presentation | Translation, encryption/decryption          |
|     5 | Session      | Establish/manage/terminate sessions         |
|     4 | Transport    | Segmentation and host-to-host communication |
|     3 | Network      | IP addressing and routing/path selection    |
|     2 | Data Link    | Frames, Layer 2 addressing, node-to-node    |
|     1 | Physical     | Bits, cables, signals and physical media    |

---

# 20. TCP/IP Suite

The **TCP/IP Suite** is a conceptual model and a set of communication protocols used on the Internet and other networks.

It is called **TCP/IP** because TCP and IP are two foundational protocols within the suite.

TCP/IP was developed by the **United States Department of Defense through DARPA**:

> Defense Advanced Research Projects Agency

The TCP/IP model has a similar structure to the OSI model but uses **fewer layers**.

Unlike the OSI model, which is primarily a conceptual model, the TCP/IP suite is the model associated with the protocols actually used in modern networks.

### Important point

> The OSI model still strongly influences how network engineers think about and describe networks.

---

# 21. TCP/IP Model

The TCP/IP model is commonly represented using four layers:

```text
4 — Application
3 — Transport
2 — Internet
1 — Network Access
```

### TCP/IP Layers

| TCP/IP Layer   | Main Purpose                         |
| -------------- | ------------------------------------ |
| Application    | Application-level network services   |
| Transport      | Host-to-host communication           |
| Internet       | Logical addressing and routing       |
| Network Access | Data Link and Physical communication |

---

# 22. TCP/IP Application Layer

The TCP/IP **Application Layer** covers the functions associated with the upper OSI layers.

It corresponds broadly to:

```text
OSI Layer 7 — Application
OSI Layer 6 — Presentation
OSI Layer 5 — Session
```

The TCP/IP model combines these upper-layer functions into one Application Layer.

---

# 23. TCP/IP Transport Layer

The TCP/IP **Transport Layer** corresponds to the OSI Transport Layer.

Its purpose is host-to-host communication.

The Transport Layer is responsible for transporting data between communicating hosts.

The OSI and TCP/IP models therefore have a strong relationship at this layer.

```text
OSI:
Layer 4 — Transport

TCP/IP:
Transport
```

---

# 24. TCP/IP Internet Layer

The TCP/IP **Internet Layer** corresponds broadly to the OSI Network Layer.

It deals with:

* Logical addressing
* IP
* Routing
* Communication between different networks

The router is primarily associated with this layer because routers make forwarding decisions using Layer 3 information.

```text
OSI Layer 3
     ↓
Network

TCP/IP
     ↓
Internet
```

---

# 25. TCP/IP Network Access Layer

The TCP/IP **Network Access Layer** combines functions associated with the lower OSI layers.

It broadly corresponds to:

```text
OSI Layer 2 — Data Link
OSI Layer 1 — Physical
```

Therefore:

```text
TCP/IP Network Access
        ↓
OSI Data Link
        +
OSI Physical
```

This layer deals with access to the physical network and the transmission of data across the local network medium.

---

# 26. OSI vs TCP/IP

The two models have similar purposes but different structures.

### OSI

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

### TCP/IP

```text
4 Application
3 Transport
2 Internet
1 Network Access
```

### General Mapping

```text
OSI                         TCP/IP

Application ┐
Presentation ├──────────→  Application
Session     ┘

Transport   ─────────────→  Transport

Network     ─────────────→  Internet

Data Link   ┐
Physical    ┘────────────→  Network Access
```

The TCP/IP model therefore combines some of the functions represented by separate OSI layers.

---

# 27. Why Learn Both Models?

The **OSI model** is useful for understanding and discussing networking concepts in a structured way.

The **TCP/IP Suite** represents the protocols and architecture used in modern networks and the Internet.

Therefore, network engineers commonly use the OSI model as a way of thinking about and troubleshooting networking problems while working with TCP/IP protocols in real networks.

---

# 28. Data Flow Through the Models

A simplified data flow can be represented as:

```text
Sending Host
     │
     ▼
Application
     │
     ▼
Transport
     │
     ▼
Network / Internet
     │
     ▼
Data Link / Network Access
     │
     ▼
Physical
     │
     ▼
Network
     │
     ▼
Receiving Host
```

The sender performs **encapsulation** as data moves down the stack.

The receiver performs **de-encapsulation** as data moves up the stack.

```text
Sender                         Receiver

Data                           Data
 ↓                              ↑
Segment                        Segment
 ↓                              ↑
Packet                         Packet
 ↓                              ↑
Frame                          Frame
 ↓                              ↑
Bits  ───── Network ─────────→ Bits
```

---

# 29. Key Networking Terms

## Encapsulation

The process of adding information as data moves down the networking stack.

```text
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Bits
```

## De-encapsulation

The reverse process where the receiving device processes information as it moves up the networking stack.

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Data
```

## Same-Layer Interaction

Interaction between corresponding layers on communicating systems.

## Adjacent-Layer Interaction

Interaction between neighboring layers within the same protocol stack.

## PDU

Protocol Data Unit.

```text
Layer 4 → Segment
Layer 3 → Packet
Layer 2 → Frame
Layer 1 → Bit
```

---

# 30. Practical Cisco Relevance

The OSI model is especially useful when troubleshooting Cisco networks.

For example:

### Layer 1 — Physical

Check:

* Cable
* Interface status
* Physical connectivity

### Layer 2 — Data Link

Check:

* VLAN
* MAC address
* Switching
* STP
* Frames

### Layer 3 — Network

Check:

* IP address
* Subnet mask
* Default gateway
* Routing
* Router interfaces

### Layer 4 — Transport

Think about:

* TCP
* UDP
* Ports
* Segmentation

### Layers 5–7

Think about:

* Sessions
* Data formatting
* Applications
* HTTP/HTTPS and other application protocols

---

# 31. Key Takeaways

The most important concepts from this topic are:

1. **OSI is a 7-layer conceptual networking model.**
2. **TCP/IP is a networking protocol suite and model used in modern networks.**
3. OSI was developed as a standardized conceptual framework by ISO.
4. TCP/IP was developed through DARPA and is associated with the protocols used on the Internet.
5. The OSI layers are:

   * Application
   * Presentation
   * Session
   * Transport
   * Network
   * Data Link
   * Physical
6. The TCP/IP model commonly uses four layers:

   * Application
   * Transport
   * Internet
   * Network Access
7. **Routers operate at Layer 3** in the OSI model.
8. **Switches operate at Layer 2** in the OSI model.
9. Layer 4 can segment and reassemble data.
10. Layer 3 provides logical addressing and path selection.
11. Layer 2 provides node-to-node connectivity and Layer 2 addressing.
12. Layer 1 deals with physical transmission of bits.
13. **Encapsulation** occurs as data moves down the stack.
14. **De-encapsulation** occurs as data moves up the stack.
15. PDUs change names as data moves through the stack:

```text
Data → Segment → Packet → Frame → Bits
```

16. The OSI model remains extremely useful for **network engineering and troubleshooting**, even though TCP/IP is the protocol architecture used in modern networks.

---

# 32. Final Mental Model

When troubleshooting a network, think from the bottom upward:

```text
┌──────────────────────────┐
│ Layer 7 — Application    │  What application?
├──────────────────────────┤
│ Layer 6 — Presentation   │  Is data formatted correctly?
├──────────────────────────┤
│ Layer 5 — Session        │  Is the session established?
├──────────────────────────┤
│ Layer 4 — Transport      │  TCP/UDP? Ports?
├──────────────────────────┤
│ Layer 3 — Network        │  IP? Gateway? Routing?
├──────────────────────────┤
│ Layer 2 — Data Link      │  VLAN? MAC? Switching? STP?
├──────────────────────────┤
│ Layer 1 — Physical       │  Cable? Interface? Signal?
└──────────────────────────┘
```

### The troubleshooting mindset

> **Start with the physical layer, verify Layer 2, verify Layer 3, then move upward toward transport and applications.**

This layered approach prevents guessing and helps isolate the actual location of a network problem.
