# Group Policy Implementation

## Objective

Create and configure a Group Policy Object (GPO) in Active Directory to restrict user access to Control Panel and Windows Settings.

## Creating GPO

From Domain Controller:

Server Manager
→ Tools
→ Group Policy Management

Navigate to:

Forest
→ Domains
→ corp.suhatech.local
→ Group Policy Objects

Create a new GPO:

Disable Control Panel

---

## Configuring GPO

Edit the created GPO and navigate to:

User Configuration
→ Administrative Templates
→ Control Panel

Enable the policy:

Prohibit access to Control Panel and PC settings

---

## Linking GPO

The GPO was linked to the Users OU:

corp.suhatech.local
→ Users OU
→ Disable Control Panel

This policy uses **User Configuration**, therefore it applies to user accounts inside the linked OU.

---

## Summary

This implementation demonstrates creating a GPO, configuring Administrative Template settings, and linking the policy to an Organizational Unit in Active Directory.
