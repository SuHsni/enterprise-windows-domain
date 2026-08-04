# Domain Controller Promotion

## Overview

This document describes the promotion of the first Windows Server to a Domain Controller in the SuHaTech enterprise environment.

---

## Objective

Create the first Active Directory Forest and deploy the initial Domain Controller.

---

## Server

- Server Name: DC01
- Operating System: Windows Server 2025 Standard

---

## Forest

Pending...

## Domain Controller Options

| Setting                     | Value               |
| --------------------------- | ------------------- |
| Forest Functional Level     | Windows Server 2025 |
| Domain Functional Level     | Windows Server 2025 |
| DNS Server                  | Enabled             |
| Global Catalog              | Enabled             |
| Read Only Domain Controller | Disabled            |
| DSRM Password               | Configured          |

## NetBIOS Name

| Setting             | Value |
| ------------------- | ----- |
| NetBIOS Domain Name | CORP  |

### Notes

The default NetBIOS name was accepted because it matches the corporate naming convention.

## Database Paths

| Component | Path              |
| --------- | ----------------- |
| Database  | C:\Windows\NTDS   |
| Log Files | C:\Windows\NTDS   |
| SYSVOL    | C:\Windows\SYSVOL |

### Notes

The default paths were selected because this is a single-server homelab environment. In enterprise deployments, databases and log files are commonly stored on separate storage volumes for improved performance and resilience.

## Domain

Pending...

## Promotion Status

In Progress
