# Lab 1: Active Directory & Group Policy

## What I Built
A Windows Server 2022 domain environment with Active Directory,
organizational units, user accounts, security groups, and GPOs.



## Skills Demonstrated
- Active Directory Domain Services setup
- Organizational Unit (OU) design
- Group Policy Object (GPO) creation and linking
- User and group management

Steps Taken
(A) Lab and Domain Controller Setup
- Downloaded and installed VirtualBox on my PC.
- Downloaded the Windows Server 2022 Evaluation ISO from the Microsoft Evaluation Center.
- Created three VMs, each with 2 CPUs, 4 GB RAM, and a 60 GB disk.
- Installed Windows Server 2022 Desktop Experience on one VM and completed the next steps on that server.
- Opened Server Manager → Add Roles and Features.
- Selected and installed Active Directory Domain Services.
- Promoted the server to a domain controller.
- Set the DSRM password, accepted the defaults, and restarted the server.

(B) Create Company Structure
- Opened Active Directory Users and Computers (ADUC).
- Right‑clicked my domain (corp.local) → New → Organizational Unit.
- Created a Corp OU with a nested NY OU and a Users OU inside it.
- Created four OUs: Executives, Finance, HR, IT, and created two test users in each OU.
- Created a Groups OU in the corp.local domain with a nested Security Groups OU.
- Inside the Security Groups OU, created four security groups:
- Executive-Users
- Finance-Users
- HR-Users
- IT-Admins
- Added each test user to the appropriate security group.

(C) Create Group Policy Objects
- Searched for and opened gpmc.msc.
- Right‑clicked corp.local → Create a GPO, named it Password Policy.
- Navigated to Computer Configuration → Windows Settings → Security Settings → Account Policies.
- Configured:
- Minimum password length: 12 characters
- Password complexity: Enabled
- Account lockout after 5 attempts
- Created another GPO named Desktop Restrictions.
- Navigated to User Configuration → Administrative Templates → Control Panel and enabled “Prohibit access to Control Panel and PC settings.”
- Joined a Windows 11 VM to the corp.local domain and ran gpupdate /force to apply the policies.
- Restarted the Windows 11 client and confirmed the policies were applied using gpresult /r.
- Verified the Control Panel restriction — attempting to open it produced the message:
“This operation has been cancelled due to restrictions in effect on this computer. Please contact your administrator.”
- Verified the password policy by attempting to change the password to a 4‑character value and receiving an error confirming the policy was enforced.


Screenshots
(A) 1. Active Directory Server Manager

Lessons Learned

During this lab, I encountered an issue where the Desktop Restrictions GPO was applying to my Administrator account, preventing access to the Control Panel. I realized the GPO was linked at the domain root, meaning it applied to all users, including administrators.
To fix this:
- I removed the GPO link from the domain root.
- I linked it only to the Executives, Finance, and HR OUs.
- After logging out and back into the server and running gpupdate /force, I confirmed that the Control Panel was accessible again for the Administrator account.

