# File Server Implementation

## Objective

The objective of this phase is to implement a centralized file sharing solution in the Active Directory environment.

The File Server is used to store organizational data, provide shared folders, and manage access permissions based on Active Directory Security Groups.

---

## Environment

Domain:

```

corp.suhatech.local

```

Server:

```

DC01

```

## Lab Environment Note

In a production environment, the File Server role should be installed on a dedicated server (FS01) to provide better security, performance, and role separation.

Due to limited hardware resources in this lab environment, the File Server role was configured on the existing Domain Controller (DC01).

Current lab architecture:

```

DC01

├── Active Directory Domain Services
├── DNS
├── Group Policy
└── File Server

```

---

# Creating File Storage Structure

A main directory was created on the server to store department shares.

Path:

```

C:\Shares

```

The following departmental folders were created:

```

C:\Shares

├── HR
├── IT
├── Finance
├── Management
└── Public

```

Each folder represents a department resource that will be accessed through network sharing.

---

# Configuring Shared Folders

The created folders were configured as network shares.

Example share paths:

```

\DC01\HR

\DC01\IT

\DC01\Finance

\DC01\Management

\DC01\Public

```

Share permissions were initially configured for setup purposes and later restricted using security groups.

---

# Security Groups

Access control was managed using Active Directory Security Groups.

The following groups were used:

```

SG_HR

SG_IT

SG_Finance

SG_Management

```

Security Groups allow administrators to manage permissions centrally instead of assigning permissions directly to individual users.

---

# NTFS Permission Configuration

NTFS permissions were assigned based on department responsibility.

Configuration:

```

HR Folder

SG_HR → Modify

```

```

IT Folder

SG_IT → Modify

```

```

Finance Folder

SG_Finance → Modify

```

```

Management Folder

SG_Management → Modify

```

Modify permission allows users to create, edit, and delete files inside their department folder.

---

# Share Permission Configuration

Initially, the following permission was configured:

```

Everyone → Full Control

```

After configuring Security Groups, the default Everyone access was removed.

Each share was configured with its related security group.

Example:

```

HR Share

SG_HR → Full Control

```

The final access control was based on the combination of:

- Share Permissions
- NTFS Permissions
- Active Directory Security Groups

---

# User Access Management

Users were assigned to the appropriate Security Groups in Active Directory.

Example:

```

User:

HR_User

Member Of:

SG_HR

```

Access flow:

```

User

↓

Security Group

↓

Folder Permission

↓

File Access

```

This method provides centralized and scalable permission management.

---

# Final Structure

```

C:\Shares

├── HR
│   └── SG_HR → Modify
│
├── IT
│   └── SG_IT → Modify
│
├── Finance
│   └── SG_Finance → Modify
│
├── Management
│   └── SG_Management → Modify
│
└── Public

```

---

# Limitations

Client-side access testing was not performed because an additional Windows client machine was not available in this lab environment.

The configuration and permission structure were completed on the server side.

---

# Summary

In this implementation:

- A centralized file storage structure was created.
- Department-based shared folders were configured.
- Active Directory Security Groups were used for access management.
- NTFS and Share Permissions were configured.
- File access was managed using a group-based permission model.

This project demonstrates the basic implementation of Windows Server File Services integrated with Active Directory.
