**Active Directory Lab 01**

**Creating Organizational Units (OUs) and Users in Active Directory**

**Objective**

The objective of this lab was to understand the basic administration of Active Directory by creating Organizational Units (OUs) and manually adding user accounts within a Windows Server domain environment. The lab also demonstrated how to organize users into departmental OUs and configure account properties such as password settings. This exercise provided practical experience with the Active Directory Users and Computers (ADUC) management console, which is widely used in enterprise environments for identity and access management.

**Lab Environment**

| **Component** | **Details** |
|------------------|---------------------------------------------|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 10/11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Active Directory Users and Computers (ADUC) |

**Step 1: Starting the Virtual Machines**

The lab environment was initialized by starting both the Domain Controller and the Windows client virtual machines using VMware Workstation. After the operating systems completed the boot process, both virtual machines were verified to be connected to the same virtual network. This ensured proper communication between the client machine and the Domain Controller before performing any Active Directory administrative tasks.

**Result**

Both virtual machines started successfully, and the Domain Controller was accessible for further configuration. 

**Step 2: Opening Active Directory Users and Computers**

After logging into the Windows Server Domain Controller, the **Active Directory Users and Computers (ADUC)** management console was launched through **Server Manager → Tools → Active Directory Users and Computers**. The console displayed the existing domain structure of **mydomain.com**, allowing administrative tasks such as creating Organizational Units and user accounts to be performed.

**Result**

The ADUC console opened successfully and displayed the complete Active Directory domain hierarchy.

**Step 3: Creating Organizational Units (OUs)**

To organize the Active Directory environment, several Organizational Units (OUs) were created under the domain **mydomain.com**. Separate OUs were created for administrators, employees, and groups. Within the **\_EMPLOYEES** Organizational Unit, additional child OUs were created to represent different organizational departments including **IT**, **HR**, and **Sales**.

The resulting Active Directory structure was organized as follows:

mydomain.com

│

├── \_ADMINS

│

├── \_EMPLOYEES

│ ├── IT

│ ├── HR

│ └── Sales

│

└── \_GROUPS

**Organizational Unit Structure**

| **Parent OU** | **Child OU** |
|---------------|--------------|
| mydomain.com | \_ADMINS |
| mydomain.com | \_EMPLOYEES |
| \_EMPLOYEES | IT |
| \_EMPLOYEES | HR |
| \_EMPLOYEES | Sales |
| mydomain.com | \_GROUPS |

**Result**

The Organizational Unit hierarchy was successfully created according to the planned Active Directory structure, enabling proper administrative organization of departmental resources.

**Step 4: Creating User Accounts**

User accounts were manually created within their respective departmental Organizational Units using the **New User** wizard in Active Directory Users and Computers. During account creation, each user was assigned the predefined password **P@ssw0rd123**, and the **Password never expires** option was enabled to prevent password expiration during the lab.

The following user accounts were created:

| **Username** | **Department** |
|---------------|----------------|
| john.doe | IT |
| jane.smith | HR |
| bob.wilson | Sales |
| alice.johnson | IT |
| charlie.brown | HR |

**Password Configuration**

- Password: **P@ssw0rd123**

- **Password never expires:** Enabled 

**Result**

All user accounts were successfully created and placed in their corresponding Organizational Units based on departmental requirements.

**Step 5: Verifying User Properties**

After creating all user accounts, each account's properties were reviewed through the **Account** tab in Active Directory Users and Computers. The configuration was verified to ensure that the **Password never expires** option was enabled for every user account. This verification confirmed that all user accounts were configured consistently according to the lab requirements.

**Result**

All user accounts were successfully verified, and the required password policy was correctly applied.

**Conclusion**

This lab provided practical experience with the fundamental administrative tasks performed in Active Directory. Organizational Units were successfully created to establish a structured domain hierarchy, and user accounts were organized according to their respective departments. Password policies were configured and verified for all users, demonstrating the process of managing identities within a Windows Server domain. The completed lab strengthened understanding of Active Directory administration and the importance of structured user management in enterprise environments.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_01_1.png)

![Screenshot 2](IAM_Lab_01_2.png)

![Screenshot 3](IAM_Lab_01_3.png)

![Screenshot 4](IAM_Lab_01_4.png)

![Screenshot 5](IAM_Lab_01_5.png)

![Screenshot 6](IAM_Lab_01_6.png)

