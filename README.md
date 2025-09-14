# Networking VLAN & Inter-VLAN Routing Lab

## Week 1 – VLAN & Inter-VLAN Routing

<img src ="screenshots/topology.png" alt="INTER VLAN TOPOLOGY" width="600" />


## Table of Contents

1. [Lab Objective](#lab-objective)
2. [Lab Topology](#lab-topology)
3. [IP Addressing Table](#ip-addressing-table)
4. [Device Configuraion Overview](#device-configuration-overview)
5. [Verification Steps](#verification-steps)
6. [Folder Structure](#folder-structure)
7. [Notes](#notes)
8. [License](#license)

---


### 1. Lab Objective

---

- Configure **VLANs** on multiple switches.
- Set up **trunk links** between switches and router.
- Configure **Router-on-a-Stick** for inter-VLAN routing.
- Verify connectivity between devices in different VLANs.
- Document all configurations and verification outputs.

---

### 2. Lab Topology

---

PC1-PC3 --- SW1 ---+--- R1 (G0/0)
|
PC4-PC6 --- SW2 ---+


- **VLAN 10** → PC1, PC2, PC3  
- **VLAN 20** → PC4, PC5, PC6  
- **SW1 ↔ SW2 trunk** → allows VLANs 10 & 20  
- **Router-on-a-stick** → R1 subinterfaces for VLAN 10 & VLAN 20  

---

### 3. IP Addressing Table

---


| Device | Interface | IP Address     | Subnet Mask    | Default Gateway|
|--------|-----------|----------------|----------------|----------------|
| PC1    | Fa0       | 192.168.10.10  | 255.255.255.0  | 192.168.10.1   |
| PC2    | Fa0       | 192.168.10.11  | 255.255.255.0  | 192.168.10.1   |
| PC3    | Fa0       | 192.168.10.12  | 255.255.255.0  | 192.168.10.1   |
| PC4    | Fa0       | 192.168.20.10  | 255.255.255.0  | 192.168.20.1   |
| PC5    | Fa0       | 192.168.20.11  | 255.255.255.0  | 192.168.20.1   |
| PC6    | Fa0       | 192.168.20.12  | 255.255.255.0  | 192.168.20.1   |
| R1     | G0/0.10   | 192.168.10.1   | 255.255.255.0  | N/A            |
| R1     | G0/0.20   | 192.168.20.1   | 255.255.255.0  | N/A            |

---

### 4. Device Configuration Overview

---

**SW1 – Distribution Switch**
- VLANs 10 & 20 created.
- Access ports: PC1–PC3 in VLAN 10.
- Trunk ports: Fa0/23 to router, Fa0/24 to SW2.

**SW2 – Access Switch**
- VLANs 10 & 20 created.
- Access ports: PC4–PC6 in VLAN 20.
- Trunk port: Fa0/24 to SW1.

**R1 – Router-on-a-Stick**
- G0/0 physical interface connected to SW1 trunk.
- Subinterfaces: G0/0.10 for VLAN 10, G0/0.20 for VLAN 20.

---

### 5. Verification Steps

---

On Switches

show vlan brief

show interfaces trunk
show mac address-table

On Router

show ip interface brief
show ip route
show ip arp

On PCs

Ping From PC1 to PC5

<img src ="screenshots/ping pc1 to pc5.png" alt="Ping From PC1 to PC5" width="600" />

Ping From PC6 to PC3

<img src ="screenshots/ping pc6 to pc3.png" alt="Ping From PC6 to PC3" width="600" />



ping Both Gateway

<img src ="screenshots/gateway ping.png" alt="Ping Both Gateways" width="600" />


---

### 6. Folder Structure

---

networking-vlan-intervlan/
├─ README.md
├─ verification.md
├─ labs/
│  └─ week1-vlan/
│      └─ topology.pkt
├─ configs/
│  ├─ sw1.cfg
│  ├─ sw2.cfg
│  └─ r1.cfg
└─ screenshots/
   ├─ ping pc1 to pc5.png
   ├─ ping pc6 to pc3.png
   ├─ show-vlan-brief SW1.png
   ├─ show-vlan-brief SW2.png
   ├─ show-interfaces-trunk SW1.png
   ├─ show-interfaces-trunk SW2.png
   └─ topology.png
   └─ gateway ping.png


configs/ → Configuration files for SW1, SW2, R1.

screenshots/ → Captured outputs from Packet Tracer verification commands.

verification.md → Text outputs of all show commands and ping tests.

---

### 7. Notes

---


This lab demonstrates VLAN creation, trunking, and inter-VLAN routing.

All devices are configured to avoid native VLAN mismatch, unused VLANs, or trunk negotiation issues.

Inter-VLAN connectivity verified; all ping tests successful.

---

### 8. License

---
<a href="LICENSE">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License" />
</a>

This project is licensed under the [MIT License](LICENSE).

---