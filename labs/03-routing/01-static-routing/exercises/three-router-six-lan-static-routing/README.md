# 🌐 My Static Routing Lab — Cisco Packet Tracer

Welcome! 👋 In this lab, I explored how **static routing** allows devices on different networks to communicate through interconnected routers. Using Cisco Packet Tracer, I practised configuring router interfaces, assigning IPv4 addresses, establishing next-hop relationships, and managing routing tables through the Cisco IOS CLI.

The topology consists of **3 routers, 6 switches, 6 PCs, and 6 laptops**, distributed across six LAN networks and two WAN connections.

## 🎯 What Was the Goal?

The goal was to connect six local networks through three interconnected routers, allowing devices from different LANs to communicate using static routing.

Each router manages two local networks, while the routers are connected in a linear topology:

```text
                    WAN 10.0.10.0/30       WAN 20.0.20.0/30

      ┌────────────────────────┐  ┌────────────────────────┐
      │                        │  │                        │
     R01 ──────────────────── R02 ────────────────────── R03
      │                        │                          │
      ├── SW01-1               ├── SW01-2                 ├── SW01-3
      │   ├── PC01             │   ├── PC03                │   ├── PC05
      │   └── LAP01            │   └── LAP03               │   └── LAP05
      │                        │                          │
      └── SW02-1               └── SW02-2                 └── SW02-3
          ├── PC01                 ├── PC04                    ├── PC06
          └── LAP01                └── LAP04                   └── LAP06
```

## 🧠 What I Learned

- **IP addresses identify devices.** Every router interface and end device needs an IPv4 address belonging to its respective network.
- **Subnet masks define network boundaries.** They determine which addresses belong to the same local network.
- **Default gateways provide access to remote networks.** PCs and laptops use their local router interface to communicate outside their LAN.
- **Static routes provide directions to remote networks.** Each route specifies a destination network, its subnet mask, and a next-hop address.
- **Next-hop addresses are essential.** Routers forward traffic toward neighboring routers that can reach the destination network.
- **Routing tables show how networks are reached.** Directly connected networks appear with the code `C`, while static routes appear with `S`.
- **The CLI provides control over the network.** I practised configuring interfaces, assigning addresses, adding static routes, and inspecting router configurations.

## 📋 Addressing Plan

The following tables document the IPv4 addressing used in my implementation.

### Network Overview

| Network | Type | Connected Switch / Routers | Associated Router |
| --- | --- | --- | --- |
| `192.168.11.0/25` | LAN | SW01-1 | R01 |
| `172.16.12.128/25` | LAN | SW02-1 | R01 |
| `193.169.13.0/26` | LAN | SW01-2 | R02 |
| `173.17.14.192/26` | LAN | SW02-2 | R02 |
| `194.170.15.0/28` | LAN | SW01-3 | R03 |
| `174.18.16.0/25` | LAN | SW02-3 | R03 |
| `10.0.10.0/30` | WAN | R01 ↔ R02 | — |
| `20.0.20.0/30` | WAN | R02 ↔ R03 | — |

### Router Interface Addresses

| Router | Interface | Connection | IP Address | Subnet Mask |
| --- | --- | --- | --- | --- |
| R01 | GigabitEthernet0/0/0 | SW02-1 | `172.16.12.129` | `255.255.255.128` |
| R01 | GigabitEthernet0/0/1 | SW01-1 | `192.168.11.1` | `255.255.255.128` |
| R01 | Serial0/2/0 | R02 | `10.0.10.1` | `255.255.255.252` |
| R02 | GigabitEthernet0/0/0 | SW02-2 | `173.17.14.193` | `255.255.255.192` |
| R02 | GigabitEthernet0/0/1 | SW01-2 | `193.169.13.1` | `255.255.255.192` |
| R02 | Serial0/2/0 | R01 | `10.0.10.2` | `255.255.255.252` |
| R02 | Serial0/2/1 | R03 | `20.0.20.1` | `255.255.255.252` |
| R03 | GigabitEthernet0/0/0 | SW02-3 | `174.18.16.1` | `255.255.255.128` |
| R03 | GigabitEthernet0/0/1 | SW01-3 | `194.170.15.1` | `255.255.255.240` |
| R03 | Serial0/2/1 | R02 | `20.0.20.2` | `255.255.255.252` |

### End-Device Addresses

All PCs and laptops use their `FastEthernet0` interface.

| Device | Connected Switch | IP Address | Subnet Mask | Default Gateway |
| --- | --- | --- | --- | --- |
| PC01-SW01-R01 | SW01-1 | `192.168.11.11` | `255.255.255.128` | `192.168.11.1` |
| LAP01-SW01-R01 | SW01-1 | `192.168.11.22` | `255.255.255.128` | `192.168.11.1` |
| PC01-SW02-R01 | SW02-1 | `172.16.12.131` | `255.255.255.128` | `172.16.12.129` |
| LAP01-SW02-R01 | SW02-1 | `172.16.12.132` | `255.255.255.128` | `172.16.12.129` |
| PC03-SW01-R02 | SW01-2 | `193.169.13.11` | `255.255.255.192` | `193.169.13.1` |
| LAP03-SW01-R02 | SW01-2 | `193.169.13.12` | `255.255.255.192` | `193.169.13.1` |
| PC04-SW02-R02 | SW02-2 | `173.17.14.201` | `255.255.255.192` | `173.17.14.193` |
| LAP04-SW02-R02 | SW02-2 | `173.17.14.202` | `255.255.255.192` | `173.17.14.193` |
| PC05-SW01-R03 | SW01-3 | `194.170.15.11` | `255.255.255.240` | `194.170.15.1` |
| LAP05-SW01-R03 | SW01-3 | `194.170.15.12` | `255.255.255.240` | `194.170.15.1` |
| PC06-SW02-R03 | SW02-3 | `174.18.16.11` | `255.255.255.128` | `174.18.16.1` |
| LAP06-SW02-R03 | SW02-3 | `174.18.16.22` | `255.255.255.128` | `174.18.16.1` |

## 🔌 Physical Connections

### Router-to-Router Connections

| Connected Routers | First Interface | Second Interface | Connection Type |
| --- | --- | --- | --- |
| R01 ↔ R02 | Serial0/2/0 | Serial0/2/0 | Serial |
| R02 ↔ R03 | Serial0/2/1 | Serial0/2/1 | Serial |

### Router-to-Switch Connections

| Router | Router Interface | Switch | Switch Interface |
| --- | --- | --- | --- |
| R01 | GigabitEthernet0/0/1 | SW01-1 | GigabitEthernet0/1 |
| R01 | GigabitEthernet0/0/0 | SW02-1 | GigabitEthernet0/2 |
| R02 | GigabitEthernet0/0/1 | SW01-2 | GigabitEthernet0/1 |
| R02 | GigabitEthernet0/0/0 | SW02-2 | GigabitEthernet0/2 |
| R03 | GigabitEthernet0/0/1 | SW01-3 | GigabitEthernet0/1 |
| R03 | GigabitEthernet0/0/0 | SW02-3 | GigabitEthernet0/2 |

### End-Device Connections

| End-Device Type | End-Device Interface | Switch Interface |
| --- | --- | --- |
| PC | FastEthernet0 | FastEthernet0/11 |
| Laptop | FastEthernet0 | FastEthernet0/22 |

## 🛠️ Static Routing Configuration

I used the **Cisco IOS Command-Line Interface (CLI)** to configure static routes on all three routers.

The `ip route` command uses three main parameters:

1. Destination network.
2. Destination subnet mask.
3. Next-hop IP address.

### R01 — Routes Toward Remote Networks

R01 uses R02 (`10.0.10.2`) as its next hop to reach the LAN networks located behind R02 and R03.

```text
ip route 193.169.13.0 255.255.255.192 10.0.10.2
ip route 173.17.14.192 255.255.255.192 10.0.10.2
ip route 194.170.15.0 255.255.255.240 10.0.10.2
ip route 174.18.16.0 255.255.255.128 10.0.10.2
```

### R02 — Routes Toward R01 and R03 Networks

R02 uses R01 (`10.0.10.1`) to reach the LAN networks on the left and R03 (`20.0.20.2`) to reach the LAN networks on the right.

```text
ip route 192.168.11.0 255.255.255.128 10.0.10.1
ip route 172.16.12.128 255.255.255.128 10.0.10.1
ip route 194.170.15.0 255.255.255.240 20.0.20.2
ip route 174.18.16.0 255.255.255.128 20.0.20.2
```

### R03 — Routes Toward Remote Networks

R03 uses R02 (`20.0.20.1`) as its next hop to reach the LAN networks located behind R01 and R02.

```text
ip route 193.169.13.0 255.255.255.192 20.0.20.1
ip route 173.17.14.192 255.255.255.192 20.0.20.1
ip route 192.168.11.0 255.255.255.128 20.0.20.1
ip route 172.16.12.128 255.255.255.128 20.0.20.1
```

For example, when R01 needs to reach `174.18.16.0/25`, it forwards the traffic to R02 using the next-hop address `10.0.10.2`. R02 then forwards the traffic toward R03 through `20.0.20.2`.

**Note:** The R01 route to `174.18.16.0/25` is documented with the `/25` subnet mask (`255.255.255.128`), matching the LAN network allocation.

After configuring the routes, I saved the router configurations using:

```text
copy running-config startup-config
```

## ✅ Checking Connectivity and Routing Tables

I used Cisco IOS verification commands to inspect the router interfaces and routing information.

| Command | Purpose |
| --- | --- |
| `show ip interface brief` | Displays interface IP addresses and operational status. |
| `show running-config` | Displays the current router configuration. |
| `show ip route` | Displays directly connected networks and static routes. |
| `show interfaces` | Displays detailed interface information. |
| `ping <destination-IP>` | Tests connectivity between devices. |

On PCs and laptops, I used:

```text
ipconfig
```

This allowed me to inspect the IPv4 address, subnet mask, and default gateway assigned to each end device.

A successful ping between devices on different LANs confirms that traffic can reach its destination and that a return path is available.

## 🚀 My Takeaway

This lab helped me understand how multiple networks communicate through interconnected routers and how static routing controls the path packets follow.

I also gained practical experience with IPv4 addressing, subnet masks, default gateways, router interfaces, and Cisco IOS commands. More importantly, I learned how to examine routing tables and understand the relationship between directly connected networks and manually configured routes.

Thanks for checking out my networking lab! 🌱
