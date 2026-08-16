**Active Directory Lab 03**

**Delegating Password Reset Permissions in Active Directory**

**Objective**

The objective of this lab was to understand the concept of **delegation in Active Directory** by assigning limited administrative privileges to a security group. The lab demonstrated how to delegate password reset permissions to the **IT_Team** security group, verify the delegated permissions, test password reset functionality using the graphical interface, and validate the principle of **Least Privilege** by confirming that unauthorized administrative actions were restricted.

**Lab Environment**

| **Component** | **Details** |
|------------------|---------------------------------------------|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Active Directory Users and Computers (ADUC) |

**Step 1: Delegating Password Reset Permissions**

The **Active Directory Users and Computers (ADUC)** console was opened on the Domain Controller, and the **Delegate Control Wizard** was launched for the **\_EMPLOYEES** Organizational Unit. The **IT_Team** security group was selected as the delegated group.

A custom delegation task was configured for **User objects**, and the following permissions were assigned:

- Reset Password

- Read User Information

- Write User Information

These permissions allowed members of the **IT_Team** security group to perform password resets and update user information without granting them full administrative privileges.

**Result**

Password reset permissions were successfully delegated to the **IT_Team** security group for all user accounts within the **\_EMPLOYEES** Organizational Unit.

**Step 2: Verifying Delegation Settings**

After completing the delegation process, the security settings of the **\_EMPLOYEES** Organizational Unit were reviewed through the **Security** tab in the OU properties. The delegated **IT_Team** group appeared in the access control list with the configured permissions.

This verification confirmed that the delegation had been applied successfully and that the required permissions were available to members of the security group.

**Result**

The delegated permissions were successfully verified in the Organizational Unit security settings.

**Step 3: Testing Password Reset Delegation**

To validate the delegated permissions, the Windows 11 client machine was used to log in with the **john.doe** domain account, which is a member of the **IT_Team** security group.

Using the **Active Directory Users and Computers (ADUC)** graphical interface, the password of **jane.smith** was reset to **NewPass123!** through the **Reset Password** option. After the password was updated, the user account **jane.smith** was used to log in to the client machine with the new password.

The successful login confirmed that the delegated password reset operation had been completed successfully.

**Result**

The delegated user successfully reset the password of another domain user through the ADUC graphical interface, and the updated credentials were verified by logging in with the new password.

**Screenshot 3:** *Password Reset Using ADUC*

**Screenshot 4:** *Successful Login Using the New Password*

**Step 4: Verifying Delegation Limitations**

To verify that delegation followed the **Least Privilege** principle, an attempt was made to delete an existing user account while logged in as **john.doe**. The operation failed because the delegated permissions only allowed password resets and limited user management operations.

This confirmed that administrative privileges were restricted according to the delegated permissions and that users could not perform unauthorized actions.

**Result**

The delete operation was denied, confirming that only the delegated permissions were available to the **IT_Team** security group.

**Step 5: Testing Delegation Scope**

To verify the scope of the delegated permissions, another user account located in the **Sales** Organizational Unit (**bob.wilson**) was selected. Using the delegated account, the password was successfully reset through the **Reset Password** option in Active Directory Users and Computers.

This demonstrated that the delegation applied to the parent **\_EMPLOYEES** Organizational Unit, allowing delegated permissions to be inherited by all child Organizational Units, including **IT**, **HR**, and **Sales**.

**Result**

The password reset operation was successfully completed for a user located in a different departmental Organizational Unit, confirming that delegation was inherited across all child OUs.

**Conclusion**

This lab demonstrated the implementation of **delegation in Active Directory** by assigning limited administrative privileges to the **IT_Team** security group. Password reset permissions were successfully delegated and verified using the Active Directory Users and Computers console. Members of the delegated group were able to reset passwords for users across the **\_EMPLOYEES** Organizational Unit while remaining restricted from performing higher-privileged administrative actions such as deleting user accounts. The lab highlighted the practical application of the **Least Privilege** principle and demonstrated how delegation enables secure distribution of administrative responsibilities in enterprise Active Directory environments.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_03_1.png)

![Screenshot 2](IAM_Lab_03_2.png)

![Screenshot 3](IAM_Lab_03_3.png)

![Screenshot 4](IAM_Lab_03_4.png)

![Screenshot 5](IAM_Lab_03_5.png)

![Screenshot 6](IAM_Lab_03_6.png)

![Screenshot 7](IAM_Lab_03_7.png)

