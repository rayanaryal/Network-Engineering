# Hot Standby Router Protocol (HSRP)

This section documents my understanding and hands-on practice with **HSRP (Hot Standby Router Protocol)**.

HSRP is a Cisco First Hop Redundancy Protocol (FHRP) used to provide **default-gateway redundancy**.

Without gateway redundancy, hosts may lose connectivity to remote networks if their configured default gateway becomes unavailable.

---

## Why HSRP Is Needed

Consider a LAN where every PC uses one router as its default gateway:

```text
PC1 ----\
PC2 ----- SW1 ----- R1 ----- Outside Networks
PC3 ----/            ^
                      |
                Default Gateway
```

If `R1` fails, the PCs may still communicate within their local subnet, but they lose their path to remote networks.

The default gateway has become a:

```text
Single Point of Failure
```

Adding a second router provides physical redundancy:

```text
                 R1
                /
PCs ----- SW1
                \
                 R2
```

However, the hosts still need **one default-gateway IP address**.

HSRP solves this by allowing the routers to present a **virtual default gateway** to the hosts.

---

## HSRP Virtual Gateway

Conceptually:

```text
               R1
             Active
               |
               |
PCs ---- SW1 --+---- Virtual Gateway
               |
               |
             Standby
               R2
```

The hosts use the **virtual IP address** as their default gateway rather than depending directly on the physical interface address of one router.

For example:

```text
R1 address:      192.168.10.2
R2 address:      192.168.10.3
HSRP virtual IP: 192.168.10.1
```

The PCs configure:

```text
Default Gateway = 192.168.10.1
```

If the Active HSRP router becomes unavailable, another HSRP router can take over responsibility for the virtual gateway.

---

## Active and Standby Routers

HSRP uses important roles including:

```text
Active Router
Standby Router
```

The **Active Router** currently forwards traffic sent to the HSRP virtual gateway.

The **Standby Router** is prepared to take over if the Active Router fails.

Conceptually:

```text
Normal Operation

PC
 |
SW1
 |
 +---- R1  ACTIVE
 |
 +---- R2  STANDBY


If R1 fails:

PC
 |
SW1
 |
 +---- R1  FAILED
 |
 +---- R2  ACTIVE
```

The objective is to maintain default-gateway availability even when one physical gateway device becomes unavailable.

---

> **Key takeaway:** HSRP separates the default gateway used by end devices from a single physical router by providing a redundant virtual gateway.




---

## HSRP Priority

When multiple routers participate in the same HSRP group, HSRP needs to determine which router should become the **Active Router**.

One important value used for this decision is:

```text
HSRP Priority
```

The default HSRP priority is:

```text
100
```

Unlike STP bridge priority, where the **lowest value wins**, HSRP prefers the:

```text
Highest Priority
```

For example:

```text
R1 Priority = 110
R2 Priority = 100

        ↓

R1 becomes Active
R2 becomes Standby
```

This is an important distinction:

```text
STP Root Bridge Election
Lowest priority preferred

HSRP Active Router Election
Highest priority preferred
```

---

## Configuring HSRP Priority

A router can be given a higher HSRP priority to make it the preferred Active Router.

For example:

```cisco
interface GigabitEthernet0/0
 standby 1 priority 110
```

Here:

```text
1   = HSRP group number
110 = HSRP priority
```

If the other router remains at the default priority of `100`, R1 has the preferred HSRP priority.

---

## What Is Preemption?

Priority alone does not necessarily mean that a preferred router will immediately take back the Active role after recovering from a failure.

This is where **preemption** becomes important.

Preemption allows a router with a higher HSRP priority to take over the Active role when it becomes available.

It can be configured with:

```cisco
standby 1 preempt
```

---

## Example Failover and Recovery

Suppose:

```text
R1 Priority = 110
R2 Priority = 100
```

Initially:

```text
R1 = Active
R2 = Standby
```

If R1 fails:

```text
R1 = Down
R2 = Active
```

R2 takes responsibility for the virtual gateway.

Later, R1 comes back online.

With preemption configured:

```text
R1 returns
    ↓
R1 has higher priority
    ↓
R1 preempts R2
    ↓
R1 = Active
R2 = Standby
```

Without preemption, the currently Active router may remain Active even after the higher-priority router returns.

---

## Priority and Preemption Together

A useful way for me to remember the difference is:

```text
Priority
   ↓
"Which router is preferred?"


Preemption
   ↓
"Can the preferred router take the Active role back?"
```

Therefore, a common configuration on the preferred router could be:

```cisco
interface GigabitEthernet0/0
 standby 1 priority 110
 standby 1 preempt
```

---

## HSRP Election Logic

My simplified HSRP decision process is:

```text
Routers join the same HSRP group
              ↓
Compare HSRP priority
              ↓
Higher priority preferred
              ↓
Active Router selected
              ↓
Standby Router waits
              ↓
Active fails → Standby takes over
              ↓
Preferred router returns
              ↓
Preemption determines whether it takes Active back
```

> **Key takeaway:** HSRP priority determines which router is preferred to become Active, while preemption allows a higher-priority router to reclaim the Active role after it becomes available again.


---

## HSRP Group Number

HSRP configuration uses a **group number** to associate routers that are providing redundancy for the same virtual gateway.

For example:

```cisco
standby 1 ip 192.168.10.1
```

Here:

```text
standby = HSRP configuration
1       = HSRP group number
192.168.10.1 = Virtual IP address
```

Routers participating in the same HSRP group must be configured consistently for that virtual gateway.

---

## Configuring the Virtual IP Address

Consider two routers:

```text
R1 Physical IP = 192.168.10.2
R2 Physical IP = 192.168.10.3

HSRP Virtual IP = 192.168.10.1
```

The end devices do not use either physical router address as their default gateway.

Instead:

```text
PC Default Gateway = 192.168.10.1
```

The virtual IP represents the redundant gateway service provided by the HSRP routers.

---

## Example Two-Router Configuration

### R1 - Preferred Active Router

```cisco
interface GigabitEthernet0/0
 ip address 192.168.10.2 255.255.255.0
 standby 1 ip 192.168.10.1
 standby 1 priority 110
 standby 1 preempt
 no shutdown
```

R1 has:

```text
Physical IP = 192.168.10.2
HSRP VIP    = 192.168.10.1
Priority    = 110
Preempt     = Enabled
```

Therefore, R1 is intended to be the preferred Active Router.

---

### R2 - Standby Router

```cisco
interface GigabitEthernet0/0
 ip address 192.168.10.3 255.255.255.0
 standby 1 ip 192.168.10.1
 standby 1 priority 100
 no shutdown
```

R2 has:

```text
Physical IP = 192.168.10.3
HSRP VIP    = 192.168.10.1
Priority    = 100
```

Under normal conditions:

```text
              192.168.10.1
              Virtual Gateway
                    |
            +-------+-------+
            |               |
           R1              R2
      192.168.10.2     192.168.10.3
       Priority 110     Priority 100
          ACTIVE          STANDBY
```

---

## What the PC Sees

The PC does not need to know which physical router is currently Active.

Its configuration remains:

```text
IP Address:      192.168.10.x
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
```

If R1 fails:

```text
R1 fails
   ↓
R2 becomes Active
   ↓
192.168.10.1 remains the gateway
   ↓
PC configuration does not change
```

This separation between the **physical router addresses** and the **virtual gateway address** is the central idea behind HSRP.

---

## Complete Logic

I can now think of the configuration as four separate pieces:

```text
HSRP Group
     ↓
Which routers belong together?

Virtual IP
     ↓
Which gateway address do hosts use?

Priority
     ↓
Which router is preferred as Active?

Preemption
     ↓
Can the preferred router reclaim Active status?
```

> **Key takeaway:** The physical router interfaces keep their own unique IP addresses, while routers in the same HSRP group cooperate to provide a shared virtual IP address that hosts use as their default gateway.


---

## HSRP States

HSRP routers move through a number of states while determining their role within an HSRP group.

The important states are:

```text
Initial
Learn
Listen
Speak
Standby
Active
```

A simplified view is:

```text
Initial
   ↓
Learn
   ↓
Listen
   ↓
Speak
   ↓
Standby
   ↓
Active
```

The two states I care about most during normal operation are:

```text
Active
Standby
```

The **Active Router** currently forwards traffic for the virtual gateway.

The **Standby Router** is ready to take over if the Active Router fails.

---

## Verifying HSRP

The primary verification command is:

```cisco
show standby
```

A shorter summary can be displayed with:

```cisco
show standby brief
```

These commands allow me to verify:

```text
HSRP group number
Current state
Priority
Preemption
Active router
Standby router
Virtual IP address
```

---

## Example Verification Output

A typical summary may look like:

```text
Interface   Grp  Pri  P  State    Active           Standby          Virtual IP
Gi0/0       1    110  P  Active   local            192.168.10.3     192.168.10.1
```

This tells me:

```text
Group      = 1
Priority   = 110
Preempt    = Enabled
State      = Active
Active     = local router
Standby    = 192.168.10.3
Virtual IP = 192.168.10.1
```

On the other router, I would expect something similar to:

```text
Interface   Grp  Pri  P  State     Active           Standby   Virtual IP
Gi0/0       1    100     Standby   192.168.10.2     local     192.168.10.1
```

---

## Interpreting the Output

If the output shows:

```text
State = Active
```

that router currently owns responsibility for forwarding traffic sent to the HSRP virtual gateway.

If the output shows:

```text
State = Standby
```

that router is prepared to take over if the Active Router becomes unavailable.

The word:

```text
local
```

means the router on which I am running the command.

---

## Testing HSRP Failover

A useful lab test is to deliberately shut down the Active router interface.

For example:

```cisco
interface GigabitEthernet0/0
 shutdown
```

I can then check the second router:

```cisco
show standby brief
```

The expected result is:

```text
Standby
   ↓
Active
```

The virtual IP remains the same:

```text
192.168.10.1
```

The host therefore continues using the same default gateway.

---

## Testing Recovery and Preemption

After restoring the preferred router:

```cisco
interface GigabitEthernet0/0
 no shutdown
```

if the router has:

```cisco
standby 1 priority 110
standby 1 preempt
```

it can reclaim the Active role because it has the higher priority.

The sequence becomes:

```text
R1 Active
   ↓
R1 fails
   ↓
R2 becomes Active
   ↓
R1 returns
   ↓
R1 has higher priority + preempt
   ↓
R1 becomes Active again
```

---

> **Key takeaway:** `show standby` and `show standby brief` allow me to verify not only whether HSRP is configured, but which router is Active, which is Standby, whether preemption is enabled, and which virtual gateway is being protected.

















