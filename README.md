
# Enterprise-Directory-Services
Deploying a virtualized Windows Server and Active Directory environment to manage user accounts, GPOs, and OU security permissions.

The first step I took was setting up the lab using Oracle VirtualBox: 


                    My PC                    
                VirtualBox
                     │
          ┌──────────┴──────────┐
          │                     │
   Windows Server 2022    Windows 11
      "DC01"                 "PC01"
          │                     │
          │                     │
          └──── LAB NETWORK ────┘
                  │
             192.168.50.0/24

             <img width="841" height="563" alt="Setting up the Window server" src="https://github.com/user-attachments/assets/3abf2994-b73c-477e-8001-71d970857a73" />

             <img width="933" height="635" alt="Installed Windows Server Successfully" src="https://github.com/user-attachments/assets/8fa91e04-bf66-47fe-8014-3f728c03be0c" />

             
The second step that I took was configuring the Network and IP addresses on the server: 

                 DC01
                  │
        ┌─────────┴─────────┐
        │                   │
    Adapter 1           Adapter 2
       NAT              IT-LAB
        │                   │
    Internet          Private Lab

    <img width="617" height="442" alt="Verifying the Ipv4 configuration using ipcon<img width="501" height="478" alt="Creating group " src="https://github.com/user-attachments/assets/18c495a1-c2f6-4026-9799-c18155edcb7e" />
fg " src="https://github.com/user-attachments/assets/2878656e-8402-4884-a836-7d82b9a70f35" />

    <img width="621" height="443" alt="Assigning TCP IP addresses to the Ethernet adapter 2" src="https://github.com/user-attachments/assets/752d170b-4e6e-4eba-92f6-cc1589a48a38" />

     <img width="838" height="598" alt="Enabling DHCP Server " src="https://github.com/user-attachments/assets/33e2d11e-d852-423a-902f-1d2ab28e029e" />

<img width="621" height="443" alt="Assigning TCP IP addresses to the Ethernet adapter 2" src="https://github.com/user-attachments/assets/752d170b-4e6e-4eba-92f6-cc1589a48a38" />

The next step I took was to go through Server Manager to add the roles and features, as well as Active Directory Domain Services: 

```text
DC01 (Domain Controller)
└── corp.local (Root Domain)
    ├── Users
    ├── Groups
    ├── OUs (Organizational Units)
    └── Computers
```
<img width="512" height="445" alt="Adding Roles and Features " src="https://github.com/user-attachments/assets/4623309c-807d-456d-90dd-d3199918a9a0" />

<img width="605" height="438" alt="Promoting the server to Domain controller" src="https://github.com/user-attachments/assets/1d322358-3010-4aa4-ac6e-5b2e807d7b76" />




---------------------------------------------------------------------------------

Now, after I promoted the server to be the domain controller and installed the Active Directory features: 
- I Created an Organizational Unit (OU).
- I also created a test user.
- Then I also created a help desk Group.


<img width="506" height="480" alt="Creating a Test User " src="https://github.com/user-attachments/assets/d48de05d-b0b2-4175-bc26-4134249c4619" />


<img width="504" height="484" alt="Creating An organizational Unit OU" src="https://github.com/user-attachments/assets/43c1c0e6-cc10-4559-9ea6-fc10a82c8951" />


<img width="501" height="478" alt="Creating group " src="https://github.com/user-attachments/assets/48c7e60a-12f4-4eab-8500-11f9a4067abd" />


<img width="504" height="482" alt="Adding the test user to the Helpdesk group" src="https://github.com/user-attachments/assets/8b186043-e3a8-42c2-8919-5c1681002a31" />



And that's how the diagram comes up after adding the test user to the Helpdesk group: 

```text      
CORP.LOCAL
     │
     ├─ IT
     │  ├─ test.user
     │  └─ Helpdesk
     │
     └─ Workstations

-------------------------------------------------------------------


After that, I configured a group policy (GPO) for the IT domain that I created earlier: 

OU
 ↓
GPO
 ↓
Policy settings
 ↓
Users / Computers

<img width="503" height="446" alt="Creating a group Policy object (GPO)" src="https://github.com/user-attachments/assets/751cdc97-9252-4332-99c5-c69705f95441" />


-----------------------------------------------------------------------

```text
The final Diagram of the project until now ( I will keep updating it): 
                 DC01
          Windows Server 2022
                 │
          Active Directory
                 │
             corp.local
                 │
        ┌────────┼─────────┐
        │        │         │
       IT   Workstations  Users
        │
    test.user
        │
     Helpdesk
        │
   GPO Policy


