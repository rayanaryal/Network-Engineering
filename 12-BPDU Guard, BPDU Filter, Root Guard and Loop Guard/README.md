# BPDU Guard, BPDU Filter, Root Guard & Loop Guard

This section documents important **Spanning Tree Protocol (STP) protection mechanisms** used to protect Layer 2 networks from loops, unauthorised switches, unexpected STP changes, and unidirectional link failures.

The main STP protection features covered in this section are:

- PortFast
- BPDU Guard
- BPDU Filter
- Root Guard
- Loop Guard
- ErrDisable
- ErrDisable Recovery
- Unidirectional links

---

# 1. STP Toolkit

STP provides loop prevention in switched networks, but additional features can be used to make the network safer and more predictable.

| Feature | Main purpose |
|---|---|
| **PortFast** | Allows an edge port connected to an end host to enter Forwarding immediately |
| **BPDU Guard** | Protects PortFast/edge ports from receiving BPDUs |
| **BPDU Filter** | Prevents a port from sending/processing BPDUs |
| **Root Guard** | Prevents a port from becoming a Root Port because of a superior BPDU |
| **Loop Guard** | Protects against loops caused by unexpectedly missing BPDUs |
| **ErrDisable** | Places a port into a disabled state after certain violations |
| **ErrDisable Recovery** | Automatically re-enables an err-disabled port after a configured period |

---

# 2. PortFast & BPDUs

## What is PortFast?

PortFast is designed for switch ports connected to **end devices**, such as:

- PCs
- Printers
- Servers
- Other devices that do not participate in STP

Normally, an STP port goes through states before forwarding traffic.

```text
Listening
    ↓
Learning
    ↓
Forwarding
```

PortFast allows an edge port to move directly into the **Forwarding** state.

```text
Port comes up
      ↓
   PortFast
      ↓
Immediately Forwarding
```

This is useful because an end device does not need to wait for the normal STP transition process.

---

## Important: PortFast does NOT disable STP

A PortFast-enabled port still participates in STP.

It can continue to send BPDUs.

The port can also react if it receives a BPDU.

```text
              BPDU
                ↓
        ┌──────────────┐
        │     SW1      │
        │              │
        │   PortFast   │
        │    G0/1      │
        └──────┬───────┘
               │
               │
              PC
```

A PortFast port continues to send BPDUs.

The document notes that BPDUs are sent approximately every **2 seconds**.

Because an end host normally does not run STP, a PortFast-enabled port should not normally receive BPDUs.

---

## What happens if a PortFast port receives a BPDU?

If a PortFast-enabled port receives an STP BPDU, it will revert to acting like a regular STP port without PortFast.

```text
PortFast-enabled port
          │
          │ receives BPDU
          ↓
"Something is running STP here"
          │
          ↓
PortFast behaviour is removed
          │
          ↓
Normal STP behaviour
```

### Memory trick

> **PortFast = "I expect an end device here."**

If a BPDU arrives:

> **"Something is not behaving like a normal end device."**

---

# 3. BPDU Guard

## The problem

PortFast should normally only be enabled on ports connected to devices that do not send BPDUs.

For example:

```text
              SW1
               |
               |
          PortFast port
               |
          Wall Jack
               |
              PC
```

This is normal.

But imagine an end user connects another switch to that port:

```text
                 SW1
                  |
             PortFast port
                  |
              Wall Jack
                  |
             User's Switch
                  |
             Other devices
```

The new switch can send BPDUs.

This can potentially affect the STP topology.

---

# 4. BPDU Guard – The Solution

**BPDU Guard** protects ports intended for end hosts.

Its basic rule is:

```text
Port receives BPDU
       ↓
   BPDU Guard
       ↓
Port enters err-disabled state
```

Therefore, if someone connects an unauthorised switch to a PortFast/edge port, the switch can disable that port.

```text
                SW1
                 |
            BPDU Guard
                 |
                 X
                 |
        Unauthorised switch
```

### Main purpose

> **BPDU Guard protects the STP topology from switches being connected to ports intended for end hosts.**

---

# 5. BPDU Guard Configuration

BPDU Guard can be configured in two ways:

1. Per-port
2. Globally for PortFast-enabled ports

---

## 5.1 Per-Port Configuration

Enter the interface configuration mode:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# spanning-tree bpduguard enable
```

This enables BPDU Guard on that particular interface.

---

## 5.2 Global Configuration

BPDU Guard can also be enabled by default on all PortFast/edge ports:

```cisco
SW1(config)# spanning-tree portfast bpduguard default
```

This means:

```text
PortFast / Edge ports
        ↓
   BPDU Guard
        ↓
Applied by default
```

---

## 5.3 Disable BPDU Guard on a Specific Port

If BPDU Guard has been enabled globally, it can be disabled on a specific interface:

```cisco
SW1(config-if)# spanning-tree bpduguard disable
```

---

## 5.4 Checking BPDU Guard

The document demonstrates checking the status with:

```cisco
SW1# show spanning-tree interface g0/1 detail
```

Look for information such as:

```text
The port is in the portfast edge mode
Bpdu guard is enabled
```

---

# 6. BPDU Guard and PortFast

PortFast and BPDU Guard are commonly used together.

```text
             END DEVICE
                 |
                 |
             PortFast
                 +
            BPDU Guard
                 |
                SW1
```

Their purposes are different:

| Feature | Purpose |
|---|---|
| **PortFast** | Quickly places the edge port into Forwarding |
| **BPDU Guard** | Protects the edge port if a BPDU is received |

### Important

BPDU Guard does **not** stop the port from sending BPDUs.

The port can still send BPDUs.

If the port receives a BPDU, BPDU Guard causes the interface to enter **err-disabled** state.

---

# 7. ErrDisable

**ErrDisable** is a Cisco switch feature that places an interface into a disabled state when certain conditions or violations occur.

A BPDU Guard violation is one example.

Other examples include:

- Power policing violations
- Port Security violations
- Dynamic ARP Inspection (DAI) violations

Example:

```text
BPDU received
      ↓
BPDU Guard violation
      ↓
ErrDisable
      ↓
Port disabled
```

The port effectively stops forwarding traffic.

---

# 8. Re-enabling an Err-Disabled Port

Before re-enabling an err-disabled port, the underlying problem should be fixed.

Otherwise:

```text
Re-enable port
      ↓
Problem still exists
      ↓
Violation happens again
      ↓
Port becomes err-disabled again
```

There are two ways to recover the port.

---

## 8.1 Manual Recovery

The interface can be manually reset using:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# shutdown
SW1(config-if)# no shutdown
```

The basic process is:

```text
shutdown
   ↓
no shutdown
   ↓
Port comes back
```

---

# 9. ErrDisable Recovery

ErrDisable Recovery can automatically re-enable a port after a configured period.

The document notes that the default recovery timer is:

```text
300 seconds
```

which is:

```text
5 minutes
```

ErrDisable Recovery is disabled by default.

---

## Check ErrDisable Recovery

```cisco
SW1# show errdisable recovery
```

This command displays the recovery status and timer.

---

## Enable BPDU Guard Recovery

To enable automatic recovery for BPDU Guard violations:

```cisco
SW1(config)# errdisable recovery cause bpduguard
```

---

## Change the Recovery Interval

For example:

```cisco
SW1(config)# errdisable recovery interval 600
```

This sets the recovery interval to:

```text
600 seconds
= 10 minutes
```

---

## Recovery Process

```text
BPDU received
      ↓
BPDU Guard
      ↓
ErrDisable
      ↓
Fix underlying problem
      ↓
ErrDisable Recovery timer
      ↓
Port automatically re-enabled
```

### Important

Automatic recovery does not fix the original problem.

The underlying problem should still be solved.

---

# 10. BPDU Filter

## What is BPDU Filter?

BPDU Filter prevents a port from sending BPDUs.

The document describes BPDU Filter as a feature that:

> Stops a port from sending BPDUs or processing received BPDUs.

BPDU Filter can be configured:

- Per-port
- As a default for PortFast/edge ports

---

# 11. BPDU Filter – The Problem

A switch port connected to an end host can continue sending BPDUs approximately every 2 seconds.

```text
SW1
 |
 | BPDU
 ↓
PC
```

For a normal end-host connection, these BPDUs are unnecessary.

The document identifies two reasons:

1. Sending BPDUs uses some bandwidth and switch processing.
2. BPDUs contain information about the LAN's STP topology.

Therefore, BPDU Filter can be used when preventing BPDUs from being sent is required.

---

# 12. BPDU Filter – Per-Port Configuration

To enable BPDU Filter directly on an interface:

```cisco
SW1(config)# interface g0/1
SW1(config-if)# spanning-tree bpdufilter enable
```

With this configuration:

```text
Port
 ↓
BPDU Filter
 ↓
Does not send BPDUs
 ↓
Ignores received BPDUs
```

The document warns:

> Use with caution!

Because this configuration effectively disables STP processing on the port.

---

## Disable Per-Port BPDU Filter

```cisco
SW1(config-if)# spanning-tree bpdufilter disable
```

---

# 13. BPDU Filter – Global Default

BPDU Filter can also be enabled by default on PortFast/edge ports:

```cisco
SW1(config)# spanning-tree portfast bpdufilter default
```

This activates BPDU Filter on PortFast-enabled ports.

---

## What happens if a BPDU is received?

When BPDU Filter is enabled through the global PortFast/edge configuration and the port receives a BPDU:

```text
BPDU received
      ↓
PortFast disabled
      ↓
BPDU Filter disabled
      ↓
Port operates as normal STP port
```

This is different from the per-port BPDU Filter configuration.

---

# 14. BPDU Filter vs BPDU Guard

These two features are easy to confuse.

| Feature | BPDU Guard | BPDU Filter |
|---|---|---|
| Main purpose | Protect the port from BPDUs | Prevent/ignore BPDUs |
| Sends BPDUs normally? | Yes | Depends on configuration |
| BPDU received | Port becomes err-disabled | Behaviour depends on how Filter was configured |
| Protects against an unauthorised switch? | Yes | Not in the same way |
| Use with PortFast? | Common | Possible, but use carefully |

### Easy memory trick

```text
BPDU GUARD
"Don't send me a BPDU!"
        ↓
BPDU received
        ↓
🚨 SHUT THE PORT DOWN
```

```text
BPDU FILTER
"Don't send/process BPDUs here."
```

---

# 15. BPDU Guard + BPDU Filter

The document also discusses using BPDU Guard and BPDU Filter together.

If BPDU Filter is enabled through the **global configuration** and the port receives a BPDU:

```text
BPDU received
      ↓
BPDU Filter disabled
      ↓
BPDU Guard triggered
      ↓
ErrDisable
```

However, if BPDU Filter is enabled directly on the interface:

```cisco
spanning-tree bpdufilter enable
```

and the port receives a BPDU:

```text
BPDU received
      ↓
BPDU ignored
      ↓
BPDU Guard is not triggered
```

Therefore, the configuration method matters.

---

# 16. Recommended Use of BPDU Filter

The document recommends:

- Enable PortFast and BPDU Guard.
- BPDU Filter can be enabled by default when required.
- Avoid enabling BPDU Filter directly per-port unless there is a good reason.

The important reason is that per-port BPDU Filter can cause the port to ignore BPDUs and effectively bypass normal STP protection.

---

# 17. Root Bridge Placement

STP prevents Layer 2 loops by electing a **Root Bridge**.

The Root Bridge should not simply be selected randomly.

The document identifies several things to consider:

### Optimal traffic flow

Traffic should ideally take efficient paths.

### Minimise latency

The Root Bridge should help avoid unnecessarily long paths.

### Minimise congestion

The topology should avoid creating unnecessary traffic concentration.

### Stability and reliability

The Root Bridge should be placed on a stable and reliable part of the network.

---

# 18. Root Guard

## The Problem

Within your own LAN, you can normally control the Root Bridge by configuring the bridge priority.

For example:

```text
Lower Bridge Priority
        ↓
Better chance of becoming Root Bridge
```

However, sometimes your switches connect to switches outside your direct control.

Examples include:

- Service provider networks
- Metro Ethernet
- Other external/customer networks

Example:

```text
          Service Provider
                 |
        ┌────────┴────────┐
        │                 │
       SW1               SW2
     Customer          Customer
        LAN               LAN
```

An external switch could potentially send a **superior BPDU**.

---

# 19. What is a Superior BPDU?

A superior BPDU is a BPDU that is better according to the STP algorithm.

For example, it may advertise:

- A better Root Bridge
- A lower Root Bridge ID
- A better path to the Root Bridge

Without protection, switches may accept the external switch as the Root Bridge.

This can change the STP topology and potentially cause inefficient traffic paths.

---

# 20. Root Guard – The Solution

**Root Guard** prevents a port from becoming a Root Port because of superior BPDUs.

It is normally configured on ports connected to switches outside your control.

Example:

```text
Your LAN                    External network

 SW1
  |
  |
 SW2 ----------- SW6
                 |
          "I should be Root!"
                 ↓
           Superior BPDU
```

Root Guard protects the customer LAN from accepting the external switch as the Root Bridge.

---

# 21. Root Guard Configuration

Root Guard is configured per interface.

```cisco
SW2(config)# interface g0/2
SW2(config-if)# spanning-tree guard root
```

Another example:

```cisco
SW3(config)# interface g0/2
SW3(config-if)# spanning-tree guard root
```

Unlike PortFast/BPDU Guard and Loop Guard, the document notes that there is **no global default command** for Root Guard.

---

# 22. Root Guard Violation

If a Root Guard-enabled port receives a superior BPDU:

```text
Superior BPDU
      ↓
Root Guard
      ↓
Root Inconsistent
      ↓
Port stops forwarding
```

Cisco may display states such as:

```text
BKN
ROOT_Inc
```

Where:

```text
BKN      = Broken
ROOT_Inc = Root Inconsistent
```

The port is effectively blocked by STP.

---

# 23. Root Guard Recovery

A Root Guard port does not require a manual `shutdown` / `no shutdown` once the superior BPDU problem has been resolved.

The port will recover automatically after it stops receiving superior BPDUs and those BPDUs age out.

The document notes:

```text
BPDU Max Age = 20 seconds by default
```

Simplified process:

```text
Superior BPDU received
        ↓
Root Guard
        ↓
Root Inconsistent
        ↓
Port blocks
        ↓
Superior BPDU stops
        ↓
BPDU ages out
        ↓
Port automatically recovers
```

---

# 24. Root Guard – Important Concept

Root Guard protects the Root Bridge placement.

Think:

```text
ROOT GUARD
     ↓
"Don't let this external switch become Root."
```

### Memory trick

> **Root Guard protects who can become Root.**

---

# 25. Loop Guard

## The Problem

Loop Guard protects the network from Layer 2 loops caused by an STP port unexpectedly stopping its reception of BPDUs.

A common cause is a **unidirectional link**.

---

# 26. Unidirectional Links

A unidirectional link is a network link where data transmission works in only one direction.

For example:

```text
SW1 ─────────── SW2
 ↑                X
 │                │
Frames work       Frames don't work
in this direction
```

SW1 may be able to send frames to SW2, while SW2 cannot successfully send frames back to SW1.

---

# 27. Causes of Unidirectional Links

Unidirectional links are typically caused by Layer 1 physical problems.

Examples include:

- Damaged cables
- Faulty connectors
- Faulty transceivers
- Fibre-optic problems

They are more common with fibre-optic links because fibre connections normally use separate fibres for transmitting and receiving.

```text
Fibre link

SW1 ================= SW2
     TX ----------> RX
     RX <---------- TX
```

If one fibre is damaged:

```text
SW1 ================= SW2
     TX ----------> RX     ✓
     RX <---------- TX     X
```

communication may become unidirectional.

---

# 28. Why Unidirectional Links Are Dangerous for STP

Normally, BPDUs are generated by the Root Bridge and forwarded through Designated Ports.

Consider:

```text
        SW1
       /   \
      /     \
    SW2-----SW3
```

Suppose SW3 has a blocking/non-designated port because it receives superior BPDUs from SW2.

```text
SW2 ───────── SW3
             X
        Blocking
```

Now imagine the link becomes unidirectional.

SW2's BPDUs can no longer reach SW3.

SW3 may stop receiving BPDUs.

---

# 29. The Loop Guard Problem

Without Loop Guard:

```text
SW2's BPDUs stop reaching SW3
             ↓
SW3 stops receiving BPDUs
             ↓
STP assumes something has changed
             ↓
Port can become Designated
             ↓
Port starts Forwarding
```

SW3 can start sending BPDUs.

SW2 may receive SW3's inferior BPDUs and ignore them because SW2 still has the superior STP information.

The result can be:

```text
        SW1
       /   \
      /     \
    SW2-----SW3
       \_____/
        LOOP
```

Both paths can end up forwarding.

This can create a **Layer 2 loop**.

---

# 30. Loop Guard – The Solution

Loop Guard prevents a port from incorrectly becoming a Designated Port when BPDUs unexpectedly stop arriving.

With Loop Guard:

```text
BPDU reception stops
        ↓
Max Age timer expires
        ↓
Loop Guard
        ↓
Loop Inconsistent
        ↓
Port remains blocked
```

Instead of allowing the port to transition to Forwarding, Loop Guard places it into the **Broken / Loop Inconsistent** state.

---

# 31. Loop Guard State

The document describes the port as entering:

```text
Loop Inconsistent
```

This blocks the port.

An important detail is:

```text
Root Inconsistent / Loop Inconsistent
```

are STP blocking conditions.

The interface can remain:

```text
up/up
```

while STP continues to block the port.

---

# 32. Loop Guard Recovery

If the port starts receiving BPDUs again:

```text
BPDUs return
     ↓
Loop Guard detects them
     ↓
Loop Inconsistent condition clears
     ↓
Port automatically recovers
```

No manual `shutdown` / `no shutdown` is normally required.

---

# 33. Loop Guard Configuration

Loop Guard can be enabled in two ways.

---

## 33.1 Per-Port

```cisco
SW3(config)# interface g0/1
SW3(config-if)# spanning-tree guard loop
```

---

## 33.2 Global Default

```cisco
SW3(config)# spanning-tree loopguard default
```

This enables Loop Guard by default on appropriate STP ports.

---

## 33.3 Disable Loop Guard on a Specific Port

If Loop Guard has been enabled globally:

```cisco
SW3(config-if)# spanning-tree guard none
```

This disables the guard feature on that interface.

---

# 34. Loop Guard and Root Guard

**Root Guard and Loop Guard are mutually exclusive on the same port.**

They protect against different STP problems.

### Root Guard

Root Guard prevents a port from becoming a **Root Port** because of a superior BPDU.

```text
Superior BPDU
      ↓
Root Guard
      ↓
Root Inconsistent
```

### Loop Guard

Loop Guard prevents a **Root/Non-Designated port** from becoming a Designated Port because BPDUs unexpectedly stop arriving.

```text
BPDUs disappear
      ↓
Loop Guard
      ↓
Loop Inconsistent
```

---

# 35. Root Guard vs Loop Guard

| Feature | Root Guard | Loop Guard |
|---|---|---|
| Main protection | Protects Root Bridge placement | Protects against Layer 2 loops |
| Trigger | Superior BPDU received | Expected BPDUs stop arriving |
| Prevents | Port becoming Root Port | Port becoming Designated Port |
| Result | Root Inconsistent | Loop Inconsistent |
| Automatic recovery | Yes | Yes |
| Same port simultaneously? | No | No |

---

# 36. Why Root Guard and Loop Guard Are Different

Think about the direction of the STP problem.

```text
                 ROOT GUARD
                     ↓
          "Someone is claiming
             to be better Root"
                     ↓
              Superior BPDU
```

Whereas:

```text
                 LOOP GUARD
                     ↓
          "I expected BPDUs,
             but they disappeared"
                     ↓
             Possible loop
```

### Easy memory trick

```text
ROOT GUARD
"Don't let another switch become Root."

LOOP GUARD
"Don't let a blocked port become Forwarding
just because BPDUs disappeared."
```

---

# 37. Root Guard + Loop Guard Example

A topology may use both features on **different interfaces**.

For example:

```text
                  External Switch
                       SW6
                        |
                        |
                    Root Guard
                        |
                        |
          ┌─────────────SW2
          │
          │
      Loop Guard
          │
          │
         SW3
```

Example configuration:

```text
SW2 G0/0 → Loop Guard
SW2 G0/1 → Loop Guard
SW2 G0/2 → Root Guard
```

The important point is:

> Root Guard and Loop Guard can coexist in the network, but they should not be configured on the same port.

---

# 38. Specific Configuration vs Global Configuration

The document highlights that more specific interface configuration can take precedence over a global default.

For example:

```cisco
SW1(config)# spanning-tree loopguard default
```

enables Loop Guard by default.

But on a specific interface:

```cisco
SW1(config)# interface g0/2
SW1(config-if)# spanning-tree guard root
```

Root Guard is configured specifically on that interface.

Therefore, the interface-level configuration determines the guard behaviour for that port.

---

# 39. STP Protection Features – Big Picture

The four major features can be remembered like this:

```text
                    STP PROTECTION
                          |
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ↓                 ↓                 ↓
   BPDU GUARD        BPDU FILTER       ROOT GUARD
        │                 │                 │
        │                 │                 │
  BPDU received       Filter BPDUs     Superior BPDU
        │                 │                 │
        ↓                 ↓                 ↓
  ERR-DISABLED       Ignore/filter     ROOT INCONSISTENT
                                         

                          +
                          
                     LOOP GUARD
                          │
                   BPDUs disappear
                          │
                          ↓
                  LOOP INCONSISTENT
```

---

# 40. Quick Comparison

| Feature | Question it answers |
|---|---|
| **PortFast** | "Can this end-device port go to Forwarding immediately?" |
| **BPDU Guard** | "What if a BPDU appears on my PortFast/edge port?" |
| **BPDU Filter** | "Can I prevent/filter BPDUs on this port?" |
| **Root Guard** | "What if an external switch claims to be a better Root Bridge?" |
| **Loop Guard** | "What if BPDUs unexpectedly disappear from a port?" |
| **ErrDisable** | "What happens when a serious port violation occurs?" |
| **ErrDisable Recovery** | "Can the err-disabled port automatically recover?" |

---

# 41. The Most Important Differences

## PortFast

```text
End device
    ↓
PortFast
    ↓
Immediate Forwarding
```

**Purpose:** Speed up edge-port activation.

---

## BPDU Guard

```text
BPDU received
      ↓
BPDU Guard
      ↓
ErrDisabled
```

**Purpose:** Protect an edge/end-host port from an unexpected switch.

---

## BPDU Filter

```text
BPDU
 ↓
BPDU Filter
 ↓
Prevent / filter BPDU processing
```

**Purpose:** Prevent or filter BPDUs.

**Use with caution**, especially when configured directly on a port.

---

## Root Guard

```text
Superior BPDU
      ↓
Root Guard
      ↓
Root Inconsistent
      ↓
Port blocked
```

**Purpose:** Protect the Root Bridge placement.

---

## Loop Guard

```text
BPDUs unexpectedly disappear
             ↓
         Loop Guard
             ↓
      Loop Inconsistent
             ↓
        Port blocked
```

**Purpose:** Prevent a port from incorrectly moving to Forwarding and creating a Layer 2 loop.

---

# 42. Important Cisco Commands

## PortFast

```cisco
interface g0/1
 spanning-tree portfast
```

---

## BPDU Guard – Per Port

```cisco
interface g0/1
 spanning-tree bpduguard enable
```

---

## BPDU Guard – Default on PortFast Ports

```cisco
spanning-tree portfast bpduguard default
```

---

## Disable BPDU Guard

```cisco
interface g0/1
 spanning-tree bpduguard disable
```

---

## BPDU Filter – Per Port

```cisco
interface g0/1
 spanning-tree bpdufilter enable
```

---

## Disable BPDU Filter

```cisco
interface g0/1
 spanning-tree bpdufilter disable
```

---

## BPDU Filter – Default on PortFast Ports

```cisco
spanning-tree portfast bpdufilter default
```

---

## Root Guard

```cisco
interface g0/2
 spanning-tree guard root
```

---

## Loop Guard – Per Port

```cisco
interface g0/1
 spanning-tree guard loop
```

---

## Loop Guard – Default

```cisco
spanning-tree loopguard default
```

---

## Disable Guard on a Port

```cisco
interface g0/1
 spanning-tree guard none
```

---

## ErrDisable Recovery – BPDU Guard

```cisco
errdisable recovery cause bpduguard
```

---

## Change ErrDisable Recovery Timer

```cisco
errdisable recovery interval 600
```

---

## Check ErrDisable Recovery

```cisco
show errdisable recovery
```

---

## Check STP Interface Details

```cisco
show spanning-tree interface g0/1 detail
```

---

# 43. STP Protection Memory Map

A simple way to remember all of these features:

```text
                    STP
                     |
       ┌─────────────┼─────────────┐
       │             │             │
       ↓             ↓             ↓
   END DEVICE     EXTERNAL       LINK FAILURE
       │           SWITCH             │
       │             │                │
       ↓             ↓                ↓
   PORTFAST      ROOT GUARD       LOOP GUARD
       │             │                │
       ↓             ↓                ↓
 Immediate       Protect Root      Protect
 Forwarding      Bridge            against loops
       │
       ↓
  BPDU GUARD
       │
       ↓
 BPDU received
       │
       ↓
 ERR-DISABLED
```

---

# 44. Exam Memory Tricks

### PortFast

> **PortFast = Fast Forwarding for edge ports**

---

### BPDU Guard

> **BPDU Guard = BPDU arrives → shut the port down**

```text
BPDU → Guard → ErrDisabled
```

---

### BPDU Filter

> **BPDU Filter = Filter the BPDUs**

---

### Root Guard

> **Root Guard = Protect the Root**

```text
Superior BPDU
      ↓
Root Guard
      ↓
Root Inconsistent
```

---

### Loop Guard

> **Loop Guard = Protect against missing BPDUs and possible loops**

```text
BPDUs disappear
      ↓
Loop Guard
      ↓
Loop Inconsistent
```

---

# 45. Final Summary

The STP protection toolkit provides different protections for different problems.

### PortFast

Allows ports connected to end hosts to immediately enter the STP Forwarding state, bypassing Listening and Learning.

### BPDU Guard

Protects PortFast/edge ports from unexpected BPDUs. If a BPDU is received, the port enters the err-disabled state.

### BPDU Filter

Prevents or filters BPDUs. It should be used carefully because certain configurations can effectively bypass normal STP processing.

### Root Guard

Protects the Root Bridge placement by preventing a port from becoming a Root Port because of a superior BPDU.

### Loop Guard

Protects against Layer 2 loops when a port unexpectedly stops receiving BPDUs.

### ErrDisable

Disables a port after certain violations, such as a BPDU Guard violation.

### ErrDisable Recovery

Allows an err-disabled port to automatically recover after a configured timer, provided the underlying problem has been resolved.

---

# 46. One-Page Revision Sheet

```text
┌───────────────────────────────────────────────────────────┐
│                    STP PROTECTION                         │
├───────────────────────────────────────────────────────────┤
│                                                           │
│ PORTFAST                                                  │
│ → End-device/edge port                                   │
│ → Immediately Forwarding                                 │
│                                                           │
│ BPDU GUARD                                                │
│ → Unexpected BPDU received                               │
│ → ErrDisabled                                             │
│                                                           │
│ BPDU FILTER                                               │
│ → Filters/prevents BPDUs                                  │
│ → Use carefully                                           │
│                                                           │
│ ROOT GUARD                                                │
│ → Superior BPDU received                                  │
│ → Root Inconsistent                                       │
│ → Protects Root Bridge placement                          │
│                                                           │
│ LOOP GUARD                                                │
│ → Expected BPDUs disappear                                │
│ → Loop Inconsistent                                       │
│ → Prevents possible Layer 2 loop                          │
│                                                           │
│ ERRDISABLE RECOVERY                                       │
│ → Automatically recovers err-disabled ports              │
│                                                           │
└───────────────────────────────────────────────────────────┘
```

---

# 47. Final Mental Model

If you remember nothing else, remember this:

```text
PORTFAST
"Let my end device start quickly."

        ↓

BPDU GUARD
"If a BPDU appears here, shut the port."

        ↓

BPDU FILTER
"Don't send/process BPDUs here."

        ↓

ROOT GUARD
"Don't let an external switch become Root."

        ↓

LOOP GUARD
"If BPDUs disappear, don't allow a blocked
port to incorrectly start forwarding."

        ↓

ERRDISABLE
"The port is disabled because a violation occurred."

        ↓

ERRDISABLE RECOVERY
"Automatically bring it back after the timer
once the problem has been resolved."
```

## Key Cisco Commands to Remember

```cisco
! BPDU Guard
spanning-tree bpduguard enable

! BPDU Guard on PortFast ports by default
spanning-tree portfast bpduguard default

! BPDU Filter
spanning-tree bpdufilter enable

! BPDU Filter on PortFast ports by default
spanning-tree portfast bpdufilter default

! Root Guard
spanning-tree guard root

! Loop Guard
spanning-tree guard loop

! Loop Guard by default
spanning-tree loopguard default

! Disable guard on an interface
spanning-tree guard none

! ErrDisable Recovery
errdisable recovery cause bpduguard

! Change recovery timer
errdisable recovery interval 600

! Check recovery
show errdisable recovery

! Check STP interface details
show spanning-tree interface g0/1 detail
```

---

**End of BPDU Guard, BPDU Filter, Root Guard & Loop Guard notes**
