# 🔀 My Dynamic Routing Lab — RIP in Cisco Packet Tracer

Welcome! 👋 In this lab, I built on my static-routing practice and explored **dynamic routing** with the Routing Information Protocol (RIP). The Packet Tracer project connects three local networks through three routers, allowing the routers to learn routes from one another instead of requiring every remote route to be entered manually.

## 🎯 Lab Goal

The goal was to configure RIP so hosts in each LAN could communicate across the router chain. The topology uses **3 routers, 3 switches, and 6 PCs**—two PCs on each switch:

```text
Router0 ───────── Router1 ───────── Router2
   │                │                │
Switch0          Switch1          Switch2
   │                │                │
PC0 + PC1        PC2 + PC3        PC4 + PC5
```

## 🧠 What I Learned

- **Dynamic routing shares network information.** Routers running RIP advertise reachable networks to their neighbors and add learned routes to their routing tables.
- **RIP uses hop count.** It selects a route based on the number of routers a packet must cross. This simple metric is useful for a small lab, though it doesn't compare link speed or congestion.
- **Routers need to advertise their directly connected networks.** Enabling RIP alone is not enough; the correct network statements must be configured on each router.
- **PC addressing still matters.** Each PC needs an address, subnet mask, and the local router interface as its default gateway.
- **Routing must work in both directions.** A ping reply needs a return path, so route learning on every router matters.
- **Verification is part of configuration.** `show ip route` lets me confirm learned routes (shown with `R`), while `show ip interface brief` and `ping` help check interfaces and end-to-end reachability.

## 🗺️ Network Layout and Addressing

The lab uses three LANs and two router-to-router links. The project follows the same address plan as the static-routing exercise in this repository; the purpose here is to let RIP exchange those routes automatically.

| Network | Purpose |
| --- | --- |
| `10.0.0.0/8` | Router0 LAN, Switch0, PC0 and PC1 |
| `20.0.0.0/8` | Router1 LAN, Switch1, PC2 and PC3 |
| `30.0.0.0/8` | Router2 LAN, Switch2, PC4 and PC5 |
| `40.0.0.0/8` | Router0 ↔ Router1 serial link |
| `50.0.0.0/8` | Router1 ↔ Router2 serial link |

Each PC uses the router's LAN interface as its default gateway. The detailed interface and host addresses are documented in the [static-routing lab](../01-static-routing/README.md).

## ⚙️ RIP Configuration

On each router, I entered privileged and global configuration modes, then enabled RIP and advertised the networks directly connected to that router. The network statements below reflect the lab's addressing plan:

**Router0**

```text
router rip
network 10.0.0.0
network 40.0.0.0
```

**Router1**

```text
router rip
network 20.0.0.0
network 40.0.0.0
network 50.0.0.0
```

**Router2**

```text
router rip
network 30.0.0.0
network 50.0.0.0
```

The `network` commands enable RIP on matching interfaces and let the routers advertise those connected networks. After the routers exchange updates, each should learn routes to the remote LANs. I can use `show ip route` to inspect the routing table and look for routes marked `R`.

## ✅ Checking the Lab

I can test connectivity by pinging PCs on other LANs. If a ping fails, I can check:

1. The PC's IP address, mask, and default gateway.
2. Router interface addresses and whether interfaces are up (`show ip interface brief`).
3. The RIP-learned routes (`show ip route`).
4. The return route from the destination network.

## 🚀 My Takeaway

This lab showed me how routers can learn routes dynamically and keep routing tables up to date through a routing protocol. Compared with static routing, RIP reduces the need to enter each remote destination by hand. It also helped me connect the routing table to the actual path a packet takes through multiple routers.

Open [`dynamic_routing.pkt`](dynamic_routing.pkt) in Cisco Packet Tracer to explore the topology. 🌱
