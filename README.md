# Spanning Tree Protocol (STP) Lab – Cisco Packet Tracer

This lab demonstrates how **Spanning Tree Protocol (STP)** prevents Layer 2 loops by electing a root bridge and blocking redundant paths in a switched network. The topology is designed and tested using **Cisco Packet Tracer**.

##  Lab Topology
![Lab Screenshot](./stp_lab_topology.png) <!-- Add your image here with same name -->

---

### Devices in the Topology

| Device | Role       | Connected Ports     | Notes                |
|--------|------------|---------------------|----------------------|
| MLS0   | Core Switch (Root Bridge) | Fa0/1, Fa0/2 (PCs), Fa0/3, Fa0/4 (to MLS1 & MLS2) | Set as STP Root |
| MLS1   | Access Switch | Fa0/1, Fa0/2 (PCs), Fa0/3, Fa0/4 (to MLS0 & MLS2) |                  |
| MLS2   | Access Switch | Fa0/1, Fa0/2 (PCs), Fa0/3, Fa0/4 (to MLS0 & MLS1) |                  |
| PCs    | End Devices   | Each connected to Fa0/1 or Fa0/2 of switches      | VLAN 10 or 20     |

---

##  Lab Objectives

-  Prevent loops using STP in a redundant Layer 2 topology
-  Configure VLANs for end-device segmentation
-  Trunk links between switches for VLAN propagation
-  Assign IP addresses to end devices and test connectivity
-  Set STP root bridge manually

---

##  Step-by-Step Lab Configuration

### Step 1️ – VLAN Configuration (On All Switches)

```bash
conf t
vlan 10
 name SALES
vlan 20
 name HR
exit
```

###  Step 2️ – Assign VLANs to Access Ports
on MLS1
```bash
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 10
exit
```
On MLS2:
```bash
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 20
exit
```
On MLS0:
```bash
interface fa0/1
 switchport mode access
 switchport access vlan 10

interface fa0/2
 switchport mode access
 switchport access vlan 20
exit
```
### Step 3️ – Configure Trunk Ports Between Switches
```bash
On Trunk Interfaces (Fa0/3 and Fa0/4 on all switches):\
interface range fa0/3 - 4
 switchport trunk encapsulation dot1q
 switchport mode trunk
exit
```

### Step 4️ – Assign IP Addresses to PCs
Open PC > Desktop > IP Configuration in Packet Tracer.

| PC  | IP Address    | VLAN | Connected To |
| --- | ------------- | ---- | ------------ |
| PC0 | 192.168.10.10 | 10   | MLS1 (Fa0/1) |
| PC3 | 192.168.10.11 | 10   | MLS1 (Fa0/2) |
| PC1 | 192.168.10.12 | 10   | MLS0 (Fa0/1) |
| PC2 | 192.168.20.10 | 20   | MLS2 (Fa0/1) |
| PC4 | 192.168.20.11 | 20   | MLS2 (Fa0/2) |

Subnet Mask: 255.255.255.0


### Step 5️ – Configure STP Root Bridge (On MLS0 Only)
```bash
conf t
spanning-tree vlan 1 priority 4096
exit
```
Or use this alternative:
```bash
spanning-tree vlan 1 root primary
```

### Step 6️ – Validate STP Operation
On all switches, run:
```bash
show spanning-tree
```
Check:

MLS0 is elected as root bridge.

One port in MLS1 or MLS2 is in blocking state.

No Layer 2 loop exists.

---

Testing and Validation

ping from PC0 to PC3 – Should succeed (same VLAN 10)

ping from PC2 to PC4 – Should succeed (same VLAN 20)

ping from PC0 to PC2 – Should fail (different VLANs)

Use: show interfaces trunk

to verify trunk ports.


---

 
### Key Learnings
Understand how STP elects the Root Bridge

Identify which ports are placed in Blocking State

Visualize STP convergence and loop prevention

Modify Bridge Priority to change Root Bridge election
---
### How to Run
Download the .pkt file from this repository

Open with Cisco Packet Tracer

Observe STP convergence

Run show spanning-tree on each switch to analyze behavior   
---
⭐ If you found this lab useful, give it a ⭐️ and follow for more networking labs!
