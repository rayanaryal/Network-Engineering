# Access Control Lists (ACLs)

This section documents my study and hands-on practice with **Access Control Lists (ACLs)** in Cisco networks.

ACLs provide a way to control network traffic by defining rules that determine which packets are **permitted** and which packets are **denied**.

> **Status:** Work in progress — I will continue expanding this section as I study and test additional ACL concepts.

---

## Topics Covered So Far

- Introduction to ACLs
- Permit and deny rules
- Source and destination matching
- Wildcard masks
- Applying ACLs to interfaces
- Inbound and outbound direction
- Basic extended ACL syntax
- Hands-on ACL topology

---

## What Is an ACL?

An **Access Control List (ACL)** is a traffic-filtering mechanism that can be used on a router or Layer 3 switch.

A useful way to think about an ACL is as a security guard positioned in the traffic path asking:

```text
What traffic is this?
        ↓
Where did it come from?
        ↓
Where is it going?
        ↓
Is it allowed through?
```

The ACL then makes a decision:

```text
Packet
   ↓
ACL Rule
   ↓
Permit or Deny
```

ACLs therefore allow an administrator to enforce network access policies rather than allowing all routed traffic to pass unrestricted.

---

## Example Security Policy

One example from my study is a network containing different departments.

Suppose:

```text
Sales → Server VLAN     Allowed
Sales → HR Network      Denied
```

An ACL can enforce this policy by matching the relevant source and destination networks and then permitting or denying the traffic.

For example:

```cisco
access-list 100 deny ip 192.168.1.128 0.0.0.31 192.168.1.160 0.0.0.15
access-list 100 permit ip any any
```

Conceptually:

```text
Traffic from specified source
             ↓
   Destination HR network?
        /           \
      Yes            No
       ↓              ↓
     DENY        Continue checking
```

The following rule:

```cisco
access-list 100 permit ip any any
```

then permits other IP traffic matched by that statement.

---

## ACL Direction

An ACL is applied to an interface in a particular direction:

```text
Inbound  (in)
Outbound (out)
```

Conceptually:

```text
                Router
                   |
IN → [Interface] → Routing Decision
                   |
                   ↓
                  OUT
```

The direction determines where packets encounter the ACL relative to the interface.

Understanding this becomes important when deciding **where an ACL should be placed in the network**.

---

> **Current lesson:** ACLs allow me to translate a network security policy into permit and deny rules that control traffic based on defined matching conditions.
