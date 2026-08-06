# Client Creation and Domain Join Journey

## Active Directory Lab - Client Deployment Phase

## Objective

After successfully preparing the Active Directory environment, the next required step was creating a client machine and joining it to the domain.

The goal was to build a small enterprise-like lab environment where a Domain Controller could manage client computers.

The expected architecture:

```
                 Domain Controller

                 Windows Server VM

                      |

                      |

                Client Computer
```

The Active Directory environment was already prepared with:

- Active Directory Domain Services
- Domain Controller configuration
- Domain name
- Organizational Units (OUs)
- Users
- Security Groups

The remaining task was adding a client machine to the domain and testing:

- Domain Join
- Domain Authentication
- User Login
- Future Group Policy deployment

---

# Initial Challenge: Creating a Domain Client

The first planned solution was creating another virtual machine and installing Windows 11 as the client operating system.

The expected architecture was:

```
Windows 10 Host

      |

      |

Windows Server VM
Domain Controller

      |

      |

Windows 11 VM
Domain Client
```

This approach would represent a common enterprise environment where multiple virtual machines simulate company infrastructure.

However, the host machine had limited hardware resources.

## Host System Specifications

Operating System:

```
Windows 10
```

RAM:

```
8 GB
```

Current usage:

- Windows 10 Host
- Windows Server Virtual Machine

Adding another Windows 11 Virtual Machine would require additional memory and CPU resources.

Because the main objective was learning Active Directory administration, not testing Windows 11 itself, creating a Windows 11 VM was considered inefficient for this environment.

Therefore, alternative client solutions were evaluated.

---

# Reviewing Available Client Options

Because the available hardware resources were limited, existing operating systems and devices were reviewed.

The requirements for the client were:

- Windows-based client preferred
- Ability to join Active Directory Domain
- Ability to test authentication
- Ability to use future Group Policy scenarios
- Minimum additional resource usage

Several options were considered.

---

# Option 1: Windows 11 Virtual Machine

## Consideration

Windows 11 VM was the initial plan.

Advantages:

- Modern Windows operating system
- Realistic enterprise client
- Full compatibility with modern Active Directory environments

## Problem

The host system had only 8GB RAM.

Running:

- Windows 10 Host
- Windows Server Domain Controller VM
- Windows 11 Client VM

would cause:

- High RAM usage
- Slow performance
- Possible instability

## Decision

This option was postponed because the hardware limitation was more important than having the newest client operating system.

---

# Option 2: Linux Client Investigation

Available ISO files on the system were reviewed.

Available Linux distributions:

- Kali Linux
- Tails OS
- Ubuntu

The possibility of using Linux as an Active Directory client was considered.

Linux systems can integrate with Active Directory using technologies such as:

- Samba
- Kerberos
- LDAP
- Winbind

However, this was not selected for the current stage.

## Reason

The purpose of this lab was specifically Windows Active Directory administration:

- Windows Domain Join
- Windows Authentication
- Security Group Management
- Organizational Unit Management
- Group Policy Deployment
- Windows Client Administration

Using Linux would introduce additional topics:

- Linux domain integration
- Samba configuration
- Kerberos troubleshooting

These topics are valuable, but they were outside the current learning objective.

## Decision

Linux clients were postponed for a future:

```
Active Directory + Linux Integration Lab
```

---

# Option 3: Windows 8 Physical Laptop

Another available device was a second laptop running:

```
Windows 8
```

This option was considered because:

- It was already available
- It did not require additional VM resources
- It could act as a real physical domain client

Advantages:

- Real hardware client
- No additional RAM usage on the main system
- Suitable for Active Directory testing

However, this option was not immediately used because the initial goal was to complete the configuration using the existing main machine.

The Windows 8 laptop was kept as a possible secondary client for later testing.

---

# Option 4: Creating an Older Windows VM

Creating an additional lightweight Windows client VM was also considered.

A lightweight older Windows version could reduce resource consumption compared with Windows 11.

This option was not completely rejected.

It remained a possible solution for future scenarios where multiple clients are required.

For example:

- Testing different Group Policies
- Creating multiple organizational units with different client machines
- Simulating a larger company environment

---

# Final Client Decision

Considering:

- Limited RAM
- Available hardware
- Time limitations
- Learning objectives

the decision was made to use the existing Windows 10 host machine as the first domain client.

Advantages:

- No additional VM required
- No extra RAM consumption
- Real Windows environment
- Fastest way to test Domain Join

Final planned architecture:

```
Windows Server VM

Role:
Domain Controller

Domain:
corp.suhatech.local

IP:
192.168.1.10


          Network


Windows 10 Physical Host

Role:
Domain Client

IP:
192.168.1.8
```

---

# Network Configuration Challenge

## Initial VMware NAT Configuration

The Domain Controller virtual machine was initially configured with VMware NAT networking.

Initial server configuration:

```
Server IP:

192.168.93.10
```

The Windows 10 host machine had:

```
192.168.1.8
```

The problem was that both devices were located in different network ranges.

Server:

```
192.168.93.x
```

Client:

```
192.168.1.x
```

For Active Directory operations, the client must communicate directly with:

- Domain Controller
- DNS Server
- LDAP services
- Kerberos authentication services

The NAT configuration was not suitable for this lab design.

# Changing VMware Network Mode

After identifying the network isolation problem caused by NAT, the VMware network configuration was reviewed.

The goal was to place both systems in the same network so the client could communicate directly with the Domain Controller.

## Previous Configuration

VMware Adapter:

```text
NAT
```

Network result:

```text
Domain Controller:
192.168.93.10

Windows 10 Client:
192.168.1.8
```

Because both devices were in different networks, Active Directory communication was unreliable.

---

## Bridge Adapter Configuration

The VMware network adapter was changed from:

```text
NAT
```

to:

```text
Bridged Adapter
```

During the configuration, VMware required selecting the physical network adapter.

The bridge was initially checked and corrected to use the physical Wi-Fi adapter.

After applying the change, the Domain Controller received an IP address from the same network as the host machine.

New configuration:

Domain Controller:

```text
IP Address:
192.168.1.10
```

Windows 10 Host:

```text
IP Address:
192.168.1.8
```

Both systems were now inside the same network.

---

# Network Connectivity Testing

After changing the network mode, connectivity was tested.

## Testing Client Reachability

From the Domain Controller:

```cmd
ping 192.168.1.8
```

After network correction, communication became possible.

## Testing Internet Access

The Domain Controller was also tested:

```cmd
ping google.com
```

Internet connectivity was successful.

This confirmed that the Domain Controller had both:

- Network connectivity
- Internet access

---

# DNS Configuration Challenge

After solving the network problem, the next challenge was DNS.

Active Directory depends heavily on DNS.

In a domain environment, clients must be able to locate:

- Domain Controllers
- Kerberos services
- LDAP services
- Domain records

Initially, the client was using automatic DNS settings provided by the home router.

Example:

```text
Automatic DNS
```

This configuration works for normal internet usage but is not suitable for Active Directory.

A domain client should use the Domain Controller as its primary DNS server.

---

# Changing Client DNS Configuration

The Windows client DNS was changed manually.

Preferred DNS:

```text
192.168.1.10
```

The Domain Controller became responsible for resolving domain records.

After the change:

DNS cache was cleared:

```cmd
ipconfig /flushdns
```

DNS resolution was tested:

```cmd
nslookup corp.suhatech.local
```

Result:

```text
Name:
corp.suhatech.local

Address:
192.168.1.10
```

This confirmed that the client could locate the Active Directory domain.

---

# Internet Dependency Observation

After changing the DNS configuration, an important behavior was observed.

When the Domain Controller virtual machine was turned off:

- Domain services were unavailable.
- DNS resolution was affected.

The reason was that the client was configured to use only the Domain Controller as its DNS server.

In an enterprise environment, this situation is normally prevented by:

- Multiple Domain Controllers
- DNS redundancy
- Proper DNS forwarding configuration

This troubleshooting process demonstrated the importance of DNS availability in Active Directory environments.

---

# Successful Domain Join - Windows 10 Host

After completing:

- Network configuration
- DNS configuration
- Connectivity tests

the Windows 10 host machine was joined to the domain.

Domain:

```text
corp.suhatech.local
```

Authentication was performed using the domain administrator account.

The join process completed successfully.

The confirmation message appeared:

```text
Welcome to the corp.suhatech.local domain
```

The computer object was also visible inside Active Directory.

At this stage:

- Domain Controller was working.
- Client communication was working.
- Domain Join functionality was confirmed.

---

# First Client Limitation: Testing Domain User Login

The next step was testing login with a normal domain user.

However, the Windows 10 host had a special limitation.

The Domain Controller was running as a VMware virtual machine on the same physical host system.

During testing:

- The user session on Windows 10 was signed out.
- The VMware environment state changed.
- The Domain Controller virtual machine became suspended/unavailable.

Because Active Directory authentication requires communication with the Domain Controller during login, testing the domain user login on this client was unreliable.

The issue was not caused by Active Directory configuration.

The limitation was related to the lab architecture.

---

# Moving to a Second Physical Client

To continue testing without depending on the host machine environment, the second available laptop was used.

The laptop operating system was:

```text
Windows 8
```

The purpose was:

- Create a real client machine
- Join it to the domain
- Test domain user authentication
- Prepare for future Group Policy testing

---

# Windows 8 Client Network Configuration

The Windows 8 laptop was connected to the same network.

The Domain Controller:

```text
192.168.1.10
```

The client DNS was changed to:

```text
192.168.1.10
```

This allowed the client to locate:

```text
corp.suhatech.local
```

---

# Connectivity Verification on Windows 8 Client

Network communication was tested.

## Ping Test

Command:

```cmd
ping 192.168.1.10
```

Result:

Successful replies received.

This confirmed that the client could reach the Domain Controller.

---

## DNS Test

Command:

```cmd
nslookup corp.suhatech.local
```

Result:

```text
Server:
192.168.1.10

Name:
corp.suhatech.local

Address:
192.168.1.10
```

DNS resolution was successful.

---

# Windows 8 Domain Join

The Windows 8 laptop was joined to:

```text
corp.suhatech.local
```

The computer successfully became a member of the Active Directory domain.

The machine appeared inside Active Directory Computers.

---

# Domain User Authentication Test

After successful domain join, a normal domain user was tested.

User:

```text
Sara Mohammadi
```

The login attempt reached the domain but failed during profile creation.

Error:

```text
The User Profile Service service failed the sign-in.
User profile cannot be loaded.
```

---

# Troubleshooting User Profile Creation

The client was checked for profile creation.

Path:

```text
C:\Users
```

A folder existed:

```text
sara.mohammadi
```

However, the folder was empty.

This indicated:

- Authentication reached the domain.
- Windows started creating the local profile.
- Profile creation failed before completion.

---

# Testing With Another Domain User

To confirm that the issue was not related to Sara's account, another domain user was tested.

The same error appeared:

```text
The User Profile Service service failed the sign-in.
```

Conclusion:

The problem was not:

- User account
- Password
- Active Directory user creation

The issue was related to the Windows 8 client profile creation process.

---

# Current Status of Client Deployment Phase

## Completed Successfully

[x] Active Directory Domain Controller created

[x] Domain configured

[x] Users created

[x] Security Groups created

[x] Organizational Units created

[x] Client selection process completed

[x] VMware networking configured

[x] NAT issue resolved

[x] Bridge networking configured

[x] DNS configured correctly

[x] Windows 10 Host joined to domain

[x] Windows 8 Laptop joined to domain

[x] Domain connectivity verified

---

# Remaining Limitation

The current limitation is:

A healthy client environment is still required for final validation of:

- Domain User desktop login
- Group Policy application
- User-based policies
- Computer-based policies

The Active Directory infrastructure itself is functional.

The remaining issue is isolated to the client-side profile creation process.

---

# Next Steps

The next stages of the Active Directory lab:

1. Continue Active Directory administration from the Domain Controller.

2. Configure Group Policy Objects (GPO).

3. Link policies to Organizational Units.

4. Later verify policies using a stable Windows client.

---

# Final Lessons Learned

During this phase, the following practical lessons were learned:

1. Hardware limitations directly affect lab architecture decisions.

2. Not every operating system is suitable for every Active Directory scenario.

3. Linux can integrate with Active Directory, but Windows clients are preferred for Windows administration labs.

4. VMware networking configuration is critical for domain environments.

5. Active Directory depends heavily on DNS.

6. Successful Domain Join does not always guarantee successful user login.

7. Client troubleshooting is a separate process from Domain Controller troubleshooting.

8. Real enterprise troubleshooting requires separating:
   - Server problems
   - Network problems
   - DNS problems
   - Client problems
   - User problems
