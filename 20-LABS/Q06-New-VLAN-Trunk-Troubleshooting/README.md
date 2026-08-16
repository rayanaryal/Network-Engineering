# VLAN Trunk Troubleshooting Lab

## Scenario

A newly added VLAN is not passing traffic across an existing trunk link.

This lab builds a working two-site network using VLANs, 802.1Q trunking, Router-on-a-Stick (ROAS), VLSM, static routing, and DHCP.

After verifying that the original network is fully operational, VLAN 50 is introduced into the existing network. The new VLAN initially fails to obtain DHCP connectivity because it is not permitted across the required trunk links.

The issue is then diagnosed using Cisco IOS verification commands and resolved by updating the trunk's allowed VLAN list.

## Main Troubleshooting Question

> Why can devices in the existing VLANs communicate successfully while hosts in the newly added VLAN 50 cannot reach their gateway or obtain an IP address through DHCP?

## Network Topology

The lab consists of two separate LAN sites connected through two routers.

### Left Site

- VLAN 10 — HR
- VLAN 20 — Sales
- VLAN 50 — NEW_VLAN
- Two Layer 2 switches
- Router R1

### Right Site

- VLAN 30 — Management
- VLAN 40 — Engineers
- Two Layer 2 switches
- Router R2

### WAN Connection

R1 and R2 are connected using the `11.0.0.0/30` network.

```text
LEFT SITE                                      RIGHT SITE

VLAN 10 - HR                                  VLAN 30 - Management
VLAN 20 - Sales                               VLAN 40 - Engineers
VLAN 50 - NEW_VLAN
      |                                              |
     SW2                                            SW4
      |                                              |
   [TRUNK]                                        [TRUNK]
      |                                              |
     SW1                                            SW3
      |                                              |
   [TRUNK]                                        [TRUNK]
      |                                              |
     R1 ----------- 11.0.0.0/30 ------------------- R2


## IP Addressing and VLAN Plan

VLSM was used to allocate subnet sizes based on the number of hosts required by each VLAN.

| Site | VLAN | Department | Network | Prefix | Default Gateway |
|---|---:|---|---|---:|---|
| Left | 20 | Sales | 192.168.1.0 | /27 | 192.168.1.1 |
| Left | 10 | HR | 192.168.1.32 | /28 | 192.168.1.33 |
| Left | 50 | NEW_VLAN | 192.168.1.48 | /29 | 192.168.1.49 |
| Right | 30 | Management | 192.168.2.0 | /27 | 192.168.2.1 |
| Right | 40 | Engineers | 192.168.2.32 | /28 | 192.168.2.33 |

### WAN Network

| Connection | Network | R1 Address | R2 Address |
|---|---|---|---|
| R1 ↔ R2 | 11.0.0.0/30 | 11.0.0.1 | 11.0.0.2 |

### VLAN 50 Addressing

VLAN 50 was introduced later as the newly added VLAN used for the troubleshooting scenario.

- **Required hosts:** 5
- **Network:** `192.168.1.48/29`
- **Subnet mask:** `255.255.255.248`
- **Default gateway:** `192.168.1.49`
- **Usable range:** `192.168.1.49 - 192.168.1.54`
- **Broadcast address:** `192.168.1.55`

A `/29` provides 8 total addresses and 6 usable host addresses, which satisfies the five-host requirement.

## Initial Working Configuration

Before introducing VLAN 50, the original network was configured and verified successfully.

The working network included:

- VLAN creation and access-port assignment
- 802.1Q trunking
- Router-on-a-Stick (ROAS)
- Inter-VLAN routing
- Router-to-router WAN connectivity
- Static routing between sites
- DHCP services for each local VLAN
- End-to-end connectivity between the left and right sites

### VLAN and Access Port Configuration

Example VLAN creation:

```cisco
vlan 30
 name Mgmt

vlan 40
 name Eng
```

PC-facing interfaces were configured as access ports:

```cisco
interface fa0/1
 switchport mode access
 switchport access vlan 30
```

Verification:

```cisco
show vlan brief
show interfaces fa0/1 switchport
```

### 802.1Q Trunking

Links between switches and links toward the routers were configured as trunks where multiple VLANs needed to be transported.

Example:

```cisco
interface gigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 30,40
```

Verification:

```cisco
show interfaces trunk
```

### Router-on-a-Stick

Router subinterfaces were used as the Layer 3 gateways for each VLAN.

Example from the right site:

```cisco
interface gigabitEthernet0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.2.1 255.255.255.224

interface gigabitEthernet0/0/0.40
 encapsulation dot1Q 40
 ip address 192.168.2.33 255.255.255.240
```

### WAN Connectivity

The two routers were connected using:

```text
11.0.0.0/30

R1: 11.0.0.1
R2: 11.0.0.2
```

Connectivity was verified with:

```cisco
ping 11.0.0.2
```

The test returned a 100% success rate.

### Static Routing

Static routes were configured so each router could reach the VLAN networks at the remote site.

Example:

```cisco
ip route 192.168.2.0 255.255.255.224 11.0.0.2
ip route 192.168.2.32 255.255.255.240 11.0.0.2
```

Routes were verified using:

```cisco
show ip route
```

### DHCP

Each router was configured to provide DHCP services to its local VLANs.

Example:

```cisco
ip dhcp excluded-address 192.168.2.1

ip dhcp pool Management
 network 192.168.2.0 255.255.255.224
 default-router 192.168.2.1
 dns-server 8.8.8.8
```

After troubleshooting the initial DHCP configuration, clients successfully received their IP configuration dynamically.

### Baseline Verification

Before VLAN 50 was introduced, connectivity was tested across the two sites.

The successful tests confirmed that:

```text
Access VLANs          ✓
802.1Q trunks         ✓
Router-on-a-Stick     ✓
DHCP                  ✓
Static routing        ✓
WAN connectivity      ✓
Cross-site routing    ✓
End-to-end connectivity ✓
```

This established a known-good baseline before introducing the new VLAN.

## Introducing VLAN 50

After confirming that the existing network was fully operational, VLAN 50 was introduced on the left site.

The goal was to simulate the following troubleshooting scenario:

> **A newly added VLAN isn't passing traffic across a trunk link.**

### VLAN 50 Configuration

VLAN 50 was created on SW2:

```cisco
vlan 50
 name NEW_VLAN
```

Ports `Fa0/11-Fa0/15` were assigned as access ports for the new VLAN:

```cisco
interface range fa0/11-15
 switchport mode access
 switchport access vlan 50
 no shutdown
```

Verification:

```cisco
show vlan brief
```

### Router-on-a-Stick for VLAN 50

A new subinterface was created on R1:

```cisco
interface gigabitEthernet0/0/0.50
 encapsulation dot1Q 50
 ip address 192.168.1.49 255.255.255.248
```

This configured `192.168.1.49` as the default gateway for VLAN 50.

### DHCP Configuration

A DHCP pool was created for the new subnet:

```cisco
ip dhcp excluded-address 192.168.1.49

ip dhcp pool NEW_VLAN
 network 192.168.1.48 255.255.255.248
 default-router 192.168.1.49
 dns-server 8.8.8.8
```

A test PC was connected to `Fa0/11` on SW2 and configured as a DHCP client.

### The Failure

The client failed to obtain an IP address:

```text
DHCP request failed
```

Since the original VLANs and network services were already working, the failure indicated that the issue was associated with the newly introduced VLAN 50.

At this point, the configuration was not immediately changed. The network was inspected to identify where VLAN 50 traffic was being blocked.

## Troubleshooting the VLAN 50 Failure

Rather than changing multiple configurations at once, the existing network was inspected systematically.

Since the original VLANs were functioning correctly, attention was focused on the path that the newly created VLAN 50 needed to take.

The expected path was:

```text
VLAN 50 PC
    ↓
Fa0/11 - Access VLAN 50
    ↓
SW2
    ↓
SW2 ↔ SW1 Trunk
    ↓
SW1
    ↓
SW1 ↔ R1 Trunk
    ↓
R1 Gi0/0/0.50
    ↓
DHCP Service
```

### Checking the Trunk

The trunk configuration was inspected using:

```cisco
show interfaces trunk
```

The output showed that the existing trunk allowed only:

```text
Vlans allowed on trunk
Gig0/1    10,20
```

However, the newly created VLAN was:

```text
VLAN 50
```

This immediately identified the problem.

### Root Cause

VLAN 50 had been successfully created and assigned to access ports, but it had **not been added to the allowed VLAN list on the existing trunk links**.

Therefore, VLAN 50 traffic could not traverse the complete Layer 2 path toward the router.

```text
VLAN 10 ──→ Trunk ✓
VLAN 20 ──→ Trunk ✓
VLAN 50 ──→ Trunk ✗
```

This explained why the existing VLANs continued to operate normally while the newly added VLAN failed.

## Corrective Action

VLAN 50 was added to the existing trunk without removing VLANs 10 and 20:

```cisco
switchport trunk allowed vlan add 50
```

The `add` keyword is important when modifying an existing allowed VLAN list.

Before:

```text
10,20
```

After:

```text
10,20,50
```

Using:

```cisco
switchport trunk allowed vlan 50
```

instead would replace the existing allowed VLAN list with VLAN 50 rather than adding VLAN 50 to it.

## Extending VLAN 50 Across the Complete Path

Adding VLAN 50 to only one side of the network path was not sufficient.

Because VLAN 50 traffic needed to travel through SW1 before reaching R1, VLAN 50 also needed to exist on SW1 and be permitted across the required trunk links.

### Create VLAN 50 on SW1

```cisco
vlan 50
 name NEW_VLAN
```

The VLAN database was verified using:

```cisco
show vlan brief
```

### Inspect SW1 Trunks

SW1 had two relevant trunk connections:

```text
SW2
 |
 | Gi0/1
 |
SW1
 |
 | Fa0/24
 |
R1
```

Initially, both trunks permitted only:

```text
10,20
```

VLAN 50 therefore needed to be added to both trunk interfaces.

Because both interfaces required the same configuration, an interface range was used:

```cisco
interface range fa0/24, gigabitEthernet0/1
 switchport trunk allowed vlan add 50
```

### Verify the Trunks

The configuration was checked again:

```cisco
show interfaces trunk
```

The allowed VLAN list now showed:

```text
Fa0/24    10,20,50
Gig0/1    10,20,50
```

VLAN 50 now had a complete Layer 2 path from the access switch toward its default gateway.

## Final Verification

The VLAN 50 client was configured to request an address using DHCP again.

This time:

```text
DHCP successful ✓
```

The successful DHCP request confirmed the complete path:

```text
VLAN 50 PC
    ↓
Fa0/11 - Access VLAN 50
    ↓
SW2
    ↓
Trunk - VLAN 50 allowed
    ↓
SW1
    ↓
Trunk - VLAN 50 allowed
    ↓
R1 Gi0/0/0.50
    ↓
DHCP Pool
    ↓
IP address assigned ✓
```

## Troubleshooting Result

**Problem:** A newly added VLAN could not pass traffic across the existing trunk infrastructure.

**Root Cause:** VLAN 50 was missing from the allowed VLAN lists on the required trunk links.

**Verification Command:**

```cisco
show interfaces trunk
```

**Corrective Command:**

```cisco
switchport trunk allowed vlan add 50
```

**Result:** VLAN 50 successfully reached its router subinterface and the client obtained an IP address through DHCP.


## Troubleshooting Methodology

A major objective of this lab was to troubleshoot systematically rather than immediately changing configuration.

The general troubleshooting process used was:

```text
Physical Connectivity
        ↓
VLAN Existence
        ↓
Access Port Membership
        ↓
802.1Q Trunk Status
        ↓
Allowed VLAN List
        ↓
Router Subinterfaces
        ↓
Default Gateway
        ↓
Routing Table
        ↓
DHCP
        ↓
End-to-End Connectivity
```

This approach helps isolate the layer at which communication is failing before configuration changes are made.

## Key Lessons Learned

- Each VLAN creates a separate Layer 2 broadcast domain.
- PC-facing interfaces are normally configured as access ports.
- Trunk links transport traffic for multiple VLANs using 802.1Q tagging.
- Creating a VLAN on one switch does not automatically make it available throughout the switched network.
- A VLAN must exist on the relevant switches and be permitted across the required trunk links.
- Router-on-a-Stick provides Layer 3 gateways and inter-VLAN routing using router subinterfaces.
- The VLAN ID configured with `encapsulation dot1Q` must match the VLAN being routed.
- `show interfaces trunk` is a key troubleshooting command when VLAN traffic cannot cross a trunk.
- `switchport trunk allowed vlan add <VLAN-ID>` adds a VLAN without removing VLANs already permitted on the trunk.
- Static IP testing can help distinguish a DHCP problem from a VLAN, trunk, or gateway connectivity problem.
- Establishing a known-good baseline before introducing a network change makes troubleshooting significantly easier.

## Skills Demonstrated

This lab demonstrates practical experience with:

- Cisco IOS CLI
- VLAN configuration
- Access port configuration
- IEEE 802.1Q trunking
- Router-on-a-Stick (ROAS)
- Inter-VLAN routing
- VLSM and IPv4 subnetting
- Static routing
- DHCP configuration
- WAN connectivity
- Cisco IOS verification commands
- Layer 2 and Layer 3 troubleshooting
- Fault isolation
- End-to-end connectivity testing

## Useful Verification Commands

```cisco
show vlan brief
show interfaces trunk
show interfaces switchport
show ip interface brief
show ip route
show ip dhcp pool
show ip dhcp binding
show running-config
ping <destination-ip>
```

## Conclusion

This lab demonstrated that successfully creating a new VLAN involves more than creating the VLAN and assigning access ports.

When VLAN 50 was introduced, the existing network continued to operate while the new VLAN failed. By inspecting the trunk configuration, VLAN 50 was found to be missing from the allowed VLAN list.

After extending VLAN 50 across the complete Layer 2 path and verifying its Router-on-a-Stick and DHCP configuration, the client successfully obtained an IP address.

The key troubleshooting principle demonstrated by this lab is:

> **When an existing network works but a newly added VLAN does not, trace the new VLAN's complete path from the access port to its Layer 3 gateway and verify every trunk along that path.**




















