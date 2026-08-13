# Cisco Networking Fundamentals

This section documents my understanding of the fundamental concepts behind Cisco routers and switches. It covers device memory, configuration storage, the Cisco IOS boot process, and basic device administration.

These notes are part of my hands-on networking journey and are supported by practical Cisco IOS and Packet Tracer exercises.

---

## Topics Covered

- RAM
- NVRAM
- Flash Memory
- Running Configuration
- Startup Configuration
- Cisco IOS
- Cisco Boot Process
- VLAN Database
- Basic IOS Verification Commands

- ---

## Cisco Device Memory

Cisco routers and switches use different types of memory for different purposes. Understanding where configurations and operating system files are stored is important when configuring, saving, rebooting, or troubleshooting Cisco devices.

### RAM

**RAM (Random Access Memory)** is volatile memory used while the device is operating.

RAM stores information such as:

- Running configuration (`running-config`)
- Routing tables
- ARP tables
- Packet buffers
- Other active processes

Because RAM is **volatile**, its contents are lost when the device is powered off or restarted.

The current running configuration can be viewed with:

```cisco
show running-config
```


### NVRAM

**NVRAM (Non-Volatile Random Access Memory)** retains its contents when the device loses power.

It is primarily used to store the
```text
startup-config
```

The startup configuration can be viewed with:

```cisco
show startup-config
```
### Flash Memory

**Flash memory** is non-volatile storage used primarily to store the **Cisco IOS image** and other system files.

Unlike RAM, the contents of Flash memory are retained when the router or switch is powered off or restarted.

The files stored in Flash can be viewed using:

```cisco
show flash:
```

On some Cisco devices, the following command can also be used:

```cisco
dir flash:
```
---

## Memory Comparison

| Memory Type | Volatile? | Primary Purpose | Example |
|---|---|---|---|
| **RAM** | Yes | Holds active information while the device is running | `running-config`, routing table, ARP table |
| **NVRAM** | No | Stores the saved device configuration | `startup-config` |
| **Flash** | No | Stores Cisco IOS and other system files | IOS image |

### Configuration Flow

When configuring a Cisco device, changes are made to the **running configuration in RAM**.

To preserve those changes after a reboot, the running configuration must be copied to **NVRAM**:

```cisco
copy running-config startup-config
```

---

## Cisco IOS Boot Process

When a Cisco router or switch is powered on, it follows a boot sequence to initialise the hardware, locate the Cisco IOS software, and load the saved configuration.

### Boot Sequence

1. **POST (Power-On Self-Test)**
   - The device checks its hardware components.
   - This includes CPU, memory, and interfaces.

2. **Bootstrap Program**
   - The bootstrap program begins the process of locating and loading the Cisco IOS.

3. **Load Cisco IOS**
   - The device locates the Cisco IOS image, commonly stored in **Flash memory**.
   - The IOS is loaded so the device can begin operating.

4. **Load Startup Configuration**
   - The device looks in **NVRAM** for the `startup-config`.
   - If a startup configuration exists, it is loaded into **RAM** as the `running-config`.

The overall process can be remembered as:

```text
Power On
   ↓
POST
   ↓
Bootstrap
   ↓
Locate IOS
   ↓
Flash → Cisco IOS
   ↓
NVRAM → startup-config
   ↓
RAM → running-config
   ↓
Device Operational
```

### What Happens If There Is No Startup Configuration?

If the device cannot find a valid `startup-config` in NVRAM, it may enter the **initial configuration dialog (setup mode)**.

This is commonly seen on a new or erased Cisco device.

### Useful Verification Commands

```cisco
show version
```

Displays information about the Cisco IOS version, device uptime, hardware, configuration register, and other system information.

```cisco
show running-config
```

Displays the configuration currently active in RAM.

```cisco
show startup-config
```

Displays the saved configuration stored in NVRAM.

```cisco
show flash:
```

Displays files stored in Flash memory, including the Cisco IOS image where applicable.

> **Key takeaway:** Flash commonly stores the IOS, NVRAM stores the saved `startup-config`, and RAM contains the active `running-config`.







---

## Basic Cisco IOS Administration

Cisco IOS provides different command modes for viewing information and configuring a device.

### IOS Command Modes

| Mode | Prompt Example | Purpose |
|---|---|---|
| User EXEC | `Router>` | Basic monitoring commands |
| Privileged EXEC | `Router#` | Advanced verification and management |
| Global Configuration | `Router(config)#` | Device-wide configuration |
| Interface Configuration | `Router(config-if)#` | Configure individual interfaces |
| Router Configuration | `Router(config-router)#` | Configure routing protocols |

### Moving Between IOS Modes

Enter privileged EXEC mode:

```cisco
enable
```

Enter global configuration mode:

```cisco
configure terminal
```

Enter an interface:

```cisco
interface GigabitEthernet0/0/0
```

Return one level:

```cisco
exit
```

Return directly to privileged EXEC mode:

```cisco
end
```

---

## Essential Verification Commands

These are some of the commands I frequently use when configuring and troubleshooting Cisco devices.

### Check Interface Status

```cisco
show ip interface brief
```

This provides a quick summary of interface IP addresses and their **Status/Protocol** state.

### View the Active Configuration

```cisco
show running-config
```

### View the Saved Configuration

```cisco
show startup-config
```

### View Device and IOS Information

```cisco
show version
```

### View Directly Connected Cisco Devices

```cisco
show cdp neighbors
```

For more detailed CDP information:

```cisco
show cdp neighbors detail
```

### Test IP Connectivity

```cisco
ping 192.168.1.1
```

### View the Routing Table

```cisco
show ip route
```

---

## Saving the Configuration

Configuration changes initially exist in the **running configuration in RAM**.

To make the configuration survive a reboot:

```cisco
copy running-config startup-config
```

A commonly used alternative is:

```cisco
write memory
```

> **Important:** Configuring a Cisco device and saving its configuration are two separate actions. If the running configuration is not saved, changes can be lost after a reboot.


