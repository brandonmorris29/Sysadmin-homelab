# Lab 1: Active Directory & Group Policy

## What I Built
A Windows Server 2022 domain environment with Active Directory,
organizational units, user accounts, security groups, and GPOs.



## Skills Demonstrated
- Active Directory Domain Services setup
- Organizational Unit (OU) design
- Group Policy Object (GPO) creation and linking
- User and group management


## Steps Taken
(A)Lab and Domain Controller Setup

1.Download and installed Virtualbox on my PC
2.Download Windows Server 2022 Evaluation ISO from the Microsoft Evaluation Center
3.Create 3 VM's with 2CPU's, 4GB RAM, 60GB disk
4.Install Windows Server 2022 Desktop experience and did the next 5 steps for my Windows Server2022
5.Open Server Manager > Add Roles and Features
6.Select Active Directory Domain Services and install
7.Promote Server to domain controller
8.Set DSRM password, click through defaults ,and restart server

(B) Create Company Structure

1. Open ADUC
2. Right-click my domain (corp.local) > New > Organizational Unit
3. Created Corp Oganizational unit with NY OU nested inside and Users Ou nested inside of that.
4. Created 4 OU's called Executives, Finance, HR, IT, and created 2 test users for each OU
5. Created A OU called Groups in the corp.local domain with a nested OU called Security Groups
6. Within the securoty groups folder I created 4 security groups called Executive-Users, Finance-Users, HR-Users, and IT-Admins
7. Added each user to their appropriate security group

(C) Create Group policy objects

1. Window search for gpmc.msc
2. Right-click on corp.local > Create GPO and name password policy.
3. Navigate to Computer Config > Windows Settings > Security Settings > Account Policies
4. From here we set a minimum password length of 12, complexity required, and lockout after 5 attempts
5. Another GPO is created and named Destop Restircitons
6. For this policy we navigate to User Config > Admin Templates > Control Panel > hide Control Panel for non-admins
7. On a VM with Windows 11 I join the device to corp.locals domain and run a gpupDATE /force to forcefully update the group policy
8. The Win 11 client gets restarted abd I confirm the policies being applied by running a gpresult /r in command prompt
9. When navigating to control panel there's an error message stating " This operarion has been cancelled due to restrictions in effect on this computer Please contact your administrator" (policy works)
10. I also check that the password policy is being applied by running ctrl+alt+del. I attempt to change the password with a 4 letter password and I'm greeted with an error telling me the password policy is working.
## Screenshots


## Lessons Learned
During this lab encountered and issue where the control panel policy was beeing applied to my administrator profile as well not allowing me to access this tool. 
I then realized the policy was linked at the root domain meaning everyone will have with policy enforced on their profile.
I deleted the GPO from root, then linked it to the Executive, Finance, and HR OU's.
I then logged out and back into my Windows server, ran a gpupdate /force, and confirmed that control panel was working.
