# 🌐 Dynamic Routing with RIPv2 — Cisco Packet Tracer

In this lab, I practised **dynamic routing using RIP Version 2 (RIPv2)** in Cisco Packet Tracer. I learned how routers exchange routing information automatically to enable communication between different networks.

The topology includes **3 routers, 6 switches, 6 PCs, and 6 laptops**, connected through six LANs and two WAN links.

## 🎯 What Was the Goal?

Connect all six LAN networks using RIPv2, replacing manually configured static routes with dynamic route discovery.

```text
       R01 ───────── R02 ───────── R03
        │             │             │
      SW01-1        SW01-2        SW01-3
      SW02-1        SW02-2        SW02-3
        │             │             │
      2 devices     2 devices     2 devices
      per switch    per switch    per switch
```

## 🧠 What I Learned

- **Dynamic routing:** Routers exchange routing information automatically.
- **RIPv2:** Supports classless routing and carries subnet mask information.
- **Hop count:** RIP uses the number of routers crossed as its routing metric.
- **Routing updates:** Routers learn remote networks from their neighbors.
- **Routing tables:** Routes learned through RIP appear with the `R` code.
- **Verification:** I practised inspecting routing tables and testing connectivity.

## 📋 Addressing Plan

The addressing scheme remains the same as in my static routing exercise.

### Network Overview

| Network | Type | Switch / Connection | Router |
|---|---|---|---|
| `192.168.11.0/25` | LAN | SW01-1 | R01 |
| `172.16.12.128/25` | LAN | SW02-1 | R01 |
| `193.169.13.0/26` | LAN | SW01-2 | R02 |
| `173.17.14.192/26` | LAN | SW02-2 | R02 |
| `194.170.15.0/28` | LAN | SW01-3 | R03 |
| `174.18.16.0/25` | LAN | SW02-3 | R03 |
| `10.0.10.0/30` | WAN | R01 ↔ R02 | — |
| `20.0.20.0/30` | WAN | R02 ↔ R03 | — |

### Router Interface Addresses

| Router | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R01 | GigabitEthernet0/0/0 | `172.16.12.129` | `255.255.255.128` |
| R01 | GigabitEthernet0/0/1 | `192.168.11.1` | `255.255.255.128` |
| R01 | Serial0/2/0 | `10.0.10.1` | `255.255.255.252` |
| R02 | GigabitEthernet0/0/0 | `173.17.14.193` | `255.255.255.192` |
| R02 | GigabitEthernet0/0/1 | `193.169.13.1` | `255.255.255.192` |
| R02 | Serial0/2/0 | `10.0.10.2` | `255.255.255.252` |
| R02 | Serial0/2/1 | `20.0.20.1` | `255.255.255.252` |
| R03 | GigabitEthernet0/0/0 | `174.18.16.1` | `255.255.255.128` |
| R03 | GigabitEthernet0/0/1 | `194.170.15.1` | `255.255.255.240` |
| R03 | Serial0/2/1 | `20.0.20.2` | `255.255.255.252` |

### End-Device Addresses

All end devices use the `FastEthernet0` interface.

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC01-SW01-R01 | `192.168.11.11` | `255.255.255.128` | `192.168.11.1` |
| LAP01-SW01-R01 | `192.168.11.22` | `255.255.255.128` | `192.168.11.1` |
| PC01-SW02-R01 | `172.16.12.131` | `255.255.255.128` | `172.16.12.129` |
| LAP01-SW02-R01 | `172.16.12.132` | `255.255.255.128` | `172.16.12.129` |
| PC03-SW01-R02 | `193.169.13.11` | `255.255.255.192` | `193.169.13.1` |
| LAP03-SW01-R02 | `193.169.13.12` | `255.255.255.192` | `193.169.13.1` |
| PC04-SW02-R02 | `173.17.14.201` | `255.255.255.192` | `173.17.14.193` |
| LAP04-SW02-R02 | `173.17.14.202` | `255.255.255.192` | `173.17.14.193` |
| PC05-SW01-R03 | `194.170.15.11` | `255.255.255.240` | `194.170.15.1` |
| LAP05-SW01-R03 | `194.170.15.12` | `255.255.255.240` | `194.170.15.1` |
| PC06-SW02-R03 | `174.18.16.11` | `255.255.255.128` | `174.18.16.1` |
| LAP06-SW02-R03 | `174.18.16.22` | `255.255.255.128` | `174.18.16.1` |

## 🛠️ RIPv2 Configuration

I configured RIP Version 2 on each router through the Cisco IOS CLI.

### R01

```text
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 172.16.0.0
 network 192.168.11.0
```

### R02

```text
router rip
 version 2
 no auto-summary
 network 10.0.0.0
 network 20.0.0.0
 network 173.17.0.0
 network 193.169.13.0
```

### R03

```text
router rip
 version 2
 no auto-summary
 network 20.0.0.0
 network 174.18.0.0
 network 194.170.15.0
```

With RIPv2 enabled, routers exchange routing updates and dynamically learn remote networks through their neighboring routers.

## ✅ Verification and Connectivity

I used the following commands to inspect the network:

| Command | Purpose |
|---|---|
| `show ip interface brief` | Check interface addresses and status. |
| `show ip route` | Inspect learned and connected routes. |
| `show ip protocols` | Verify RIP configuration. |
| `show ip rip database` | Inspect RIP routing information. |
| `ping <destination-IP>` | Test connectivity between devices. |

In the routing table, routes marked with **`R`** indicate networks learned through RIP.

## 🚀 My Takeaway

This exercise helped me understand how dynamic routing simplifies communication between multiple networks. Compared with static routing, RIPv2 allows routers to exchange network information automatically instead of requiring individual routes to be configured manually.
