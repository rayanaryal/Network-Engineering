# DTP & VTP

This section covers two important Cisco technologies related to VLANs and trunking:

- **DTP — Dynamic Trunking Protocol**
- **VTP — VLAN Trunking Protocol**

The notes are focused on **CCNA 200-301 exam preparation**, Cisco IOS configuration, understanding switchport modes, trunk negotiation, VTP operation, VTP revision numbers, and the risks associated with VTP.

---

# Table of Contents

1. [DTP Introduction](#1-dtp-introduction)
2. [DTP and Switchport Modes](#2-dtp-and-switchport-modes)
3. [Trunk Mode](#3-trunk-mode)
4. [Access Mode](#4-access-mode)
5. [Dynamic Desirable Mode](#5-dynamic-desirable-mode)
6. [Dynamic Auto Mode](#6-dynamic-auto-mode)
7. [DTP Administrative Mode Comparison](#7-dtp-administrative-mode-comparison)
8. [DTP with Non-Switch Devices](#8-dtp-with-non-switch-devices)
9. [DTP Security and `switchport nonegotiate`](#9-dtp-security-and-switchport-nonegotiate)
10. [DTP Encapsulation Negotiation](#10-dtp-encapsulation-negotiation)
11. [DTP Frame VLAN](#11-dtp-frame-vlan)
12. [DTP Quick Memory Guide](#12-dtp-quick-memory-guide)
13. [VTP Introduction](#13-vtp-introduction)
14. [VTP Operating Modes](#14-vtp-operating-modes)
15. [VTP Server](#15-vtp-server)
16. [VTP Client](#16-vtp-client)
17. [VTP Transparent Mode](#17-vtp-transparent-mode)
18. [VTP Versions](#18-vtp-versions)
19. [VTP Domain](#19-vtp-domain)
20. [VTP Revision Number](#20-vtp-revision-number)
21. [VTP Revision Number 0](#21-vtp-revision-number-0)
22. [VTP Revision Number X](#22-vtp-revision-number-x)
23. [The Major Danger of VTP](#23-the-major-danger-of-vtp)
24. [VTP Database Synchronisation](#24-vtp-database-synchronisation)
25. [VTP Server-to-Server Synchronisation](#25-vtp-server-to-server-synchronisation)
26. [VTP Transparent Mode in Detail](#26-vtp-transparent-mode-in-detail)
27. [VTP Extended VLAN Range](#27-vtp-extended-vlan-range)
28. [VTP2 and Token Ring](#28-vtp2-and-token-ring)
29. [DTP vs VTP](#29-dtp-vs-vtp)
30. [CCNA Exam Memory Map](#30-ccna-exam-memory-map)
31. [Quick Revision Table](#31-quick-revision-table)
32. [CCNA Quick Quiz](#32-ccna-quick-quiz)
33. [Final Summary](#33-final-summary)

---

# 1. DTP Introduction

## What is DTP?

**DTP — Dynamic Trunking Protocol** is a **Cisco proprietary protocol** that allows Cisco switches to dynamically negotiate whether a switchport should operate as an **access port or trunk port**.

DTP is designed to allow connected Cisco switches to automatically determine their trunking status.

```text
        SW1                         SW2
   ┌───────────┐              ┌───────────┐
   │           │              │           │
   │           │==============│           │
   │           │     DTP      │           │
   └───────────┘              └───────────┘
```

Instead of manually configuring both sides, DTP can negotiate the trunk.

---

## Important

DTP is a **Cisco proprietary protocol**.

It is used between Cisco switches to negotiate trunking.

```text
Cisco Switch ←──── DTP ────→ Cisco Switch
```

DTP is not required when the trunk is manually configured.

---

# 2. DTP and Switchport Modes

There are several switchport administrative modes that are important when studying DTP.

The main CCNA-relevant modes are:

```text
access
trunk
dynamic desirable
dynamic auto
```

There are also other switchport modes such as:

```text
dot1q-tunnel
private-vlan
```

but these are not the main DTP negotiation modes required for understanding the standard CCNA DTP scenarios.

---

## Main DTP Modes

| Administrative Mode | Behaviour |
|---|---|
| `access` | Forces the port to operate as an access port |
| `trunk` | Forces the port to operate as a trunk |
| `dynamic desirable` | Actively attempts to form a trunk |
| `dynamic auto` | Passively waits for the other side to request trunking |

---

# 3. Trunk Mode

The command:

```cisco
switchport mode trunk
```

manually configures the interface as a trunk.

Example:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode trunk
```

The port is now configured to operate as a trunk.

```text
        SW1                         SW2
   ┌───────────┐              ┌───────────┐
   │           │              │           │
   │   TRUNK   │==============│   TRUNK   │
   │           │              │           │
   └───────────┘              └───────────┘
```

A trunk can carry traffic from multiple VLANs.

---

# 4. Access Mode

The command:

```cisco
switchport mode access
```

manually configures the port as an access port.

Example:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode access
```

An access port normally belongs to a single VLAN.

```text
        SW1
         |
         |
      ACCESS
         |
         |
        PC
```

For example:

```cisco
SW1(config-if)# switchport access vlan 10
```

This places the access port into VLAN 10.

---

## Static Access vs Dynamic Access

A **static access port** is an access port that belongs to a specific VLAN unless manually changed.

```text
Access Port
     |
     ↓
VLAN 10
```

There are also dynamic access mechanisms that can automatically assign VLANs based on the connected device's MAC address.

However, dynamic access is **outside the main CCNA DTP scope**.

---

# 5. Dynamic Desirable Mode

The command is:

```cisco
switchport mode dynamic desirable
```

Example:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode dynamic desirable
```

## What does Dynamic Desirable mean?

A port in **dynamic desirable** mode actively tries to form a trunk.

Think:

> **Desirable = "I want to become a trunk."**

It actively negotiates with the device on the other side.

---

## Dynamic Desirable + Trunk

```text
SW1                         SW2
Dynamic Desirable            Trunk
       |                       |
       |------ DTP ------------|
               ↓
             TRUNK
```

Result:

```text
TRUNK
```

---

## Dynamic Desirable + Dynamic Desirable

```text
SW1                         SW2
Dynamic Desirable            Dynamic Desirable
       |                       |
       |--------- DTP ---------|
                 ↓
               TRUNK
```

Result:

```text
TRUNK
```

---

## Dynamic Desirable + Dynamic Auto

```text
SW1                         SW2
Dynamic Desirable            Dynamic Auto
       |                       |
       |--------- DTP ---------|
                 ↓
               TRUNK
```

Result:

```text
TRUNK
```

This works because **desirable actively requests trunking**, while auto is willing to form a trunk when the other side requests it.

---

# 6. Dynamic Auto Mode

The command is:

```cisco
switchport mode dynamic auto
```

Example:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode dynamic auto
```

## What does Dynamic Auto mean?

Dynamic Auto is **passive**.

It does **not actively try to form a trunk**.

Instead, it waits for the other side to actively negotiate trunking.

Think:

> **Auto = "I'll wait and see."**

---

## Dynamic Auto + Dynamic Auto

```text
SW1                         SW2
Dynamic Auto                 Dynamic Auto
       |                       |
       |                       |
       |       DTP             |
       |<--------------------->|
```

Neither side actively requests trunking.

Result:

```text
ACCESS
```

---

## Dynamic Auto + Dynamic Desirable

```text
SW1                         SW2
Dynamic Auto                 Dynamic Desirable
       |                       |
       |--------- DTP ---------|
                 ↓
               TRUNK
```

Result:

```text
TRUNK
```

---

## Dynamic Auto + Trunk

```text
SW1                         SW2
Dynamic Auto                 Trunk
       |                       |
       |--------- DTP ---------|
                 ↓
               TRUNK
```

Result:

```text
TRUNK
```

---

# 7. DTP Administrative Mode Comparison

This is one of the most important CCNA tables to memorise.

| SW1 | SW2 | Result |
|---|---|---|
| `access` | `access` | Access |
| `access` | `trunk` | Access / non-trunking on the access side |
| `access` | `dynamic desirable` | Access |
| `access` | `dynamic auto` | Access |
| `trunk` | `trunk` | Trunk |
| `trunk` | `dynamic desirable` | Trunk |
| `trunk` | `dynamic auto` | Trunk |
| `dynamic desirable` | `dynamic desirable` | Trunk |
| `dynamic desirable` | `dynamic auto` | Trunk |
| `dynamic auto` | `dynamic auto` | Access |

The most important combinations are:

```text
Desirable + Desirable = TRUNK

Desirable + Auto = TRUNK

Auto + Auto = ACCESS
```

---

# 8. DTP with Non-Switch Devices

DTP is designed for Cisco switch-to-switch negotiation.

For example:

```text
Switch ───────── Switch
        DTP
```

But consider:

```text
Switch ───────── PC
```

A PC does not participate in DTP.

Therefore, DTP cannot negotiate a trunk with the PC.

The switchport will operate as an access port.

Similarly:

```text
Switch ───────── Router
```

A router does not participate in DTP negotiation in the same way as a Cisco switch.

Therefore, the switchport should be manually configured according to the required design.

---

# 9. DTP Security and `switchport nonegotiate`

DTP is enabled by default on Cisco switch interfaces according to the source material.

However, for security and predictability, manual configuration is recommended.

Instead of relying on DTP:

```cisco
switchport mode access
```

or:

```cisco
switchport mode trunk
```

can be manually configured.

---

## Disable DTP Negotiation

The command is:

```cisco
switchport nonegotiate
```

Example:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport nonegotiate
```

This means:

```text
Manually configured trunk
        +
DTP negotiation disabled
```

---

## Important

`switchport nonegotiate` should be used with a statically configured access/trunk port rather than relying on dynamic negotiation.

---

## Access Mode Also Disables DTP Negotiation

Configuring:

```cisco
switchport mode access
```

also disables DTP negotiation on the interface.

Therefore, two important ways discussed in the notes for disabling DTP negotiation are:

```cisco
switchport nonegotiate
```

or:

```cisco
switchport mode access
```

---

# 10. DTP Encapsulation Negotiation

Some older Cisco switches supported more than one trunk encapsulation:

```text
ISL
802.1Q
```

DTP could negotiate the trunk encapsulation between supported Cisco switches.

The command found in older Cisco IOS configurations is:

```cisco
switchport trunk encapsulation negotiate
```

This allowed the switch to negotiate the encapsulation.

---

## ISL vs 802.1Q

Historically:

```text
ISL
802.1Q
```

were Cisco trunk encapsulation options.

The document notes that when both switches supported ISL and 802.1Q, **ISL was favoured** during encapsulation negotiation.

However, modern Cisco switching is overwhelmingly based on **802.1Q**, and many modern switches do not support ISL at all.

For CCNA study, the important historical concept is:

> DTP could also negotiate trunk encapsulation on older Cisco platforms.

---

# 11. DTP Frame VLAN

An important CCNA question is:

> **When using 802.1Q, which VLAN are DTP frames sent in?**

### Answer:

> **The native VLAN.**

The default native VLAN is normally:

```text
VLAN 1
```

Therefore:

```text
802.1Q
   ↓
DTP frames
   ↓
Native VLAN
   ↓
Default = VLAN 1
```

---

## Historical ISL Case

According to the document:

```text
ISL
 ↓
DTP frames sent in VLAN 1
```

For 802.1Q:

```text
802.1Q
 ↓
DTP frames sent in native VLAN
```

---

# 12. DTP Quick Memory Guide

Remember the personalities:

```text
TRUNK
"I am a trunk."

ACCESS
"I am an access port."

DYNAMIC DESIRABLE
"I want to become a trunk."

DYNAMIC AUTO
"I will become a trunk if you ask me."
```

---

## The Most Important Three

```text
DESIRABLE + DESIRABLE
        ↓
      TRUNK
```

```text
DESIRABLE + AUTO
        ↓
      TRUNK
```

```text
AUTO + AUTO
        ↓
      ACCESS
```

---

# 13. VTP Introduction

## What is VTP?

**VTP — VLAN Trunking Protocol** is a Cisco protocol used to distribute VLAN information between switches in the same VTP domain.

The basic idea is:

```text
                 VTP Server
                     |
              VLAN database
                     |
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    Client         Client       Transparent
```

A VTP server can create, modify, and delete VLANs.

VTP clients can synchronise their VLAN database from the VTP server.

---

## Why was VTP created?

VTP was designed for large networks with many switches and VLANs.

Without VTP:

```text
SW1 → configure VLANs
SW2 → configure VLANs
SW3 → configure VLANs
SW4 → configure VLANs
SW5 → configure VLANs
```

With VTP:

```text
             VTP Server
          VLAN configuration
                  |
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     Client    Client    Client
```

The VLAN information can be synchronised.

---

## Important CCNA Note

VTP is **rarely used in modern networks**, and the source material recommends avoiding it unless there is a specific reason to use it.

This is important because VTP can introduce significant operational risk.

---

# 14. VTP Operating Modes

The document covers three VTP modes:

```text
Server
Client
Transparent
```

---

# 15. VTP Server

A VTP server can:

- Add VLANs
- Modify VLANs
- Delete VLANs
- Store the VLAN database
- Advertise VLAN information over trunk links
- Increase the VTP revision number when the VLAN database changes

Example:

```text
             VTP SERVER
                 |
        VLAN 10, 20, 30
                 |
        ┌────────┼────────┐
        ↓        ↓        ↓
     Client   Client   Client
```

---

## VLAN Database Changes

If a VLAN is:

```text
Added
Modified
Deleted
```

the VTP server increases the:

```text
Revision Number
```

Example:

```text
Revision 5
    ↓
Add VLAN 40
    ↓
Revision 6
```

---

## VTP Server Advertisement

The server advertises the latest VLAN database over trunk interfaces.

VTP clients can synchronise their VLAN database to the server.

---

## Important

A VTP server can also behave as a VTP client for synchronisation purposes.

Therefore:

> **A VTP server can synchronise its VLAN database from another VTP server with a higher revision number in the same VTP domain.**

This is a very important concept.

---

# 16. VTP Client

A VTP client receives VLAN database information from VTP servers.

The source material describes VTP clients as:

- Unable to add/modify/delete VLANs
- Synchronising their VLAN database to the server with the highest revision number in their VTP domain
- Advertising/forwarding VTP advertisements to other clients over trunk ports

Conceptually:

```text
             VTP SERVER
          Revision 10
               |
               |
             trunk
               |
               ↓
          VTP CLIENT
          Revision 10
```

If the client receives a newer database:

```text
Client Revision 5
        +
Server Revision 10
        ↓
Client synchronises
        ↓
Client Revision 10
```

---

# 17. VTP Transparent Mode

VTP Transparent mode behaves differently from Server and Client mode.

The document describes VTP Transparent mode as:

> It does not participate in the VTP domain and does not synchronise its VLAN database.

A transparent switch maintains its own VLAN database.

```text
              VTP SERVER
                   |
                   |
              VTP CLIENT
                   |
                   |
             TRANSPARENT
                   |
                   |
               VLAN DB
              independent
```

---

## Transparent Mode Can Modify VLANs

A VTP transparent switch can:

```text
Add VLAN
Modify VLAN
Delete VLAN
```

These changes affect its own local VLAN database.

They are not advertised as its own VLAN database changes to synchronise other switches.

---

## Transparent Mode Forwards VTP Advertisements

An important detail:

> A VTP transparent switch can forward VTP advertisements that are in the same VTP domain.

Therefore:

```text
VTP Server
    |
    | VTP advertisement
    ↓
Transparent Switch
    |
    | forwards advertisement
    ↓
VTP Client
```

But the transparent switch does not synchronise its own VLAN database from the server.

---

# 18. VTP Versions

The document covers:

```text
VTP Version 1
VTP Version 2
VTP Version 3
```

---

# 19. VTP Version 1

VTPv1 is the original version discussed in the notes.

It supports basic VTP VLAN database synchronisation.

---

# 20. VTP Version 2

According to the document:

> VTPv2 is not much different from VTPv1.

The major difference highlighted in the notes is:

```text
VTPv2
  ↓
Token Ring VLAN support
```

Therefore:

> If you use Token Ring VLANs, VTPv2 must be enabled.

Otherwise, according to the source material, there is no particular reason to choose VTPv2 over VTPv1 for that feature.

---

# 21. VTP Version 3

VTPv3 introduces additional capabilities compared with VTPv1/v2.

One important point from the document is:

```text
VTPv1/v2
    ↓
Do NOT support
extended VLAN range
1006–4094
```

Whereas:

```text
VTPv3
    ↓
Supports
extended VLAN range
1006–4094
```

---

# 22. VTP Domain

A **VTP domain** is a logical group of switches that share VTP information.

For example:

```text
VTP Domain: CISCO
```

Switches using:

```text
Domain = CISCO
```

can participate in the same VTP domain.

---

## Example

```text
SW1
Domain: CISCO

SW2
Domain: CISCO

SW3
Domain: CISCO
```

These switches can exchange VTP information over their trunk connections.

---

## Different VTP Domains

If:

```text
SW1 → Domain CISCO
SW2 → Domain NETWORK
```

they are not members of the same VTP domain.

---

# 23. VTP Domain NULL

The document highlights an important behaviour:

> If a switch has no VTP domain configured (domain NULL) and receives a VTP advertisement containing a VTP domain name, it can automatically join that VTP domain.

Conceptually:

```text
Switch
Domain = NULL
     |
     | receives VTP advertisement
     |
     ↓
Advertisement says:
Domain = CISCO
     |
     ↓
Switch joins CISCO domain
```

This is an important reason to be careful with VTP.

---

# 24. VTP Revision Number

The **VTP revision number** identifies the version of the VLAN database within the VTP domain.

Think of it like:

```text
VLAN Database
     +
Revision Number
```

The higher revision number represents a newer VLAN database.

---

## Example

```text
SW1
Revision 5

SW2
Revision 10
```

If they are in the same VTP domain and the conditions for synchronisation are met:

```text
Revision 10
     ↓
Newer database
     ↓
Revision 5 switch synchronises
```

---

# 25. VTP Revision Number 0

A switch can have:

```text
Revision Number = 0
```

This represents the initial/reset state of the VTP revision number.

The document highlights two ways the revision number can be reset to 0:

### Change VTP domain to an unused domain

```text
Old Domain
    ↓
Change to unused domain
    ↓
Revision = 0
```

### Change VTP mode to Transparent

```text
VTP Server/Client
       ↓
Transparent
       ↓
Revision = 0
```

---

# 26. VTP Revision Number X

Every time a VTP server modifies the VLAN database, the revision number increases.

For example:

```text
Revision 5
    ↓
Add VLAN 50
    ↓
Revision 6
```

Another change:

```text
Revision 6
    ↓
Modify VLAN 50
    ↓
Revision 7
```

Another change:

```text
Revision 7
    ↓
Delete VLAN 50
    ↓
Revision 8
```

Therefore:

> **VTP servers increase the revision number whenever a VLAN is added, modified, or deleted.**

---

# 27. The Major Danger of VTP

This is one of the **most important VTP concepts for the CCNA exam**.

Imagine your network currently has:

```text
VTP Domain: CISCO
Revision: 5
```

And the network contains:

```text
VLAN 10
VLAN 20
VLAN 30
VLAN 40
```

Now imagine you take an old switch from another network.

That switch has:

```text
VTP Domain: CISCO
Revision: 50
```

but its VLAN database contains:

```text
VLAN 1
VLAN 99
VLAN 220
```

You connect it to your network.

---

## What can happen?

Because:

```text
Domain matches
        +
Revision is higher
```

the other switches may consider its VLAN database to be newer.

```text
Old switch
Revision 50
     |
     | Superior VTP information
     ↓
Existing network
Revision 5
```

The switches can synchronise to the higher revision database.

---

## Result

Your existing VLAN database can be replaced.

```text
BEFORE

VLAN 10
VLAN 20
VLAN 30
VLAN 40
```

After synchronisation:

```text
VLAN 1
VLAN 99
VLAN 220
```

Potentially, VLANs that were previously required by the network disappear.

This can cause major network disruption.

---

# 28. Why the VTP Revision Number Is Dangerous

The dangerous combination is:

```text
Same VTP Domain
        +
Higher Revision Number
        +
Unwanted VLAN Database
```

This can cause:

```text
Incorrect VLAN database
        ↓
VLANs disappear
        ↓
Ports may lose VLAN membership
        ↓
Network connectivity problems
```

---

# 29. Safe Thinking Before Connecting an Old Switch

Before connecting an old switch to a VTP network, check:

```text
VTP Domain
VTP Mode
VTP Version
VTP Revision Number
VLAN Database
```

Especially:

```text
VTP Revision Number
```

---

# 30. VTP Database Synchronisation

The basic synchronisation process can be visualised as:

```text
             VTP SERVER
             Revision 10
                  |
                  |
            VTP Advertisement
                  |
                  ↓
             VTP CLIENT
             Revision 5
                  |
                  ↓
          Higher revision?
                  |
                 YES
                  |
                  ↓
       Synchronise VLAN database
                  |
                  ↓
             Revision 10
```

---

# 31. VTP Server-to-Server Synchronisation

One of the interesting VTP concepts is that **VTP servers can synchronise with other VTP servers**.

Example:

```text
SW1                     SW2
VTP Server              VTP Server
Revision 5              Revision 10
   |                         |
   └──────── trunk ──────────┘
```

Because SW2 has the higher revision:

```text
Revision 10 > Revision 5
```

SW1 can synchronise to the newer VLAN database.

Therefore:

> **Do not assume that only VTP clients synchronise. VTP servers can also synchronise.**

---

# 32. VTP Transparent Mode in Detail

Transparent mode is different.

Example:

```text
SW1
VTP Server
Domain CISCO
     |
     |
     ↓
SW2
VTP Transparent
Domain CISCO
     |
     |
     ↓
SW3
VTP Client
Domain CISCO
```

SW2 maintains its own VLAN database.

If SW2 creates:

```text
VLAN 100
```

that VLAN is local to SW2.

It does not synchronise the VLAN database as a VTP server would.

---

## Transparent Mode Behaviour

| Behaviour | Transparent |
|---|---|
| Synchronises VLAN database? | No |
| Can create VLANs? | Yes |
| Can modify VLANs? | Yes |
| Can delete VLANs? | Yes |
| Maintains its own VLAN database? | Yes |
| Forwards VTP advertisements? | Yes, when applicable |
| Participates in database synchronisation? | No |

---

# 33. VTP Server vs Client vs Transparent

| Feature | Server | Client | Transparent |
|---|---|---|---|
| Add VLAN | Yes | No | Yes |
| Modify VLAN | Yes | No | Yes |
| Delete VLAN | Yes | No | Yes |
| Maintains VLAN database | Yes | Yes | Yes |
| Synchronises database | Yes | Yes | No |
| Advertises VTP information | Yes | Yes/forwards | Forwards |
| Own VLAN changes propagated | Yes | No | No |

---

# 34. VTP Default Operating Mode

The document states that Cisco switches operate in:

```text
VTP Server mode
```

by default.

Therefore:

```text
Default VTP Mode
       ↓
     Server
```

However, exact defaults can vary between Cisco platforms and software releases, so when working on actual equipment, verify the platform-specific behaviour.

---

# 35. DTP vs VTP

These two protocols are easy to confuse because both are Cisco technologies involving switches.

But they solve **completely different problems**.

---

## DTP

**Dynamic Trunking Protocol**

Main purpose:

```text
Negotiate:
Access or Trunk
```

Example:

```text
SW1 ←──── DTP ────→ SW2
```

DTP deals with **trunk negotiation**.

---

## VTP

**VLAN Trunking Protocol**

Main purpose:

```text
Synchronise VLAN database
```

Example:

```text
        VTP Server
             |
       VLAN database
             |
       ┌─────┴─────┐
       ↓           ↓
    Client       Client
```

VTP deals with **VLAN database distribution**.

---

# 36. DTP vs VTP – Easy Memory Trick

```text
DTP
D = Dynamic
T = Trunking
P = Protocol

→ "Should this link become a trunk?"
```

```text
VTP
V = VLAN
T = Trunking
P = Protocol

→ "How should VLAN information be shared?"
```

---

# 37. Important Relationship Between DTP and VTP

DTP and VTP are separate protocols.

A trunk is important because VTP advertisements are carried between switches over trunk connections.

Conceptually:

```text
              TRUNK
        =================
        |               |
       SW1             SW2
        |               |
       DTP             VTP
        |               |
 Trunk negotiation   VLAN database
```

DTP can help establish the trunk.

VTP can then use the trunk to exchange VTP information.

---

# 38. DTP Configuration Examples

## Force Trunk

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode trunk
```

---

## Force Access

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode access
```

---

## Dynamic Desirable

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode dynamic desirable
```

---

## Dynamic Auto

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport mode dynamic auto
```

---

## Disable DTP Negotiation

```cisco
SW1(config)# interface g0/1
SW1(config-if)# switchport nonegotiate
```

---

# 39. DTP Configuration Recommendation

For security and predictable network behaviour, manually configure switchports.

Instead of:

```cisco
switchport mode dynamic desirable
```

or:

```cisco
switchport mode dynamic auto
```

use:

```cisco
switchport mode access
```

or:

```cisco
switchport mode trunk
```

when the role of the port is known.

---

## Example: PC Port

```cisco
interface g0/1
 switchport mode access
 switchport access vlan 10
```

---

## Example: Switch-to-Switch Trunk

```cisco
interface g0/1
 switchport mode trunk
 switchport nonegotiate
```

This makes the intended role explicit and prevents unnecessary DTP negotiation.

---

# 40. DTP Troubleshooting

Useful commands include:

```cisco
show interfaces switchport
```

and:

```cisco
show interfaces trunk
```

These commands help determine:

- Administrative mode
- Operational mode
- Trunk status
- Access VLAN
- Native VLAN
- Allowed VLANs

---

## Example

```cisco
SW1# show interfaces g0/1 switchport
```

Look for:

```text
Administrative Mode
Operational Mode
Administrative Trunking Encapsulation
Operational Trunking Encapsulation
Access Mode VLAN
Trunking Native Mode VLAN
```

---

# 41. VTP Verification

Useful commands include:

```cisco
show vtp status
```

This can display information such as:

```text
VTP Version
VTP Operating Mode
VTP Domain Name
VTP Pruning Mode
VTP V2 Mode
VTP Traps Generation
VTP Revision
```

The exact output depends on the Cisco platform and IOS version.

---

# 42. VTP Troubleshooting Checklist

If VTP synchronisation is not working, check:

```text
1. VTP domain
2. VTP version
3. VTP mode
4. Trunk connection
5. VTP revision number
6. VTP password, if configured
7. VLAN database
```

---

# 43. CCNA Exam Memory Map

```text
                         DTP
                          |
              "Should this link be
                  a trunk?"
                          |
        ┌─────────────────┼─────────────────┐
        ↓                 ↓                 ↓
      TRUNK            DESIRABLE           AUTO
        |                 |                 |
   Force trunk       Wants trunk       Waits for
                                      other side
```

Important combinations:

```text
DESIRABLE + DESIRABLE = TRUNK

DESIRABLE + AUTO = TRUNK

AUTO + AUTO = ACCESS
```

---

```text
                         VTP
                          |
                  "Share VLAN
                   information"
                          |
           ┌──────────────┼──────────────┐
           ↓              ↓              ↓
        SERVER          CLIENT       TRANSPARENT
           |              |              |
      Creates VLANs   Syncs VLAN DB   Own VLAN DB
      Changes VLANs                   No sync
      Revision ↑                      Forwards VTP
```

---

# 44. Critical VTP Concept

Always remember:

```text
Higher VTP Revision Number
              ↓
       Newer VLAN database
```

Therefore:

```text
Same VTP Domain
       +
Higher Revision Number
       +
Unwanted/Old Switch
       ↓
Potential VLAN database overwrite
```

This is the major danger of VTP.

---

# 45. VTP Revision Number Example

Imagine:

```text
SW1
Domain: CISCO
Revision: 5

VLANs:
10
20
30
40
```

An old switch arrives:

```text
SW5
Domain: CISCO
Revision: 50

VLANs:
1
99
220
```

Because:

```text
50 > 5
```

SW5's VLAN database can be considered newer.

Potential result:

```text
Existing VLAN database
        ↓
Replaced/synchronised
        ↓
Old switch's VLAN database
```

This is why VTP must be treated carefully.

---

# 46. VTP Version Quick Guide

| Version | Important Point |
|---|---|
| **VTPv1** | Original VTP version |
| **VTPv2** | Adds Token Ring VLAN support |
| **VTPv3** | Supports extended VLAN range and adds further improvements |

From the source material:

```text
VTPv1/v2
1006–4094
   ↓
Not supported

VTPv3
1006–4094
   ↓
Supported
```

---

# 47. Important VTP Facts

### Fact 1

VTP is Cisco proprietary.

### Fact 2

VTP can distribute VLAN information between switches.

### Fact 3

VTP has three important operating modes:

```text
Server
Client
Transparent
```

### Fact 4

VTP servers can create, modify, and delete VLANs.

### Fact 5

VTP clients synchronise their VLAN database.

### Fact 6

VTP transparent switches maintain their own VLAN database.

### Fact 7

VTP servers increase the revision number when VLANs are added, modified, or deleted.

### Fact 8

A switch with a higher revision number can cause other switches in the same VTP domain to synchronise to its VLAN database.

### Fact 9

Changing the VTP domain to an unused domain resets the revision number to 0.

### Fact 10

Changing the VTP mode to transparent resets the revision number to 0.

### Fact 11

VTPv1/v2 do not support the extended VLAN range 1006–4094 according to the source material.

### Fact 12

VTPv3 supports the extended VLAN range.

---

# 48. CCNA Quick Quiz

## Question 1

What does DTP stand for?

<details>
<summary>Answer</summary>

**Dynamic Trunking Protocol**

</details>

---

## Question 2

What does DTP do?

<details>
<summary>Answer</summary>

DTP dynamically negotiates whether a Cisco switchport should operate as an access port or trunk port.

</details>

---

## Question 3

Which mode actively tries to form a trunk?

<details>
<summary>Answer</summary>

```text
Dynamic Desirable
```

</details>

---

## Question 4

Which mode is passive?

<details>
<summary>Answer</summary>

```text
Dynamic Auto
```

</details>

---

## Question 5

What happens with:

```text
Dynamic Desirable + Dynamic Auto
```

<details>
<summary>Answer</summary>

```text
TRUNK
```

</details>

---

## Question 6

What happens with:

```text
Dynamic Auto + Dynamic Auto
```

<details>
<summary>Answer</summary>

```text
ACCESS / NON-TRUNK
```

</details>

---

## Question 7

What command configures dynamic desirable?

<details>
<summary>Answer</summary>

```cisco
switchport mode dynamic desirable
```

</details>

---

## Question 8

What command disables DTP negotiation?

<details>
<summary>Answer</summary>

```cisco
switchport nonegotiate
```

</details>

---

## Question 9

When using 802.1Q, which VLAN are DTP frames sent in?

<details>
<summary>Answer</summary>

**The native VLAN.**

The default native VLAN is normally VLAN 1.

</details>

---

## Question 10

What does VTP stand for?

<details>
<summary>Answer</summary>

**VLAN Trunking Protocol**

</details>

---

## Question 11

What is the purpose of VTP?

<details>
<summary>Answer</summary>

To distribute/synchronise VLAN database information between switches in the same VTP domain.

</details>

---

## Question 12

What are the three VTP modes?

<details>
<summary>Answer</summary>

```text
Server
Client
Transparent
```

</details>

---

## Question 13

Which VTP mode can create, modify and delete VLANs?

<details>
<summary>Answer</summary>

```text
Server
```

VTP Transparent mode can also make local VLAN changes, but those changes are not synchronised as a VTP server's database.

</details>

---

## Question 14

Can a VTP client create VLANs?

<details>
<summary>Answer</summary>

No.

A VTP client synchronises its VLAN database from VTP information.

</details>

---

## Question 15

Does a VTP transparent switch synchronise its VLAN database with a VTP server?

<details>
<summary>Answer</summary>

**No.**

It maintains its own VLAN database.

</details>

---

## Question 16

Does a VTP transparent switch forward VTP advertisements?

<details>
<summary>Answer</summary>

Yes, it can forward VTP advertisements in the same VTP domain.

</details>

---

## Question 17

What happens to the VTP revision number when a VLAN is added, modified or deleted on a VTP server?

<details>
<summary>Answer</summary>

The revision number increases.

</details>

---

## Question 18

What happens if a switch with a higher revision number joins the same VTP domain?

<details>
<summary>Answer</summary>

Other switches may synchronise to the higher-revision VLAN database.

This is the major danger of VTP.

</details>

---

## Question 19

What happens to the revision number if the VTP domain is changed to an unused domain?

<details>
<summary>Answer</summary>

It resets to:

```text
0
```

</details>

---

## Question 20

What happens to the revision number when VTP mode is changed to Transparent?

<details>
<summary>Answer</summary>

It resets to:

```text
0
```

</details>

---

## Question 21

Which VTP version supports the extended VLAN range 1006–4094?

<details>
<summary>Answer</summary>

```text
VTPv3
```

</details>

---

## Question 22

What is the major difference between VTPv1 and VTPv2 mentioned in these notes?

<details>
<summary>Answer</summary>

VTPv2 adds support for Token Ring VLANs.

</details>

---

# 49. Ultra-Quick Revision

If you have only a few minutes before the exam:

```text
DTP
↓
Dynamic Trunking Protocol
↓
Cisco proprietary
↓
Negotiates access/trunk status
```

```text
Dynamic Desirable
↓
Actively wants trunk
```

```text
Dynamic Auto
↓
Passively waits
```

```text
Desirable + Desirable
↓
TRUNK
```

```text
Desirable + Auto
↓
TRUNK
```

```text
Auto + Auto
↓
ACCESS
```

```text
switchport nonegotiate
↓
Disable DTP negotiation
```

```text
802.1Q DTP frames
↓
Native VLAN
```

---

```text
VTP
↓
VLAN Trunking Protocol
↓
Distributes VLAN database information
```

```text
VTP Server
↓
Can create/modify/delete VLANs
↓
Revision number increases
```

```text
VTP Client
↓
Synchronises VLAN database
```

```text
VTP Transparent
↓
Does NOT synchronise VLAN database
↓
Maintains local VLAN database
↓
Can forward VTP advertisements
```

```text
Higher VTP revision
        ↓
Newer VLAN database
        ↓
Potential synchronisation
```

```text
VTP danger
↓
Old switch
+
Same domain
+
Higher revision
↓
Potential VLAN database overwrite
```

```text
VTPv1/v2
↓
No extended VLAN range 1006–4094

VTPv3
↓
Supports extended VLAN range
```

---

# 50. Final Summary

## DTP

**Dynamic Trunking Protocol** allows Cisco switches to dynamically negotiate trunking.

The four most important switchport modes are:

```text
access
trunk
dynamic desirable
dynamic auto
```

Remember:

```text
Desirable + Desirable = Trunk

Desirable + Auto = Trunk

Auto + Auto = Access
```

For security and predictable behaviour, manually configure switchports:

```cisco
switchport mode access
```

or:

```cisco
switchport mode trunk
```

DTP negotiation can be disabled with:

```cisco
switchport nonegotiate
```

---

## VTP

**VLAN Trunking Protocol** distributes VLAN database information between switches in the same VTP domain.

The three important modes are:

```text
Server
Client
Transparent
```

Remember:

```text
SERVER
→ Creates/modifies/deletes VLANs
→ Revision number increases
→ Advertises VLAN database
```

```text
CLIENT
→ Synchronises VLAN database
→ Cannot normally make VLAN database changes
```

```text
TRANSPARENT
→ Does not synchronise VLAN database
→ Maintains local VLAN database
→ Can make local VLAN changes
→ Can forward VTP advertisements
```

---

## The Most Important VTP Warning

```text
Same VTP Domain
       +
Higher Revision Number
       +
Old/Unwanted Switch
       ↓
Potential VLAN Database Synchronisation
       ↓
Potential Network Disruption
```

Therefore:

> **Always understand the VTP revision number before connecting an old switch to an existing VTP network.**

---

# 51. Final Mental Model

```text
                    VLAN / TRUNKING
                          |
             ┌────────────┴────────────┐
             │                         │
            DTP                       VTP
             │                         │
             ↓                         ↓
     "Should this link          "How is the VLAN
       become a trunk?"          database shared?"
             │                         │
       ┌─────┼─────┐           ┌──────┼──────┐
       ↓     ↓     ↓           ↓      ↓      ↓
     Trunk Desirable Auto    Server Client Transparent
                   │
                   ↓
             Auto + Auto
                   ↓
                ACCESS
```

### The five things I would memorise first for the CCNA:

```text
1. Desirable + Auto = Trunk

2. Auto + Auto = Access

3. switchport nonegotiate = Disable DTP negotiation

4. Higher VTP revision = Potentially newer VLAN database

5. Same VTP domain + unwanted higher revision
   = Major VTP danger
```

---

## Useful Verification Commands

### DTP / Switchport

```cisco
show interfaces switchport
```

```cisco
show interfaces trunk
```

### VTP

```cisco
show vtp status
```

---

## Key Commands

```cisco
! Force access
switchport mode access

! Force trunk
switchport mode trunk

! Dynamic desirable
switchport mode dynamic desirable

! Dynamic auto
switchport mode dynamic auto

! Disable DTP negotiation
switchport nonegotiate

! Check switchport configuration
show interfaces switchport

! Check trunk status
show interfaces trunk

! Check VTP status
show vtp status
```

---

**End of DTP & VTP Notes**

These notes are intended as a CCNA study reference covering the concepts, behaviour, configuration commands, troubleshooting points, and exam-style questions associated with DTP and VTP.
