# Organizational Unit Design

## Overview

This document describes the Organizational Unit (OU) structure for the SuHaTech enterprise Active Directory environment.

The design follows common enterprise best practices by separating users, computers, servers, groups, service accounts, and administrative accounts into dedicated Organizational Units.

---

## Objectives

- Improve administrative organization
- Simplify Group Policy deployment
- Delegate administration securely
- Prepare the environment for future growth

---

## Planned OU Structure

corp.suhatech.local

├── Admin

├── Groups

├── Servers

├── Workstations

├── Users

│ ├── IT

│ ├── HR

│ ├── Finance

│ └── Management

└── Service Accounts

---

## Design Principles

- Users are separated by department.
- Servers and Workstations are managed independently.
- Administrative accounts are isolated.
- Security Groups are managed separately from users.
- Service accounts are isolated for better security.

---

## Status

🚧 Design Completed

Deployment will be performed in the next phase.

---

## Deployment Status

The Organizational Unit structure has been successfully created.

### Implemented OUs

- Admin
- Groups
- Servers
- Service Accounts
- Users
  - IT
  - HR
  - Finance
  - Management
- Workstations

The default Active Directory containers were preserved to maintain compatibility with built-in Windows components.
