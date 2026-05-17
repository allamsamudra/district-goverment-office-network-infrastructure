# District Goverment Office Network Infrastructure

> A comprehensive local area network (LAN) implementation for a district government office (*Kantor Kecamatan*), designed and simulated using **Cisco Packet Tracer**.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Network Topology](#network-topology)
- [Hardware & Devices](#hardware--devices)
- [IP Address Scheme](#ip-address-scheme)
- [Wireless Configuration](#wireless-configuration)
- [Routing Configuration](#routing-configuration)
- [DHCP Configuration](#dhcp-configuration)
- [Network Zones](#network-zones)

---

##  Project Overview

This project documents the design and simulation of a structured network infrastructure for a district-level government office in Indonesia. The network supports wired workstations, wireless access points, and mobile devices distributed across multiple zones within the office premises.

The topology was designed with scalability, reliability, and ease of management in mind, utilizing a hierarchical three-layer approach: **core routing**, **distribution switching**, and **access-layer endpoints**.

---

##  Network Topology

The network consists of two primary routing domains interconnected via a **serial WAN link** (point-to-point), simulating an ISP or inter-department connection:

```
[ISP / Internet]
       |
  [Router Icon+]  ────── Se2/0 ──── Se2/0 ──── [Mikrotik RB951]
  192.168.100.0                                  192.168.20.0
  192.168.1.0                                    192.168.10.0
       |                                                |
[Switch 24-Port PoE]                          [Switch 8-Port PoE]
  (Ruijie Managed)                             (Ruijie Managed)
       |                                                |
[Access Points]                                  [Access Points]
       |                                                |
[Wireless Gadgets]                             [Wireless Gadgets]
```

---

##  Hardware & Devices

| Device | Model / Type | Quantity |
|---|---|---|
| Router (Main) | (Router Icon+) | 1 |
| Router (Branch) | (Mikrotik RB951 dlskominfo) | 1 |
| Modem | (Modem Icon+) | 1 | 
| Managed Switch | Ruijie 24-Port PoE Switch | 1 |
| Managed Switch | Ruijie 8-Port PoE Switch | 1 |
| Access Point | Ruijie RG 720-L | 7 |
| LAN Cable Cat 6 | BELDEN | 2 |

---

## IP Address Scheme

This IP address is not real and is provided for demonstration purposes only.

### Router Icon+

| Interface | IP Address | Function |
|---|---|---|
| Fa0/0 | 192.168.100.1 | Gateway — Network 192.168.100.0/24 (DHCP) |
| Fa1/0 | 192.168.1.1 | Gateway — Network 192.168.1.0/24 (DHCP) |
| Se2/0 | 10.10.0.1 | WAN serial link to Mikrotik |

**Networks served:** `10.10.0.0`, `192.168.100.0`, `192.168.1.0`

---

### Mikrotik RB951 (diskominfo)

| Interface | IP Address | Function |
|---|---|---|
| Fa0/0 | 192.168.20.1 | Gateway — Network 192.168.20.0/24 (DHCP) |
| Fa1/0 | 192.168.10.1 | Gateway — Network 192.168.10.0/24 (DHCP) |
| Se2/0 | 10.10.0.2 | WAN serial link to Main Router |

**Networks served:** `10.10.0.0`, `192.168.20.0`, `192.168.10.0`

---

## Wireless Configuration

All access points are configured under a unified wireless profile to ensure seamless connectivity throughout the office building.

| Parameter | Value |
|---|---|
| SSID | `WIFI KECAMATAN` |
| Security | WPA2-Personal |
| Password | `123123123` |
| Coverage | Office-wide (6 APs + 1 Modem) |
| IP Assignment | DHCP (via respective gateway) |


---

## Routing Configuration

Inter-router communication is established over a **serial point-to-point link** using the `10.10.0.0` network:

- **Main Router** → `Se2/0: 10.10.0.1`
- **Mikrotik RB951** → `Se2/0: 10.10.0.2`

Static or dynamic routing (e.g., OSPF/RIP) is configured to allow cross-domain communication between the `192.168.1.0/24`, `192.168.100.0/24`, `192.168.10.0/24`, and `192.168.20.0/24` subnets.

---

## DHCP Configuration

Both routers act as DHCP servers for their respective subnets, automatically assigning IP addresses to all connected endpoints including PCs, laptops, and smartphones.

| DHCP Server | Pool Network | Range |
|---|---|---|
| Router Icon+ Fa0/0 | 192.168.100.0/24 | Dynamic |
| Router Icon+ Fa1/0 | 192.168.1.0/24 | Dynamic |
| Mikrotik Fa0/0 | 192.168.20.0/24 | Dynamic |
| Mikrotik Fa1/0 | 192.168.10.0/24 | Dynamic |

---

##  Network Zones

The office network is divided into logical zones based on physical location and subnet:

| Zone | Subnet | Connected Devices |
|---|---|---|
| North Building | 192.168.20.0/24 | PC1, AP2, AP3, AP4, PC2 |
| West Center Building | 192.168.1.0/24 | AP1 |
| West Bottom Building | 192.168.20.0/24 | PC0, AP0 |
| Center Building | 192.168.20.0/24 | PC3, AP5 |
| Modem (Near Routers) | 192.168.100.0/24 | Modem Icon+ |

---


```
This project is created for educational and governmental infrastructure planning purposes.
```

*Designed and simulated as part of a network infrastructure project for a district government office (Kantor Kecamatan), Indonesia.*
