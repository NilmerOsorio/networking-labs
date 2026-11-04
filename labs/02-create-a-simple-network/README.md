# 🌐 Cisco Packet Tracer – Create a Simple Network

## 📌 About This Activity

In this activity from the **Cisco Networking Academy** course, I built a simple network using Cisco Packet Tracer.

The goal was to understand how different network devices connect, how end devices obtain IP addresses, and how to verify that everything is working correctly.

I worked with both wired and wireless connections, configured network interfaces, and tested connectivity to a remote server.

## 🖥️ Network Topology

The network included the following devices:

| Device | Purpose |
|---|---|
| 💻 PC | Connects to the network using an Ethernet cable. |
| 💻 Laptop | Connects to the network wirelessly. |
| 📡 Wireless Router | Connects devices and assigns IP addresses using DHCP. |
| 📦 Cable Modem | Converts the ISP's coaxial connection into Ethernet. |
| ☁️ Internet Cloud | Represents the Internet Service Provider (ISP). |

### 🔌 Physical Connections

I connected the devices using the following cables:

| Connection | Cable Type |
|---|---|
| PC → Wireless Router | Copper Straight-Through |
| Wireless Router → Cable Modem | Copper Straight-Through |
| Cable Modem → Internet Cloud | Coaxial Cable |

## 🧠 What I Learned

Here are the main concepts I explored and practised during this activity.

### 1. 🏗️ Building a Network Topology

I learnt how to use the **Logical Workspace** in Cisco Packet Tracer to build a basic network.

I added different network devices, changed their display names, and connected them through their corresponding interfaces.

I also became familiar with the different device categories available in Packet Tracer.

### 2. 🔌 Ethernet Connections and Network Interfaces

I learnt how wired connections work and how to use a **Copper Straight-Through cable** to connect devices such as a PC and a wireless router.

I also explored Network Interface Cards (NICs), which allow devices to communicate with a network through wired or wireless connections.

### 3. 📦 Understanding Cable Modems

I learnt what a cable modem does and why it is important when connecting a local network to an Internet Service Provider (ISP).

A cable modem receives a coaxial connection from the ISP and converts it into an Ethernet connection that can be used by the local network.

### 4. 🔄 DHCP – Automatic IP Address Assignment

One of the key concepts I practised was **DHCP (Dynamic Host Configuration Protocol)**.

DHCP automatically assigns IP configuration details to devices when they connect to a network.

In this activity, the wireless router acted as the DHCP server, providing IP addresses to both the PC and the laptop.

To check the assigned configuration, I used:

```bash
ipconfig
```

I also explored:

```bash
ipconfig /all
```

This command displays more detailed information about the network adapter, including its IPv4 address, subnet mask, default gateway and other configuration details.

### 5. 🌍 Understanding IPv4 Addressing

I learnt how IPv4 addresses identify devices within a network.

Both end devices received unique addresses from the following private IP range:

```text
192.168.0.x
```

I also explored three important networking components:

- **IPv4 Address:** Identifies a device within a network.
- **Subnet Mask:** Determines which part of an IP address represents the network and which part identifies the host.
- **Default Gateway:** Allows devices to communicate with networks outside their local network.

An interesting analogy from this activity is to think of an IP address as a house address:

- The network ID represents the street.
- The host ID represents the house number.
- The default gateway represents the intersection that connects the street to other streets.

### 6. 📶 Configuring a Wireless Connection

I learnt how to configure a laptop to connect to a wireless network by replacing its existing Ethernet module with a wireless NIC.

The process involved:

1. Turning off the laptop.
2. Removing the Ethernet module.
3. Installing the wireless **WPC300N** module.
4. Turning the laptop back on.
5. Opening the PC Wireless utility.
6. Finding and connecting to the `HomeNetwork` wireless network.

This helped me understand how different devices can access the same local network using either wired or wireless connections.

### 7. 🧪 Testing Network Connectivity

After configuring both devices, I learnt how to test network connectivity using the `ping` command.

From the PC's Command Prompt, I executed:

```bash
ping cisco.srv
```

The PC successfully received four replies from the destination server.

I also opened the laptop's web browser and accessed `cisco.srv` to verify that the wireless connection was working correctly.

This was a practical introduction to connectivity testing and basic network verification.

## ⌨️ Commands Practised

| Command | What it does |
|---|---|
| `ipconfig` | Displays the basic IP configuration. |
| `ipconfig /all` | Displays detailed network adapter information. |
| `ping cisco.srv` | Tests connectivity to the destination server. |

## 📚 Key Concepts

A quick summary of the main topics covered:

- 🏗️ Network topology and device configuration.
- 🔌 Ethernet and coaxial cabling.
- 🔗 Copper Straight-Through connections.
- 💻 Network Interface Cards (NICs).
- 📶 Wired and wireless communication.
- 📦 Cable modems and ISP connectivity.
- 🔄 DHCP and automatic IP assignment.
- 🌍 IPv4 addressing and private IP ranges.
- 🧩 Subnet masks and network identification.
- 🚪 Default gateways.
- 🧪 Connectivity testing using ICMP (ping).

## 💭 Final Thoughts

This was a great introduction to building and understanding a basic computer network.

One of the most interesting things I learnt was how DHCP makes network configuration much easier by automatically assigning IP addresses and other essential network information.

I also gained practical experience connecting devices, configuring wireless interfaces, inspecting IP configurations and testing connectivity.

**My biggest takeaway:** A network is more than just connecting devices with cables. Understanding how devices obtain IP addresses and communicate with each other is essential to learning how computer networks actually work.

---

### 🏷️ Activity Information

- **Course:** Cisco Networking Academy
- **Tool:** Cisco Packet Tracer
- **Activity:** Create a Simple Network
- **Topics:** Networking Fundamentals, DHCP, IPv4, Ethernet and Wireless Connectivity
