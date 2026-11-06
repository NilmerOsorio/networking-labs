# 🌐 My Static Routing Lab — Cisco Packet Tracer

Welcome! 👋 In this lab, I explored how **static routing** helps devices on different networks communicate. Using Cisco Packet Tracer, I learned how IP addresses, default gateways, and routing instructions work together to deliver a packet.

The lab network includes **3 routers, 3 switches, and 6 PCs**.

## 🎯 What Was the Goal?

The goal was to connect three local networks so their PCs could communicate through the routers. Each local network has one switch and two PCs, with the routers connected in a line:

```text
Router0 ───────── Router1 ───────── Router2
   │                │                │
Switch0          Switch1          Switch2
   │                │                │
PC0 + PC1        PC2 + PC3        PC4 + PC5
```

## 🧠 What I Learned

- **IP addresses identify devices.** The subnet mask tells a device which addresses belong to its local network.
- **A default gateway is the way out.** PCs send traffic for other networks to their local router.
- **Static routes are manual directions.** Each route tells a router which network to reach and which neighboring router to use next.
- **Replies need directions too.** Communication requires a working path to the destination and back.
- **Interfaces must be enabled.** I used `no shutdown` to enable router interfaces after assigning their IP addresses.
- **The CLI gives me direct control.** I practised entering configuration mode, adding routes, and checking the routing table with Cisco IOS commands.

## 📋 Addressing Plan

These are the IPv4 addresses used in the activity. **Every configured interface below uses subnet mask `255.0.0.0` (`/8`).** “—” means a PC-style default gateway does not apply; the routers use routing entries instead.

### Device Addresses

| Device | Interface / connection | IP address | Default gateway |
| --- | --- | --- | --- |
| PC0 | FastEthernet0 → Switch0 | `10.10.10.1` | `10.10.10.0` |
| PC1 | FastEthernet0 → Switch0 | `10.10.10.2` | `10.10.10.0` |
| PC2 | FastEthernet0 → Switch1 | `20.20.20.1` | `20.20.20.0` |
| PC3 | FastEthernet0 → Switch1 | `20.20.20.2` | `20.20.20.0` |
| PC4 | FastEthernet0 → Switch2 | `30.30.30.1` | `30.30.30.0` |
| PC5 | FastEthernet0 → Switch2 | `30.30.30.2` | `30.30.30.0` |
| Router0 | FastEthernet0/0 → Switch0 | `10.10.10.0` | — |
| Router0 | Serial2/0 → Router1 | `40.40.40.1` | — |
| Router1 | FastEthernet0/0 → Switch1 | `20.20.20.0` | — |
| Router1 | Serial2/0 → Router0 | `40.40.40.2` | — |
| Router1 | Serial3/0 → Router2 | `50.50.50.1` | — |
| Router2 | FastEthernet0/0 → Switch2 | `30.30.30.0` | — |
| Router2 | Serial2/0 → Router1 | `50.50.50.2` | — |

💡 An address ending in `.0` can be a valid host address! With the `/8` mask, `10.10.10.0` is a host in network `10.0.0.0`, so it can serve as the gateway here. No switch management IP addresses are configured in this activity.

### Network Overview

| Network | Purpose |
| --- | --- |
| `10.0.0.0/8` | PC0 and PC1 local network |
| `20.0.0.0/8` | PC2 and PC3 local network |
| `30.0.0.0/8` | PC4 and PC5 local network |
| `40.0.0.0/8` | Router0 ↔ Router1 link |
| `50.0.0.0/8` | Router1 ↔ Router2 link |

## 🛠️ Static Routing Setup with the CLI

I used the **Cisco IOS command-line interface (CLI)** to configure the routers. On each router, I entered `enable`, followed by `configure terminal`, then added the static routes with `ip route`. Each command specifies the destination network, subnet mask, and next hop.

**Router0**

```text
ip route 20.0.0.0 255.0.0.0 40.40.40.2
ip route 30.0.0.0 255.0.0.0 40.40.40.2
```

**Router1**

```text
ip route 10.0.0.0 255.0.0.0 40.40.40.1
ip route 30.0.0.0 255.0.0.0 50.50.50.2
```

**Router2**

```text
ip route 10.0.0.0 255.0.0.0 50.50.50.1
ip route 20.0.0.0 255.0.0.0 50.50.50.1
```

After adding the routes, I used `end` to leave configuration mode and `copy running-config startup-config` to save the configuration.

For example, Router0 sends traffic for the third LAN to Router1 at `40.40.40.2`, which forwards it toward Router2.

## ✅ Checking Connectivity

To check connectivity from the command line, I can use `ping <destination-IP>` within each LAN and between different LANs. A successful reply confirms that traffic can reach the destination and return.

When troubleshooting, I can check the PC’s address and gateway, use `show ip interface brief` to inspect router interfaces, and run `show ip route` to review installed routes. Static routes appear with the code `S`.

## 🚀 My Takeaway

This lab helped me understand how a packet finds its way across multiple networks and become more comfortable configuring routers through the CLI. My next step is to explore default routes and compare static routing with dynamic routing.

Feel free to explore the addressing tables and try the lab yourself! 🌱
