# Active Directory Domain Services Installation

## Overview

This document describes the installation of the Active Directory Domain Services (AD DS) role on the first Windows Server of the SuHaTech environment.

---

# Objective

Install the AD DS role required for deploying the first Active Directory forest.

---

# Installation Method

PowerShell

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

---

# Verification

The following command was executed to verify the installation:

```powershell
Get-WindowsFeature AD-Domain-Services
```

Result:

- AD DS Installed: ✅

---

# Current Status

| Component                   | Status |
| --------------------------- | ------ |
| AD DS Role Installed        | ✅     |
| Forest Created              | ❌     |
| Domain Controller Promotion | ❌     |

---

# Next Step

Promote the server to the first Domain Controller by creating the initial Active Directory forest.
