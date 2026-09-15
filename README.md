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

The second step that I took was configuring the Network and IP addresses on the server: 

                 DC01
                  │
        ┌─────────┴─────────┐
        │                   │
    Adapter 1           Adapter 2
       NAT              IT-LAB
        │                   │
    Internet          Private Lab


The next step I took was to go through Server Manager to add the roles and features, as well as Active Directory Domain Services: 

DC01
  │
  └── corp.local
       │
       ├── Users
       ├── Groups
       ├── OUs
       └── Computers

Now, after I promoted the server to be the domain controller and installed the Active Directory features: 
- I Created an Organizational Unit (OU).
- I also created a test user.
- Then I also created a help desk Group.


And that's how the diagram comes up after adding the test user to the Helpdesk group: 

                 CORP.LOCAL
                     │
            ┌────────┴────────┐
            │                 │
           IT            Workstations
            │
       ┌────┴─────┐
       │          │
   test.user   Helpdesk

After that, I configured a group policy (GPO) for the IT domain that I created earlier: 

OU
 ↓
GPO
 ↓
Policy settings
 ↓
Users / Computers


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


