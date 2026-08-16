**Active Directory Lab 04**

**Configuring Shared Folders and Access Permissions in Active Directory**

**Objective**

The objective of this lab was to configure secure shared folders in a Windows Server environment using Active Directory security groups. The lab demonstrated how to create shared folders, configure both Share and NTFS permissions, and verify that users could access only the resources assigned to their departmental roles. This exercise provided practical experience in implementing secure file sharing and access control based on the principle of **Role-Based Access Control (RBAC)**.

**Lab Environment**

| **Component** | **Details** |
|----|----|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Active Directory Users and Computers (ADUC), File Explorer |

**Step 1: Creating Departmental Shared Folders**

A new directory named **Shares** was created on the Domain Controller under the \**C:\** drive. Inside this directory, three departmental folders were created to represent the IT, HR, and Sales departments.

The resulting folder structure was as follows:

C:\Shares\\

├── IT\\

├── HR\\

└── Sales\\

These folders were prepared to serve as centralized shared resources for their respective departments.

**Result**

The departmental folder structure was successfully created on the Domain Controller.

**Screenshot 1:** *Departmental Folder Structure*

**Step 2: Configuring Shared Folder Permissions**

Each departmental folder was configured as a shared folder using the **Advanced Sharing** option in Windows. The default **Everyone** permission was removed, and access was granted only to the corresponding Active Directory security group.

The configured share permissions were as follows:

| **Shared Folder** | **Security Group** | **Share Permission** |
|-------------------|--------------------|----------------------|
| IT | IT_Team | Full Control |
| HR | HR_Team | Full Control |
| Sales | Sales_Team | Full Control |

Although **Full Control** was assigned at the share level, detailed access control was managed through NTFS permissions.

**Result**

All departmental folders were successfully shared and configured with department-specific share permissions.

**Screenshot 2:** *Shared Folder Configuration*

**Step 3: Configuring NTFS Permissions**

To provide more granular access control, NTFS permissions were configured on each departmental folder. The corresponding security group was granted permissions to read, view folder contents, and create new files while preventing unrestricted administrative control.

The following permissions were assigned:

- Read & Execute

- List Folder Contents

- Read

- Write

The **Users** group was removed from each folder to prevent unauthorized access by other domain users.

**Result**

NTFS permissions were successfully configured, ensuring that only authorized departmental users could access and modify their respective folders.

**Screenshot 3:** *NTFS Permission Configuration*

**Step 4: Verifying Access as an IT User**

The Windows 11 client machine was used to log in with the **john.doe** account, a member of the **IT_Team** security group.

The following access tests were performed:

| **Shared Folder** | **Result** |
|--------------------|----------------|
| \\172.16.0.1\IT | Access Granted |
| \\172.16.0.1\HR | Access Denied |
| \\172.16.0.1\Sales | Access Denied |

A text file was successfully created inside the **IT** shared folder, confirming that the assigned write permissions were functioning correctly. 

**Result**

The IT department user successfully accessed and modified the IT shared folder while being denied access to other departmental folders.

**Screenshot 4:** *IT User Access Verification*

**Step 5: Verifying Access as an HR User**

The client machine was then logged in using the **jane.smith** account, which belongs to the **HR_Team** security group.

The following access tests were completed:

| **Shared Folder** | **Result** |
|--------------------|----------------|
| \\172.16.0.1\HR | Access Granted |
| \\172.16.0.1\IT | Access Denied |
| \\172.16.0.1\Sales | Access Denied |

The successful access to the HR shared folder confirmed that permissions were correctly assigned based on departmental membership.

**Result**

The HR user was able to access only the HR shared folder while access to other departments remained restricted.

**Step 6: Verifying Access as a Sales User**

The client machine was logged in using the **bob.wilson** account, a member of the **Sales_Team** security group.

The following access results were observed:

| **Shared Folder** | **Result** |
|--------------------|----------------|
| \\172.16.0.1\Sales | Access Granted |
| \\172.16.0.1\IT | Access Denied |
| \\172.16.0.1\HR | Access Denied |

The test confirmed that the Sales department user could access only the Sales shared folder.

**Result**

Department-specific access control was successfully enforced for the Sales department.

**Step 7: Verifying Access as the Domain Administrator**

Finally, the Windows 11 client was logged in using the **mydomain\Administrator** account. Access tests were performed on all departmental shared folders.

The following results were observed:

| **Shared Folder** | **Result** |
|--------------------|----------------|
| \\172.16.0.1\IT | Access Granted |
| \\172.16.0.1\HR | Access Granted |
| \\172.16.0.1\Sales | Access Granted |

The administrator account had unrestricted access to all shared resources because it is a member of the **Domain Admins** group, which possesses full administrative privileges across the domain.

**Result**

The Domain Administrator successfully accessed all shared folders, confirming that administrative privileges override departmental restrictions.

**Conclusion**

This lab demonstrated the implementation of secure file sharing in a Windows Server environment using Active Directory security groups. Department-specific shared folders were successfully created, and both Share and NTFS permissions were configured to enforce **Role-Based Access Control (RBAC)**. Access testing confirmed that users could access only the folders assigned to their respective departments, while unauthorized access attempts were denied. The Domain Administrator retained unrestricted access to all shared resources, illustrating the hierarchy of administrative privileges within Active Directory. This exercise reinforced the importance of combining Share and NTFS permissions to implement secure and centralized file access management in enterprise environments.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_04_1.png)

![Screenshot 2](IAM_Lab_04_2.png)

![Screenshot 3](IAM_Lab_04_3.png)

![Screenshot 4](IAM_Lab_04_4.png)

![Screenshot 5](IAM_Lab_04_5.png)

