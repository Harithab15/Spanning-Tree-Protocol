# Spanning Tree Protocol (STP) Lab – Cisco Packet Tracer

This lab demonstrates how **Spanning Tree Protocol (STP)** prevents Layer 2 loops by electing a root bridge and blocking redundant paths in a switched network. The topology is designed and tested using **Cisco Packet Tracer**.

![Lab Screenshot](./stp_lab_topology.png) <!-- Add your image here with same name -->

---

## Lab Objective

To understand and simulate **Spanning Tree Protocol** in action, analyze port roles (Root, Designated, Blocking), and observe loop prevention mechanisms in a switched network environment.

---

## Topology Overview

- **3 Switches**: Switch1 (SW1), Switch2 (SW2), Switch3 (SW3)
- **2 PCs**: PC0 and PC1 connected to edge switches
- **Inter-Switch Links**: Redundant links to create Layer 2 loop scenario
- **Spanning Tree Behavior**: Observe which switch becomes the **Root Bridge**, and which ports are placed in **Blocking State**

---

## Step-by-Step Lab Guide

### 1. Device Configuration

**Switch1 (SW1):**
```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
Switch(config)# spanning-tree vlan 1 priority 24576
Switch(config)# exit
```
###  Switch2 (SW2):
```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW2
Switch(config)# spanning-tree vlan 1 priority 28672
Switch(config)# exit
```
###  Switch3 (SW3):
```bash
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW3
Switch(config)# spanning-tree vlan 1 priority 32768
Switch(config)# exit
```
### 2. PC IP Configuration
   | PC  | IP Address   | Subnet Mask   | Default Gateway |
| --- | ------------ | ------------- | --------------- |
| PC0 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1     |
| PC1 | 192.168.1.20 | 255.255.255.0 | 192.168.1.1     |

Use IP Configuration in Packet Tracer for each PC.

### 3. Observe STP Behavior
Wait for 30-60 seconds for STP convergence.

Use the CLI command below to verify STP status:
```bash
SW1# show spanning-tree
```
Verify:

Root Bridge ID

Port roles: Root Port (RP), Designated Port (DP), and Blocking

### Key Learnings
Understand how STP elects the Root Bridge

Identify which ports are placed in Blocking State

Visualize STP convergence and loop prevention

Modify Bridge Priority to change Root Bridge election

### How to Run
Download the .pkt file from this repository

Open with Cisco Packet Tracer

Observe STP convergence

Run show spanning-tree on each switch to analyze behavior   

⭐ If you found this lab useful, give it a ⭐️ and follow for more networking labs!
