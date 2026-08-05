# Client Creation and Domain Join Journey

## Objective

After creating the Active Directory environment, the next required step was adding a client computer to the domain.

The purpose was to create a realistic lab environment similar to a small company network:

            Domain Controller

          corp.suhatech.local

                  |

                  |

           Client Computer

The Domain Controller was already prepared with:

- Active Directory Domain Services
- Domain Configuration
- Users
- Security Groups

The missing part was creating a client machine and successfully joining it to the domain.

---

# Initial Problem: How to Create a Client Machine?

The first idea was creating another virtual machine and installing Windows 11.

The expected architecture was:

Windows 10 Host

|
|

Windows Server VM
(Domain Controller)

|
|

Windows 11 VM
(Client)

However, the host system had limited resources:

Host Operating System:

Windows 10

RAM:

8 GB

Running:

- Windows 10 Host
- Windows Server VM
- Windows 11 Client VM

at the same time would create performance issues.

Because the purpose was learning Active Directory, not testing Windows 11 itself, another method was needed.

---

# Reviewing Available Operating System Options

At this stage, available ISO files on the system were reviewed to find the fastest possible client solution.

The goal was:

- Use existing resources
- Avoid unnecessary hardware pressure
- Complete Domain Join testing

---

# Linux Client Consideration

Available Linux images included:

- Kali Linux
- Tails OS
- Ubuntu

Linux systems can technically communicate with Active Directory using technologies such as Samba and Kerberos.

However, they were not selected for this stage.

The reason was not that they cannot work.

The reason was that the current objective was Windows Active Directory administration:

- Windows Domain Join
- Windows Authentication
- Security Groups
- Group Policy
- Windows Client Management

Using Linux would introduce additional configuration unrelated to the current goal.

Therefore Linux clients were postponed for a future Active Directory + Linux integration lab.

---

# Windows 7 Client Consideration

Another option was Windows 7.

Two possible approaches were considered.

## Windows 7 Virtual Machine

Advantages:

- Requires fewer resources
- Suitable for Active Directory client testing
- Useful for creating additional clients later

This option was not rejected.

It was kept as a possible future client machine.

---

## Physical Windows 7 Laptop

A second laptop available at home was running Windows 7.

This machine could potentially be joined directly to the domain.

Advantages:

- Real physical client
- No VM resource consumption

However, this option was postponed because the current goal was completing the lab with the available main system.

The Windows 7 laptop remains a possible future domain client.

---

# Final Decision

Considering:

- Limited RAM
- Available hardware
- Time constraints
- Current learning objective

the decision was made to use the existing Windows 10 host machine as the domain client.

Final architecture:

Windows Server VM

Role:
Domain Controller

IP:
192.168.1.10

    Network

Windows 10 Physical Machine

Role:
Domain Client

IP:
192.168.1.8

---

# Network Challenge: VMware NAT

Initially, the Windows Server VM used NAT networking.

The network configuration was:

Server:

192.168.93.10

Host:

192.168.1.8

The problem:

Both devices were in different networks.

The client could not communicate properly with the Domain Controller.

For Active Directory Join, the client must reach:

- Domain Controller
- DNS
- Active Directory services

---

# Changing VMware Network Mode

The VMware network adapter was changed:

Before:

NAT

After:

Bridged Adapter

The bridge was connected to the physical Wi-Fi adapter.

After this change:

Server received:

192.168.1.10

Client:

192.168.1.8

Both systems were now inside the same network.

---

# DNS Configuration Challenge

After network connectivity was established, the next problem was DNS.

Active Directory depends heavily on DNS.

The client initially used:

Automatic DNS

provided by the home router.

This is not suitable for Active Directory because the client must find domain services through the Domain Controller DNS.

The DNS configuration was changed:

Preferred DNS:

192.168.1.10

---

# Internet Dependency Issue

After changing client DNS to the Domain Controller, an additional behavior was observed.

When the Domain Controller was powered off:

- Domain resources were unavailable
- Internet name resolution also stopped

The reason was:

The client was asking only the Domain Controller for DNS resolution.

This demonstrated the importance of DNS availability in Active Directory environments.

---

# Domain Join

After completing:

- Network configuration
- DNS configuration
- Connectivity testing

The Windows 10 client was joined to:

corp.suhatech.local

Authentication:

corp\Administrator

Successful result:

Welcome to the corp.suhatech.local domain

The Windows 10 machine successfully became a member of the Active Directory domain.

---

# Lessons Learned

During this stage, the main challenges were:

1. Limited hardware resources prevented creating a Windows 11 VM.

2. Client selection required evaluating available operating systems.

3. VMware NAT isolated the Domain Controller from the client.

4. Active Directory requires correct DNS configuration.

5. Domain environments depend on available infrastructure services.

---

# Current Result

Completed:

[x] Client machine selection

[x] Network configuration

[x] DNS configuration

[x] Domain Join
