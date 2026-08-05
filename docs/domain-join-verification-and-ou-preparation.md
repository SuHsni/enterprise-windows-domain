# Domain Join Verification and OU Preparation

## Objective

After joining the Windows 10 client to the Active Directory domain, several verification steps were performed to confirm that the environment was operating correctly before deploying any Group Policy Objects (GPOs).

Following the verification process, the client computer was organized into the appropriate Organizational Unit (OU) to follow Active Directory best practices and prepare the environment for centralized policy management.

---

# Verification Steps

## 1. Network Connectivity

Connectivity between the Windows 10 client and the Domain Controller was verified.

Command used:

```cmd
ping 192.168.1.10
```

Result:

Successful replies confirmed that the client could communicate with the Domain Controller.

Status:

✅ Passed

---

## 2. DNS Resolution

The client was configured to use the Domain Controller as its DNS server.

Command used:

```cmd
nslookup corp.suhatech.local
```

Result:

The domain name resolved successfully to the Domain Controller IP address.

Status:

✅ Passed

---

## 3. Domain Membership Verification

The client machine was verified as a member of the following domain:

```
corp.suhatech.local
```

Commands used:

```cmd
systeminfo
```

and

```cmd
wmic computersystem get domain
```

Result:

The system reported the correct Active Directory domain.

Status:

✅ Passed

---

## 4. Domain Controller Name Resolution

Hostname resolution was verified.

Command:

```cmd
ping DC01
```

Result:

The Domain Controller hostname resolved correctly.

Status:

✅ Passed

---

## 5. Computer Object Verification

The joined Windows 10 client appeared successfully inside Active Directory Users and Computers.

Initial location:

```
Computers
```

Status:

✅ Passed

---

# Preparing the Environment for Group Policy

Although Windows automatically places newly joined computers inside the default **Computers** container, this location is not intended for long-term administration.

To follow Active Directory organizational best practices, the client computer was moved into the dedicated **Workstations** Organizational Unit.

Structure before:

```
corp.suhatech.local
│
├── Computers
│     └── DESKTOP-XXXX
│
└── Workstations
```

Structure after:

```
corp.suhatech.local
│
├── Computers
│
└── Workstations
      └── DESKTOP-XXXX
```

This organizational structure allows future Group Policy Objects (GPOs) to target only workstation computers without affecting servers or domain controllers.

Status:

✅ Completed

---

# Authentication Verification

During the domain join process, Windows displayed the following message:

```
Welcome to the corp.suhatech.local domain
```

This confirmed that the join operation completed successfully.

Status:

✅ Passed

---

# Observation

During testing, an authentication error occurred after signing out of Windows.

```
We can't sign you in with this credential because your domain isn't available.
```

Investigation showed that the VMware virtual machine containing the Domain Controller had entered the **Suspended** state.

Since the Domain Controller was temporarily unavailable, domain authentication requests could not be processed.

After resuming the virtual machine, domain services became available again.

This behavior demonstrates the dependency of domain authentication on Domain Controller availability, especially during a user's first domain sign-in.

---

# Verification Summary

Completed successfully:

- Network connectivity
- DNS resolution
- Domain membership
- Domain Controller reachability
- Computer object verification
- Organizational Unit preparation
- Successful domain join

The Active Directory environment is now prepared for Group Policy deployment.