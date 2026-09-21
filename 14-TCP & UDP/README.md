# TCP & UDP

This section covers the **Transport Layer (Layer 4)** and the two major Transport Layer protocols:

- **TCP — Transmission Control Protocol**
- **UDP — User Datagram Protocol**

The notes focus on the concepts required for **CCNA exam preparation**, including Layer 4 functions, port numbers, TCP reliability, sequencing, acknowledgement, retransmission, flow control, TCP connection establishment and termination, and the differences between TCP and UDP.

---

# Table of Contents

1. [Functions of Layer 4 (Transport Layer)](#1-functions-of-layer-4-transport-layer)
2. [TCP (Transmission Control Protocol)](#2-tcp-transmission-control-protocol)
3. [TCP Header](#3-tcp-header)
4. [Establishing Connections: Three-Way Handshake](#4-establishing-connections-three-way-handshake)
5. [Terminating Connections: Four-Way Handshake](#5-terminating-connections-four-way-handshake)
6. [TCP: Sequencing / Acknowledgement](#6-tcp-sequencing--acknowledgement)
7. [TCP Retransmission](#7-tcp-retransmission)
8. [TCP Flow Control: Window Size](#8-tcp-flow-control-window-size)
9. [Comparing TCP & UDP with Diagram](#9-comparing-tcp--udp-with-diagram)
10. [Comparing TCP & UDP on Points](#10-comparing-tcp--udp-on-points)
11. [Comparing TCP & UDP in Table](#11-comparing-tcp--udp-in-table)
12. [Port Numbers](#12-port-numbers)

---

# 1. Functions of Layer 4 (Transport Layer)

The **Transport Layer** is Layer 4 of the OSI model.

```text
OSI Model

Layer 7 - Application
Layer 6 - Presentation
Layer 5 - Session
Layer 4 - Transport       ← TCP / UDP
Layer 3 - Network
Layer 2 - Data Link
Layer 1 - Physical
```

The Transport Layer provides transparent transfer of data between end hosts.

TCP and UDP can provide different services to applications.

TCP provides services such as:

- Reliable data transfer
- Error recovery
- Data sequencing
- Flow control

UDP does not provide these TCP-style reliability services.

---

## Layer 4 Addressing — Port Numbers

The Transport Layer also provides **Layer 4 addressing through port numbers**.

> These are **not physical ports/interfaces on switches or routers**.

Port numbers are used to:

- Identify the application-layer protocol/service
- Provide session multiplexing

A simple way to understand this is:

```text
IP Address
    ↓
Identifies the host/interface

Port Number
    ↓
Identifies the application/service
```

For example:

```text
192.168.1.10:443
```

means:

```text
IP Address = 192.168.1.10
Port       = 443
```

Port 443 is commonly associated with HTTPS.

---

## Port Number Ranges

The document uses the IANA port-number ranges:

| Port Range | Type |
|---|---|
| 0–1023 | Well-known ports |
| 1024–49151 | Registered ports |
| 49152–65535 | Ephemeral / Private / Dynamic ports |

### Well-Known Ports

```text
0–1023
```

These are commonly used by standard network services.

### Registered Ports

```text
1024–49151
```

These are registered for specific applications and services.

### Ephemeral / Dynamic Ports

```text
49152–65535
```

These can be dynamically assigned, commonly to client-side connections.

---

## Session Multiplexing

Port numbers allow a host to communicate with multiple applications and sessions at the same time.

For example:

```text
PC
 |
 +---- Web Browser → TCP 443
 |
 +---- SSH Client  → TCP 22
 |
 +---- DNS         → UDP 53
 |
 +---- Email       → TCP port
```

The IP address identifies the host, while the port number helps identify the appropriate application/service.

---

# 2. TCP (Transmission Control Protocol)

TCP stands for:

> **Transmission Control Protocol**

TCP is a **connection-oriented** transport protocol.

Before actually sending data to the destination host, the two hosts communicate to establish a connection.

Once the connection is established, the data exchange begins.

---

## TCP Characteristics

TCP provides:

### Connection-Oriented Communication

A TCP connection is established before normal data exchange begins.

```text
Establish Connection
        ↓
   Exchange Data
        ↓
Terminate Connection
```

---

### Reliable Communication

TCP provides reliable communication.

The destination host acknowledges received TCP segments.

If a segment is not acknowledged, TCP can retransmit it.

```text
Sender
   |
   | Segment
   ↓
Receiver
   |
   | ACK
   ↓
Sender
```

---

### Sequencing

TCP provides sequencing.

Sequence numbers in the TCP header allow the destination host to put segments back into the correct order if they arrive out of order.

```text
Segment 1
Segment 2
Segment 3
```

Even if they arrive as:

```text
Segment 1
Segment 3
Segment 2
```

TCP can use sequence information to correctly organise the data.

---

### Flow Control

TCP provides flow control.

The destination host can tell the source host to increase or decrease the rate at which data is sent.

TCP uses the **Window Size** field for flow control.

---

# 3. TCP Header

The TCP header contains several important fields.

A simplified TCP header:

```text
+-------------------------------+
|       Source Port             |
+-------------------------------+
|     Destination Port          |
+-------------------------------+
|       Sequence Number         |
+-------------------------------+
|    Acknowledgement Number     |
+-------------------------------+
| Data Offset | Flags | Window  |
+-------------------------------+
|          Checksum             |
+-------------------------------+
|       Urgent Pointer          |
+-------------------------------+
|          Options              |
+-------------------------------+
|             Data              |
+-------------------------------+
```

---

## Source Port

The **Source Port** identifies the sending application/service.

---

## Destination Port

The **Destination Port** identifies the application/service on the destination host.

---

## Sequence Number

The **Sequence Number** is used for TCP sequencing and reliable communication.

It allows the destination host to determine the position of data in the TCP communication.

---

## Acknowledgement Number

The **Acknowledgement Number** is used to acknowledge received data.

It indicates the sequence number of the next segment/byte expected.

---

## TCP Flags

TCP contains several flags.

The important flags for understanding connection establishment and termination are:

```text
SYN
ACK
FIN
```

The TCP header also contains other flags such as:

```text
RST
PSH
URG
ECE
CWR
```

For CCNA purposes, pay particular attention to:

```text
SYN → Establish connection

ACK → Acknowledge

FIN → Terminate connection
```

---

## Window Size

The **Window Size** field is used for TCP flow control.

It allows the receiver to indicate how much data can be sent before additional acknowledgement is required.

---

## Checksum

The TCP header contains a checksum used for error detection.

---

## TCP Header and Encapsulation

When application data is passed down the protocol stack, TCP adds its Layer 4 header.

Conceptually:

```text
Application Data
       ↓
+----------------+
| TCP Header     |
+----------------+
| Application    |
| Data           |
+----------------+
       ↓
TCP Segment
```

The segment is then passed to lower layers for further encapsulation.

---

# 4. Establishing Connections: Three-Way Handshake

TCP uses a **Three-Way Handshake** to establish a connection.

The three steps are:

```text
1. SYN
2. SYN + ACK
3. ACK
```

---

## Step 1 — SYN

The client sends a:

```text
SYN
```

This is used to initiate the TCP connection.

```text
PC1                         SRV1
 |                            |
 | -------- SYN ------------> |
 |                            |
```

---

## Step 2 — SYN + ACK

The server responds with:

```text
SYN + ACK
```

The server acknowledges the client's SYN and also sends its own SYN.

```text
PC1                         SRV1
 |                            |
 | -------- SYN ------------> |
 |                            |
 | <------ SYN + ACK -------- |
 |                            |
```

---

## Step 3 — ACK

The client sends:

```text
ACK
```

```text
PC1                         SRV1
 |                            |
 | -------- SYN ------------> |
 |                            |
 | <------ SYN + ACK -------- |
 |                            |
 | -------- ACK ------------> |
 |                            |
```

The TCP connection is now established.

---

## Three-Way Handshake — Easy Memory

Remember:

```text
SYN
 ↓
SYN + ACK
 ↓
ACK
```

Or:

```text
Client → SYN → Server
Client ← SYN-ACK ← Server
Client → ACK → Server
```

After this:

```text
TCP Connection Established
```

---

# 5. Terminating Connections: Four-Way Handshake

This is an important concept.

TCP normally uses a **Four-Way Handshake** to terminate a connection.

The four messages are:

```text
1. FIN
2. ACK
3. FIN
4. ACK
```

The reason four messages are normally used is that TCP is full-duplex.

Each direction of the connection is closed independently.

---

## Four-Way Handshake

```text
PC1                         SRV1
 |                            |
 | -------- FIN ------------> |
 |                            |
 | <--------- ACK ----------- |
 |                            |
 | <--------- FIN ----------- |
 |                            |
 | -------- ACK ------------> |
 |                            |
```

---

## Step 1 — FIN

The client indicates that it has finished sending data:

```text
FIN
```

```text
PC1                         SRV1
 |                            |
 | -------- FIN ------------> |
 |                            |
```

---

## Step 2 — ACK

The server acknowledges the FIN:

```text
ACK
```

```text
PC1                         SRV1
 |                            |
 | -------- FIN ------------> |
 |                            |
 | <--------- ACK ----------- |
 |                            |
```

---

## Step 3 — FIN

The server then sends its own FIN when it has finished sending data in the opposite direction.

```text
PC1                         SRV1
 |                            |
 | -------- FIN ------------> |
 |                            |
 | <--------- ACK ----------- |
 |                            |
 | <--------- FIN ----------- |
 |                            |
```

---

## Step 4 — ACK

The client acknowledges the server's FIN:

```text
ACK
```

```text
PC1                         SRV1
 |                            |
 | -------- FIN ------------> |
 |                            |
 | <--------- ACK ----------- |
 |                            |
 | <--------- FIN ----------- |
 |                            |
 | -------- ACK ------------> |
 |                            |
```

The TCP connection can now be closed.

---

## Three-Way vs Four-Way

This is extremely important to remember:

### Establishing a TCP connection

```text
THREE-WAY HANDSHAKE

SYN
 ↓
SYN + ACK
 ↓
ACK
```

### Terminating a TCP connection

```text
FOUR-WAY HANDSHAKE

FIN
 ↓
ACK
 ↓
FIN
 ↓
ACK
```

### Easy Memory

```text
START TCP
→ SYN
→ SYN-ACK
→ ACK

END TCP
→ FIN
→ ACK
→ FIN
→ ACK
```

---

# 6. TCP: Sequencing / Acknowledgement

TCP uses:

- Sequence numbers
- Acknowledgement numbers

to provide sequencing and reliable communication.

Hosts set a **random initial sequence number** when establishing a TCP connection.

---

## Example from the TCP Sequence Diagram

A simplified example:

```text
PC1                              PC2

Seq: 10
       ------------------------->

                  Seq: 50
                  Ack: 11
       <-------------------------

Seq: 11
Ack: 51
       ------------------------->

                  Seq: 51
                  Ack: 12
       <-------------------------

Seq: 12
Ack: 52
       ------------------------->
```

The numbers above are simplified examples used to understand the concept.

In real networks, sequence numbers are much larger and do not necessarily increase by exactly 1 for every packet.

---

## Sequence Number

The sequence number helps identify the position of the transmitted data.

```text
Seq = 10
Seq = 11
Seq = 12
...
```

---

## Acknowledgement Number

The acknowledgement indicates the sequence number of the next segment/byte the host expects to receive.

For example:

```text
Received:
Seq 10

Next expected:
Ack 11
```

So:

```text
ACK = "I received what I expected up to this point,
       and this is what I expect next."
```

---

## Why Sequencing Is Important

Imagine segments arrive out of order:

```text
Segment 1
Segment 3
Segment 2
```

TCP uses sequence information to put the data back into the correct order.

Therefore:

```text
TCP
 ↓
Sequence Numbers
 ↓
Correct ordering
```

---

# 7. TCP Retransmission

TCP provides reliable communication.

If a TCP segment is lost, TCP can retransmit the missing data.

Consider:

```text
PC1                              SRV1

Seq: 20
       ------------------------->

                  ACK: 21
       <-------------------------

Seq: 21
       -----------X------------->

                 LOST

Seq: 21
       ------------------------->

                  ACK: 22
       <-------------------------
```

The second segment was lost.

TCP retransmits it.

---

## Why Does TCP Retransmit?

TCP expects acknowledgement for transmitted data.

If the expected acknowledgement does not arrive, TCP can determine that data may have been lost and retransmit it.

Simplified:

```text
Data sent
   ↓
Waiting for ACK
   ↓
ACK received?
   |
   +---- YES → Continue
   |
   +---- NO → Retransmit
```

This is one of the mechanisms that makes TCP reliable.

---

# 8. TCP Flow Control: Window Size

Acknowledging every single segment individually would be inefficient.

TCP therefore uses the **Window Size** field.

The TCP header's Window Size field allows more data to be sent before an acknowledgement is required.

---

## Without Windowing

Imagine:

```text
Send segment
      ↓
Wait for ACK
      ↓
Send segment
      ↓
Wait for ACK
```

This can be inefficient.

---

## With a Window

TCP can allow multiple segments to be sent before an acknowledgement is required.

Example:

```text
Seq: 20  -------------------->
Seq: 21  -------------------->
Seq: 22  -------------------->

             <--------------- ACK 23
```

The sender does not necessarily have to wait for an acknowledgement after every individual segment.

---

## Sliding Window

TCP can dynamically adjust the amount of data that can be sent before acknowledgement.

This is called a:

> **Sliding Window**

Simplified:

```text
Seq 20
Seq 21
Seq 22
       ---------------------->

                    ACK 23
       <----------------------
```

As acknowledgements are received, the sending window moves forward.

---

## Important CCNA Point

For the CCNA, understand the **concept** rather than memorising large sequence numbers.

```text
Window Size
     ↓
Flow Control
     ↓
Controls how much data can be sent
before acknowledgement is required
```

---

# UDP (User Datagram Protocol)

UDP stands for:

> **User Datagram Protocol**

UDP is another Layer 4 transport protocol.

Unlike TCP, UDP is **not connection-oriented**.

---

## UDP Characteristics

UDP does not establish a connection with the destination host before sending data.

The data is simply sent.

```text
Sender                         Receiver

   UDP Datagram
       ----------------------->
```

There is no TCP-style three-way handshake.

---

## UDP Does Not Provide TCP-Style Reliable Communication

When UDP is used, acknowledgements are not sent for received datagrams.

If a datagram is lost:

```text
UDP Datagram
      |
      X
    LOST
```

UDP itself does not retransmit it.

The application may implement its own reliability mechanisms if required.

---

## UDP Does Not Provide Sequencing

UDP does not have a sequence-number field like TCP.

Therefore, if UDP datagrams arrive out of order:

```text
Datagram 1
Datagram 3
Datagram 2
```

UDP itself does not provide a TCP-style mechanism to reorder them.

---

## UDP Does Not Provide TCP-Style Flow Control

UDP does not have a mechanism like TCP's Window Size to control the flow of data.

---

## UDP Header

UDP has a much simpler header than TCP.

```text
+-------------------------------+
| Source Port | Destination Port|
+-------------------------------+
| Length       | Checksum        |
+-------------------------------+
|             Data              |
+-------------------------------+
```

The UDP header contains:

```text
Source Port
Destination Port
Length
Checksum
```

The UDP header is **8 bytes**.

---

# 9. Comparing TCP & UDP with Diagram

TCP has a larger header because it provides more functionality.

Simplified TCP header:

```text
+----------------------------------+
| Source Port | Destination Port  |
+----------------------------------+
|        Sequence Number           |
+----------------------------------+
|     Acknowledgement Number       |
+----------------------------------+
| Flags | Window Size              |
+----------------------------------+
| Checksum | Other TCP fields      |
+----------------------------------+
```

UDP has a much smaller header:

```text
+----------------------------------+
| Source Port | Destination Port  |
+----------------------------------+
| Length      | Checksum           |
+----------------------------------+
```

---

## TCP Header

TCP contains fields for features such as:

```text
Source Port
Destination Port
Sequence Number
Acknowledgement Number
Flags
Window Size
Checksum
```

These fields support:

```text
Reliability
Sequencing
Acknowledgement
Connection management
Flow control
```

---

## UDP Header

UDP contains:

```text
Source Port
Destination Port
Length
Checksum
```

UDP therefore has much less transport-layer overhead.

---

# 10. Comparing TCP & UDP on Points

The key comparison from the notes is:

### TCP provides more features than UDP

However, these additional features come with additional:

> **Overhead**

---

## Applications Requiring Reliable Communication

For applications that require reliable communication, TCP is preferred.

For example:

```text
Downloading a file
```

When downloading a file, missing or incorrectly ordered data can cause the file to be corrupted.

TCP provides:

```text
Sequencing
Acknowledgement
Retransmission
Flow Control
```

---

## Real-Time Voice and Video

For applications such as:

```text
Real-time voice
Real-time video
```

UDP can be preferred because timely delivery can be more important than retransmitting every lost packet.

For example:

```text
Voice packet
     ↓
Lost
     ↓
Continue with newer voice packets
```

Waiting for an old packet to be retransmitted may not be useful in a real-time conversation.

---

## Reliability Can Be Provided by the Application

Some applications use UDP but provide reliability or other mechanisms within the application itself.

Therefore:

```text
UDP
+
Application-level reliability
```

is possible.

---

## Some Applications Use Both TCP and UDP

Some applications can use both TCP and UDP depending on the situation.

Therefore, it is important not to assume that every application always uses only one transport protocol.

---

# 11. Comparing TCP & UDP in Table

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable | Unreliable / no TCP-style reliability |
| Sequencing | No sequencing |
| Flow control | No TCP-style flow control |
| More features | Fewer features |
| More overhead | Lower overhead |
| Uses acknowledgements | No TCP-style acknowledgements |
| Retransmission available | No TCP-style retransmission |
| Suitable for reliable data transfer | Suitable for applications where low overhead/timeliness is important |
| Example: file downloads | Example: VoIP / live video |

---

## Simple Comparison

```text
                 TCP              UDP
                  |                |
          Connection-oriented   Connectionless
                  |                |
              Reliable         Unreliable
                  |                |
             Sequencing       No sequencing
                  |                |
             Flow control     No flow control
                  |                |
            More overhead     Less overhead
```

---

# 12. Port Numbers

Port numbers are Layer 4 addresses.

They help identify the application or service involved in communication.

Remember:

> **Transport-layer ports are not the physical ports/interfaces on routers or switches.**

---

## TCP Port Numbers

Important TCP ports from the notes:

| Port | Protocol / Service |
|---:|---|
| 20 | FTP Data |
| 21 | FTP Control |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 80 | HTTP |
| 110 | POP3 |
| 443 | HTTPS |

---

## UDP Port Numbers

Important UDP ports from the notes:

| Port | Protocol / Service |
|---:|---|
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP |
| 161 | SNMP Agent |
| 162 | SNMP Manager |
| 514 | Syslog |

---

## TCP & UDP Port

Some protocols can use both TCP and UDP.

The notes specifically identify:

```text
DNS
Port 53
```

DNS usually uses UDP but can use TCP in some situations.

Therefore:

```text
DNS → Port 53
```

and the transport protocol can be:

```text
UDP
or
TCP
```

depending on the situation.

---

## SSH — TCP 22

SSH stands for:

> **Secure Shell**

SSH is used to securely connect to the CLI of network devices such as:

```text
Router
Switch
```

Example:

```text
PC
 |
 | TCP 22
 ↓
Router / Switch
```

---

## FTP — TCP 20 and 21

FTP uses:

```text
TCP 20 → FTP Data
TCP 21 → FTP Control
```

---

## Telnet — TCP 23

Telnet uses:

```text
TCP 23
```

It provides remote CLI access.

---

## SMTP — TCP 25

SMTP is associated with:

```text
Sending email
```

Port:

```text
TCP 25
```

---

## HTTP — TCP 80

HTTP is used for:

```text
Accessing webpages
```

Port:

```text
TCP 80
```

---

## POP3 — TCP 110

POP3 stands for:

> **Post Office Protocol**

It is associated with retrieving email.

Port:

```text
TCP 110
```

---

## HTTPS — TCP 443

HTTPS is the secure version of HTTP.

Port:

```text
TCP 443
```

---

## DHCP — UDP 67 and 68

DHCP uses:

```text
UDP 67 → DHCP Server
UDP 68 → DHCP Client
```

---

## TFTP — UDP 69

TFTP stands for:

> **Trivial File Transfer Protocol**

Port:

```text
UDP 69
```

---

## SNMP — UDP 161 and 162

SNMP stands for:

> **Simple Network Management Protocol**

The notes identify:

```text
UDP 161 → SNMP Agent
UDP 162 → SNMP Manager
```

---

## Syslog — UDP 514

Syslog commonly uses:

```text
UDP 514
```

for sending system/log messages.

---

# Quick Revision

## Layer 4

```text
Layer 4 = Transport Layer

Main protocols:
TCP
UDP
```

---

## TCP

```text
TCP
↓
Connection-oriented
↓
Reliable
↓
Sequencing
↓
Acknowledgement
↓
Retransmission
↓
Flow control
↓
Window Size
```

---

## TCP Three-Way Handshake

```text
SYN
 ↓
SYN + ACK
 ↓
ACK
```

### Remember:

```text
3-way = Establish
```

---

## TCP Four-Way Handshake

```text
FIN
 ↓
ACK
 ↓
FIN
 ↓
ACK
```

### Remember:

```text
4-way = Terminate
```

---

## TCP Sequencing

```text
Sequence Number
      ↓
Keeps track of data order
```

---

## TCP Acknowledgement

```text
ACK Number
     ↓
Indicates the next expected data
```

---

## TCP Retransmission

```text
Segment Lost
     ↓
No expected ACK
     ↓
Retransmission
```

---

## TCP Flow Control

```text
Window Size
     ↓
Controls how much data
can be sent before ACK
```

---

## UDP

```text
UDP
↓
Connectionless
↓
No TCP-style reliability
↓
No TCP-style sequencing
↓
No TCP-style flow control
↓
Low overhead
```

---

# Important Port Numbers to Memorise

```text
TCP
20  → FTP Data
21  → FTP Control
22  → SSH
23  → Telnet
25  → SMTP
80  → HTTP
110 → POP3
443 → HTTPS
```

```text
UDP
67  → DHCP Server
68  → DHCP Client
69  → TFTP
161 → SNMP Agent
162 → SNMP Manager
514 → Syslog
```

```text
TCP & UDP
53  → DNS
```

---

# Final CCNA Memory Diagram

```text
                         OSI MODEL

                    LAYER 4
                   TRANSPORT
                       |
              ┌────────┴────────┐
              |                 |
             TCP               UDP
              |                 |
       Connection-oriented   Connectionless
              |                 |
           Reliable          No TCP-style
              |               reliability
              |
       ┌──────┼─────────┐
       |      |         |
   Sequence  ACK    Retransmission
       |
   Flow Control
       |
   Window Size
```

---

# TCP Connection Lifecycle

```text
              ESTABLISH
                  |
                  ↓
              SYN
                  |
                  ↓
             SYN + ACK
                  |
                  ↓
                 ACK
                  |
                  ↓
           DATA TRANSFER
                  |
                  ↓
             Sequencing
                  |
                  ↓
          Acknowledgement
                  |
                  ↓
           Retransmission
          if required
                  |
                  ↓
           Flow Control
                  |
                  ↓
              TERMINATE
                  |
                  ↓
                FIN
                  |
                  ↓
                ACK
                  |
                  ↓
                FIN
                  |
                  ↓
                ACK
                  |
                  ↓
             CONNECTION
                CLOSED
```

---

# Final Summary

The Transport Layer is **Layer 4** of the OSI model.

Its major protocols are:

```text
TCP
UDP
```

TCP is:

```text
Connection-oriented
Reliable
Sequenced
Acknowledged
Flow-controlled
```

TCP establishes connections using:

```text
SYN
SYN + ACK
ACK
```

TCP terminates connections using the typical four-way exchange:

```text
FIN
ACK
FIN
ACK
```

TCP uses:

```text
Sequence Numbers
Acknowledgement Numbers
Retransmission
Window Size
```

UDP is:

```text
Connectionless
Low overhead
No TCP-style sequencing
No TCP-style acknowledgements
No TCP-style retransmission
No TCP-style flow control
```

UDP has a simple:

```text
8-byte header
```

containing:

```text
Source Port
Destination Port
Length
Checksum
```

The most important difference to remember is:

```text
TCP
=
More features + more overhead + reliable communication

UDP
=
Fewer features + lower overhead + connectionless communication
```

Neither protocol is automatically "better".

The appropriate protocol depends on the requirements of the application.

---

# CCNA Final Cheat Sheet

```text
Layer 4
    ↓
Transport

TCP
    ↓
Connection-oriented
Reliable
Sequencing
Acknowledgement
Retransmission
Flow control
Window Size

TCP Establishment
    ↓
SYN
SYN-ACK
ACK

TCP Termination
    ↓
FIN
ACK
FIN
ACK

UDP
    ↓
Connectionless
Low overhead
No TCP-style sequencing
No TCP-style ACK
No TCP-style retransmission
No TCP-style flow control
8-byte header

Important Ports

TCP:
20  FTP Data
21  FTP Control
22  SSH
23  Telnet
25  SMTP
80  HTTP
110 POP3
443 HTTPS

UDP:
67  DHCP Server
68  DHCP Client
69  TFTP
161 SNMP Agent
162 SNMP Manager
514 Syslog

TCP & UDP:
53 DNS
```

---

**End of TCP & UDP Notes**
