# 🔀 Lab 01: VLAN Configuration

## 🎯 Objective

Practice network segmentation with VLANs in Cisco Packet Tracer. Refer to the original requirements for the exact tasks and expected behavior.

## 📁 Lab files

- [Packet Tracer project](packet-tracer/vlan_activity.pkt)
- [Original activity requirements](requirements/requirements.png)
- `configurations/` — device command exports to add after verification.
- `diagrams/` — topology images to add.
- `evidence/` — screenshots and connectivity results to add.

## 🚀 Open the activity

1. Review the requirements image.
2. Open `packet-tracer/vlan_activity.pkt` in Cisco Packet Tracer.
3. Inspect the devices, addressing, VLAN assignments, and links before making changes.

## 📝 Configuration notes

I organized the network into three department VLANs, each with its own subnet and default gateway. The router subinterfaces provide the gateways for the corresponding VLANs.

### VLAN 10 — Human Talent

| Subnet detail | Value |
|---|---|
| Network | `192.169.10.0/25` |
| Subnet mask | `255.255.255.128` |
| Usable address range | `192.169.10.1–192.169.10.126` |
| Broadcast | `192.169.10.127` |
| Default gateway | `192.169.10.1` |
| Router subinterface | `GigabitEthernet0/0/1.10` |

| PC | Switch | Access port | IP address | Subnet mask | Default gateway |
|---|---|---|---|---|---|
| PC01-10 | sw01 | Fa0/11 | `192.169.10.2` | `255.255.255.128` | `192.169.10.1` |
| PC02-10 | sw02 | Fa0/11 | `192.169.10.3` | `255.255.255.128` | `192.169.10.1` |

### VLAN 20 — Contability

| Subnet detail | Value |
|---|---|
| Network | `174.18.20.0/26` |
| Subnet mask | `255.255.255.192` |
| Usable address range | `174.18.20.1–174.18.20.62` |
| Broadcast | `174.18.20.63` |
| Default gateway | `174.18.20.1` |
| Router subinterface | `GigabitEthernet0/0/1.20` |

| PC | Switch | Access port | IP address | Subnet mask | Default gateway |
|---|---|---|---|---|---|
| PC01-20 | sw01 | Fa0/12 | `174.18.20.2` | `255.255.255.192` | `174.18.20.1` |
| PC02-20 | sw03 | Fa0/12 | `174.18.20.3` | `255.255.255.192` | `174.18.20.1` |

### VLAN 30 — Transport

| Subnet detail | Value |
|---|---|
| Network | `11.22.30.32/27` |
| Subnet mask | `255.255.255.224` |
| Usable address range | `11.22.30.33–11.22.30.62` |
| Broadcast | `11.22.30.63` |
| Default gateway | `11.22.30.33` |
| Router subinterface | `GigabitEthernet0/0/1.30` |

| PC | Switch | Access port | IP address | Subnet mask | Default gateway |
|---|---|---|---|---|---|
| PC01-30 | sw02 | Fa0/13 | `11.22.30.34` | `255.255.255.224` | `11.22.30.33` |
| PC02-30 | sw03 | Fa0/13 | `11.22.30.35` | `255.255.255.224` | `11.22.30.33` |

All six PCs use **static IPv4 addresses**. DNS is not required for this activity.

## ✅ Verification checklist

- [ ] Compare the topology and settings with the activity requirements.
- [ ] Review VLAN membership with `show vlan brief`.
- [ ] Check applicable trunk links with `show interfaces trunk`.
- [ ] Test the expected connectivity and isolation between hosts.
- [ ] Record actual results and add supporting evidence.

## 💡 Conclusions

After verification, summarize what you learned and any configuration issues you resolved.
