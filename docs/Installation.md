# Windows Server Installation

## Overview

This document describes the initial deployment and validation of the first Windows Server in the SuHaTech enterprise environment.

The server will later be promoted to the first Domain Controller after the infrastructure prerequisites are verified.

---

# Objective

Deploy a clean installation of Windows Server 2025 and verify that the operating system and network configuration are ready for Active Directory deployment.

---

# Virtual Machine Information

| Setting                | Value                                      |
| ---------------------- | ------------------------------------------ |
| Hypervisor             | VMware Workstation                         |
| Guest Operating System | Microsoft Windows Server 2025 Standard     |
| Computer Name          | DC01                                       |
| Architecture           | x64                                        |
| Processor              | Intel Core i7-6500U (Virtualized)          |
| vCPU                   | 1                                          |
| Memory                 | 4095 MB                                    |
| Network Adapter        | Intel(R) 82574L Gigabit Network Connection |
| Link Speed             | 1 Gbps                                     |

---

# Operating System

| Setting           | Value              |
| ----------------- | ------------------ |
| Version           | 10.0.26100         |
| Build             | 26100              |
| Installation Date | 2026-07-21         |
| Time Zone         | UTC+03:30 (Tehran) |
| Current Role      | Standalone Server  |

---

# Network Configuration

| Setting            | Value         |
| ------------------ | ------------- |
| Interface          | Ethernet0     |
| Address Assignment | Static        |
| IPv4 Address       | 192.168.93.10 |
| Prefix Length      | /24           |
| Subnet Mask        | 255.255.255.0 |
| Default Gateway    | 192.168.93.2  |
| DNS Server         | 192.168.93.10 |

---

# Verification

The following validation steps were completed successfully:

- Windows Server installed successfully
- Computer renamed to **DC01**
- Static IPv4 configuration verified
- Network adapter operational (Up)
- Link speed verified (1 Gbps)
- Gateway configuration verified
- DNS configuration verified

---

# Current Status

| Component                   | Status     |
| --------------------------- | ---------- |
| Windows Installation        | ✅         |
| Server Rename               | ✅         |
| Static IPv4                 | ✅         |
| Network Verification        | ✅         |
| Active Directory            | ⏳ Pending |
| DNS Role                    | ⏳ Pending |
| Domain Controller Promotion | ⏳ Pending |

---

# Next Step

Install the Active Directory Domain Services (AD DS) role and promote this server to the first Domain Controller of the SuHaTech environment.
