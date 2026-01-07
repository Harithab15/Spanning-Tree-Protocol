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








 
### 2. PC IP Configuration
   | PC  | IP Address   | Subnet Mask   | Default Gateway |
| --- | ------------ | ------------- | --------------- |
| PC0 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1     |
| PC1 | 192.168.1.20 | 255.255.255.0 | 192.168.1.1     |

Use IP Configuration in Packet Tracer for each PC.

---
### 3. Observe STP Behavior
Wait for 30-60 seconds for STP convergence.

Use the CLI command below to verify STP status:
```bash
SW1# show spanning-tree
```
---
### Verify:

Root Bridge ID
Port roles: Root Port (RP), Designated Port (DP), and Blocking

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
