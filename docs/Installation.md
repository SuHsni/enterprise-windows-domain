# Windows Server Installation

## Overview

This document describes the deployment of the first Windows Server for the **SuHaTech** enterprise environment.

The server will be prepared as the first Domain Controller in a future phase.

---

# Objective

Deploy a clean Windows Server installation and verify the initial operating system configuration before introducing Active Directory services.

---

# Virtual Machine Information

| Setting                | Value                                      |
| ---------------------- | ------------------------------------------ |
| Hypervisor             | VMware Workstation                         |
| Guest Operating System | Microsoft Windows Server 2025 Standard     |
| Computer Name          | DC01                                       |
| Architecture           | x64                                        |
| Virtual CPU            | 1 vCPU                                     |
| Memory                 | 4095 MB                                    |
| Network Adapter        | Intel(R) 82574L Gigabit Network Connection |
| Network Mode           | NAT                                        |
| IP Address             | 192.168.93.10                              |
| Domain Membership      | WORKGROUP                                  |
| Time Zone              | UTC +03:30 (Tehran)                        |

---

# Operating System Information

| Setting           | Value      |
| ----------------- | ---------- |
| Version           | 10.0.26100 |
| Build             | 26100      |
| Installation Date | 2026-07-21 |
| Manufacturer      | Microsoft  |

---

# Current Configuration

| Item                       | Status |
| -------------------------- | ------ |
| Windows Installed          | ✅     |
| Computer Renamed           | ✅     |
| Static IPv4 Configured     | ✅     |
| Active Directory Installed | ❌     |
| DNS Server Configured      | ❌     |
| Domain Controller          | ❌     |

---

# Validation

The operating system boots successfully.

The server is reachable on the local network.

The hostname is configured as **DC01**.

The server currently operates as a standalone server and is ready for Active Directory deployment.

---

# Next Step

Install the Active Directory Domain Services (AD DS) role and promote the server to the first Domain Controller for the SuHaTech environment.
