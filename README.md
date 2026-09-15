# Enterprise Directory Services & Remote Access Lab

A hands-on enterprise IT lab built using **Oracle VirtualBox, Windows Server 2022, Windows 11, and Active Directory Domain Services (AD DS)**.

The project simulates a small corporate IT environment where I configured centralized identity management, organizational units, security groups, Group Policy, networking, and help-desk administration scenarios.

---

## Lab Architecture

The lab was built using Oracle VirtualBox with a Windows Server 2022 domain controller and a Windows 11 client.

```text
                         MY PC
                           │
                     Oracle VirtualBox
                           │
              ┌────────────┴────────────┐
              │                         │
       Windows Server 2022        Windows 11 Client
            "DC01"                    "PC01"
              │                         │
              └──────────┬──────────────┘
                         │
                    IT-LAB NETWORK
                         │
                   192.168.50.0/24
```

### Virtual Machines

| System              | Hostname | Role                      |
| ------------------- | -------- | ------------------------- |
| Windows Server 2022 | DC01     | Domain Controller / AD DS |
| Windows 11          | PC01     | Domain Client             |
| Oracle VirtualBox   | —        | Virtualization Platform   |

---

# 1. Lab Environment Setup

The first step was setting up the virtualized environment using Oracle VirtualBox.

I created a Windows Server 2022 virtual machine to act as the domain controller and a Windows 11 virtual machine to act as the client workstation.

<p align="center">
  <img src="https://github.com/user-attachments/assets/3abf2994-b73c-477e-8001-71d970857a73"
       width="750"
       alt="Windows Server 2022 virtual machine configured in Oracle VirtualBox">
</p>

<p align="center">
  <em>Windows Server 2022 virtual machine configured in Oracle VirtualBox.</em>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8fa91e04-bf66-47fe-8014-3f728c03be0c"
       width="750"
       alt="Successfully installed Windows Server 2022">
</p>

<p align="center">
  <em>Windows Server 2022 successfully installed.</em>
</p>

---

# 2. Network & IP Configuration

After creating the virtual machines, I configured the server's network adapters.

The server uses two network interfaces:

```text
                         DC01
                          │
               ┌──────────┴──────────┐
               │                     │
           Adapter 1             Adapter 2
              NAT                 IT-LAB
               │                     │
           Internet              Private LAN
```

The internal IT-LAB network uses:

```text
Network: 192.168.50.0/24
```

The second adapter provides connectivity between the domain controller and the Windows 11 client.

<p align="center">
  <img src="https://github.com/user-attachments/assets/752d170b-4e6e-4eba-92f6-cc1589a48a38"
       width="700"
       alt="Configuring TCP IPv4 settings for the IT-LAB network adapter">
</p>

<p align="center">
  <em>Configuring TCP/IPv4 settings for the internal IT-LAB network.</em>
</p>

### DHCP Configuration

I also configured the DHCP Server role to provide IP addressing for the internal lab network.

<p align="center">
  <img src="https://github.com/user-attachments/assets/33e2d11e-d852-423a-902f-1d2ab28e029e"
       width="750"
       alt="Windows Server DHCP configuration">
</p>

<p align="center">
  <em>DHCP Server configuration.</em>
</p>

---

# 3. Active Directory Domain Services

Once the basic server and network configuration was complete, I used Server Manager to install the required server roles and features.

The primary role installed was:

**Active Directory Domain Services (AD DS)**

```text
DC01
│
└── corp.local
    │
    ├── Users
    ├── Groups
    ├── Organizational Units
    └── Computers
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/4623309c-807d-456d-90dd-d3199918a9a0"
       width="700"
       alt="Adding Active Directory Domain Services role">
</p>

<p align="center">
  <em>Adding server roles and features through Server Manager.</em>
</p>

### Domain Controller Promotion

After installing AD DS, I promoted DC01 to a domain controller and created the internal domain:

```text
corp.local
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/1d322358-3010-4aa4-ac6e-5b2e807d7b76"
       width="700"
       alt="Promoting Windows Server to domain controller">
</p>

<p align="center">
  <em>Promoting DC01 to a domain controller.</em>
</p>

---

# 4. Organizational Units, Users & Security Groups

After the domain controller was configured, I created the initial Active Directory structure.

### Tasks Completed

* Created an Organizational Unit (OU)
* Created a test user account
* Created a Helpdesk security group
* Added the test user to the Helpdesk group
* Organized users and groups within the IT OU

---

## Organizational Unit

<p align="center">
  <img src="https://github.com/user-attachments/assets/43c1c0e6-cc10-4559-9ea6-fc10a82c8951"
       width="650"
       alt="Creating an Active Directory Organizational Unit">
</p>

<p align="center">
  <em>Creating the IT Organizational Unit.</em>
</p>

---

## Test User

<p align="center">
  <img src="https://github.com/user-attachments/assets/d48de05d-b0b2-4175-bc26-4134249c4619"
       width="650"
       alt="Creating a test user in Active Directory">
</p>

<p align="center">
  <em>Creating a test user account in Active Directory.</em>
</p>

---

## Helpdesk Security Group

<p align="center">
  <img src="https://github.com/user-attachments/assets/48c7e60a-12f4-4eab-8500-11f9a4067abd"
       width="650"
       alt="Creating the Helpdesk security group">
</p>

<p align="center">
  <em>Creating the Helpdesk security group.</em>
</p>

---

## Adding User to Helpdesk Group

<p align="center">
  <img src="https://github.com/user-attachments/assets/8b186043-e3a8-42c2-8919-5c1681002a31"
       width="650"
       alt="Adding the test user to the Helpdesk security group">
</p>

<p align="center">
  <em>Adding the test user to the Helpdesk security group.</em>
</p>

### Resulting Active Directory Structure

```text
CORP.LOCAL
│
├── IT
│   ├── test.user
│   └── Helpdesk
│
└── Workstations
```

This structure provides a foundation for applying security policies and managing users based on organizational roles.

---

# 5. Group Policy Configuration

After creating the organizational structure, I configured a Group Policy Object (GPO) for the IT Organizational Unit.

The basic management flow is:

```text
Organizational Unit
        │
        ▼
       GPO
        │
        ▼
 Policy Settings
        │
   ┌────┴────┐
   ▼         ▼
 Users    Computers
```

<p align="center">
  <img src="https://github.com/user-attachments/assets/751cdc97-9252-4332-99c5-c69705f95441"
       width="650"
       alt="Creating a Group Policy Object">
</p>

<p align="center">
  <em>Creating and configuring a Group Policy Object.</em>
</p>

---

# 📊 Current Project Architecture

The current state of the lab can be represented as:

```text
                         DC01
                  Windows Server 2022
                         │
                  Active Directory
                         │
                     corp.local
                         │
             ┌───────────┼───────────┐
             │           │           │
             ▼           ▼           ▼
            IT      Workstations    Users
             │
       ┌─────┴─────┐
       │           │
       ▼           ▼
  test.user    Helpdesk
                   │
                   ▼
                  GPO
```

---

# Skills Demonstrated

* Windows Server 2022
* Active Directory Domain Services (AD DS)
* Domain Controller Configuration
* Organizational Units (OUs)
* User Account Management
* Security Group Management
* Group Policy Objects (GPO)
* TCP/IPv4 Configuration
* DHCP
* DNS / Domain Services
* Windows 11 Domain Client Configuration
* Oracle VirtualBox
* Virtual Networking
* Enterprise IT Administration
* Tier 1 / Tier 2 Help Desk Concepts

---

## 📌 Project Status

**Status:** 🟢 In Progress

This repository will be continuously updated as additional enterprise infrastructure, troubleshooting scenarios, and remote-access configurations are implemented.
