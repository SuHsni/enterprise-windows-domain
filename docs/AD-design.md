# Active Directory Design

## Project

SuHaTech Enterprise Infrastructure

---

# Objective

Design the Active Directory infrastructure for the SuHaTech internal corporate network.

The purpose of this document is to define the logical structure before deploying the first Active Directory forest.

---

# Forest Design

Forest Name

corp.suhatech.local

Reason:

A single forest is sufficient for the current size of the organization and allows future expansion if additional domains are required.

---

# Domain Design

Domain Name

corp.suhatech.local

Reason:

Using a dedicated internal corporate namespace keeps the environment organized and clearly separated from public internet domains.

---

# Domain Controller

Server Name

DC01

Roles

- Active Directory Domain Services
- DNS Server

Reason

The first server will host both AD DS and DNS to simplify the initial deployment.

---

# Organizational Unit Structure

corp.suhatech.local

├── Servers
├── Workstations
├── Users
│   ├── IT
│   ├── HR
│   ├── Finance
│   └── Management
├── Groups
├── Service Accounts
└── Admins

Reason

The OU structure follows the organizational departments and separates infrastructure objects for easier administration and Group Policy management.

---

# Naming Convention

| Object | Convention |
|---------|------------|
| Domain Controller | DC01 |
| File Server | FS01 |
| Web Server | WEB01 |
| Workstations | IT-PC01, HR-PC01 |
| Users | firstname.lastname |
| Groups | Department_Role |

---

# Future Expansion

Future infrastructure may include:

- Additional Domain Controllers
- File Server
- Linux Servers
- Windows Clients
- Security Monitoring
- PowerShell Automation

---

# Current Status

Design Approved

Implementation Pending