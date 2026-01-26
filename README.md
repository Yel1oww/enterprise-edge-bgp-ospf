# 🌐 Enterprise Edge Connectivity: BGP & OSPF Integration

## 📖 Project Overview

This repository contains a Cisco Packet Tracer simulation of a mid-sized enterprise network. The project demonstrates a production-standard "Single-Homed" edge design, focusing on how internal corporate traffic (OSPF) is handed off to an External Service Provider (BGP) to reach the internet.

## 🏗️ Key Features

Dynamic Routing Integration: Bridge between OSPF Area 0 (Internal) and eBGP AS 65001 (External).

Default Route Propagation: Automated internet exit discovery for the Core-Router via default-information originate.

Subnetting Strategy: Used /30 point-to-point links for router-to-router connections to conserve IP space.

Troubleshooting Log: Documented recovery from "Gateway of last resort not set" and BGP neighbor synchronization issues.

## 🗺️ Topology Diagram

![Network Topology](./topology/network_diagram.png)

## 🚀 Technical Configuration

The network is built using Cisco ISR 4331 routers. The routing logic follows this flow:

The Core-Router identifies the Office LAN (192.168.10.0/24) and sends traffic to the Edge via OSPF.

The Edge-Router acts as the Autonomous System Border Router (ASBR), translating internal OSPF routes into BGP prefixes.

The ISP-Router peers with the Edge via eBGP, providing a gateway to external networks.

## 🧪 Verification & Testing

To prove the network is "Production Ready," the following tests were performed:

---

### 1. Internal Routing (Core-Router)
**Command:** `show ip route`  
**Purpose:** Confirming the core has learned the default route via OSPF.

![Core Routing Table](./docs/Core_Routing_Table.png)

---

### 2. External Peering (Edge-Router)
**Command:** `show ip bgp summary`  
**Purpose:** Verifying the eBGP session with the ISP is active and "Established."

![BGP Status](./docs/BGP_Status.png)

---

### 3. End-to-End Connectivity (PC0)
**Command:** `ping 192.168.1.1` & `tracert 192.168.1.1`  
**Purpose:** Demonstrating full packet flow from the user PC, through the core and edge, to the ISP.

![PC0 Connectivity](./docs/PC0_Connectivity.png)

192.168.10.1 (Core-Router)

10.1.1.1 (Edge-Router)

192.168.1.1 (ISP-Router)

## 🛠️ How to Use This Repo

Download: Grab the .pkt file from the root directory.

Open: Launch the file in Cisco Packet Tracer (v8.0+).

Explore: Use the show run command on any router to inspect the logic, or refer to the configs folder for text-based configurations.

## 📂 Repository Structure

/topology: Visual network diagrams.

/configs: Raw Cisco IOS running-configs for ISP, Edge, and Core routers.

/docs: Verification screenshots and traceroute logs.

Enterprise_Edge_Lab.pkt: The source Packet Tracer file.
