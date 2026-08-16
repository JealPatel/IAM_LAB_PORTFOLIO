**Active Directory Lab 02**

**Implementing Role-Based Access Control (RBAC) Using Security Groups**

**Objective**

The objective of this lab was to implement **Role-Based Access Control (RBAC)** in an Active Directory environment by creating security groups, assigning users to their respective groups based on departmental roles, and verifying domain authentication through client login. This lab demonstrated how Active Directory security groups simplify user management and provide centralized access control in enterprise environments.

**Lab Environment**

| **Component** | **Details** |
|------------------|---------------------------------------------|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Active Directory Users and Computers (ADUC) |

**Step 1: Creating Security Groups**

The lab began by opening the **Active Directory Users and Computers (ADUC)** console on the Domain Controller. Inside the **\_GROUPS** Organizational Unit, three security groups were created to represent different organizational departments. Each group was configured with a **Global** group scope and **Security** group type to support role-based access management within the domain.

The following security groups were created:

- **IT_Team**

- **HR_Team**

- **Sales_Team**

These groups were designed to organize users according to their departmental responsibilities and provide a scalable method for assigning permissions in future administrative tasks.

**Result**

All three security groups were successfully created within the **\_GROUPS** Organizational Unit.

**Step 2: Adding Users to Security Groups**

After creating the security groups, existing user accounts were assigned to their corresponding departmental groups. User membership was configured through the **Member Of** tab in each user's properties and verified using the **Members** tab of each security group.

The following user-to-group assignments were configured:

| **Username** | **Security Group** | **Department** |
|---------------|--------------------|----------------|
| john.doe | IT_Team | IT |
| alice.johnson | IT_Team | IT |
| jane.smith | HR_Team | HR |
| charlie.brown | HR_Team | HR |
| bob.wilson | Sales_Team | Sales |

By assigning users to security groups rather than managing permissions individually, the Active Directory environment became easier to administer and more consistent with enterprise security practices.

**Result**

All users were successfully assigned to their respective security groups according to their departments.

**Step 3: Verifying Group Membership**

The membership of each security group was verified by reviewing the **Members** tab within the group properties. This verification ensured that every user had been added to the correct department-based security group.

The group memberships were confirmed as follows:

| **Security Group** | **Members** |
|--------------------|---------------------------|
| IT_Team | john.doe, alice.johnson |
| HR_Team | jane.smith, charlie.brown |
| Sales_Team | bob.wilson |

The verification process confirmed that the Role-Based Access Control configuration had been implemented correctly.

**Result**

All security groups contained the expected members, confirming successful user assignment.

**Step 4: Testing Domain Authentication**

To validate the Active Directory configuration, domain authentication was tested from the Windows 11 client machine. The client was signed out from the administrator account and a domain user account was used to log in.

The login was successfully performed using the following credentials:

| **Username** | **Password** |
|-------------------|--------------|
| mydomain\john.doe | P@ssw0rd123 |

After confirming successful authentication, additional verification was performed by logging in with another domain user account (**mydomain\jane.smith**) using the same password.

The successful authentication confirmed that:

- The user accounts existed in Active Directory.

- The configured passwords were valid.

- Communication between the client machine and the Domain Controller was functioning correctly.

- Domain authentication services were operating as expected.

**Result**

The Windows 11 client successfully authenticated multiple domain users, confirming proper integration between the client and the Active Directory domain.

**Conclusion**

This lab demonstrated the implementation of **Role-Based Access Control (RBAC)** using Active Directory security groups. Department-based security groups were successfully created, and users were assigned according to their organizational roles. Group memberships were verified to ensure accurate user assignments, and domain authentication was successfully tested using the Windows 11 client machine. The lab provided practical experience in centralized identity and access management, highlighting how security groups simplify permission management and improve administrative efficiency in enterprise Active Directory environments.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_02_1.png)

![Screenshot 2](IAM_Lab_02_2.png)

![Screenshot 3](IAM_Lab_02_3.png)

