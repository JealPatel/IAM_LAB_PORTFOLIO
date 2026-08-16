**Active Directory Lab 06**

**Account Lockout Policy and User Account Recovery**

**Objective**

The objective of this lab was to understand how Active Directory handles account lockout events after multiple failed login attempts. The lab demonstrated how to trigger an account lockout, identify the corresponding security event in **Event Viewer**, unlock the affected account using **Active Directory Users and Computers (ADUC)**, and verify successful user authentication after the account was restored.

**Lab Environment**

| **Component** | **Details** |
|----|----|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Active Directory Users and Computers (ADUC), Event Viewer |

**Step 1: Triggering an Account Lockout**

The Windows 11 client machine was used to simulate multiple failed authentication attempts. The **john.doe** domain account was selected, and incorrect passwords were entered repeatedly until the configured account lockout threshold was reached.

After multiple unsuccessful login attempts, the system displayed a message indicating that the account had been locked due to security policy restrictions.

This exercise demonstrated how Active Directory protects user accounts from password guessing and brute-force attacks by temporarily locking compromised accounts.

**Result**

The **john.doe** user account was successfully locked after exceeding the allowed number of failed login attempts.

**Screenshot 1:** *Account Lockout Message on Windows 11*

**Step 2: Investigating the Lockout Event**

After the account lockout occurred, **Event Viewer** was opened on the Domain Controller to investigate the security event. The **Security** log was filtered using **Event ID 4740**, which records account lockout events in Active Directory.

The event log provided detailed information, including:

- Locked user account

- Caller computer name

- Time of the lockout

- Event ID (4740)

These details confirmed both the affected user account and the source system responsible for the failed authentication attempts.

**Result**

The account lockout event was successfully identified and verified through **Event ID 4740** in the Security log.

**Screenshot 2:** *Event Viewer Showing Event ID 4740*

**Step 3: Documenting the Lockout Event**

The Event Viewer details were reviewed and documented by capturing a screenshot showing the lockout event information. The screenshot included the locked account name, caller computer, and event details for future reference and reporting.

**Result**

The account lockout event was successfully documented.

**Step 4: Unlocking the User Account**

The locked user account was recovered using **Active Directory Users and Computers (ADUC)**. The properties of the **john.doe** account were opened, and the **Account** tab was accessed. The **Account is locked out** option was cleared, restoring access to the user account.

This process demonstrated how domain administrators can quickly recover locked user accounts without resetting passwords.

**Result**

The **john.doe** account was successfully unlocked through Active Directory Users and Computers.

**Screenshot 4:** *Unlocking the User Account in ADUC*

**Step 5: Verifying User Authentication**

After unlocking the account, the Windows 11 client machine was used to log in again using the correct credentials for **john.doe**.

The authentication completed successfully, confirming that the account had been restored and that the lockout condition had been removed.

**Result**

The user successfully authenticated with the correct password after the account was unlocked.

**Conclusion**

This lab demonstrated the implementation and management of the **Active Directory Account Lockout Policy**. Multiple failed authentication attempts resulted in the successful lockout of a user account, illustrating how Active Directory protects against unauthorized access and brute-force attacks. The associated security event was identified using **Event Viewer (Event ID 4740)**, allowing the source of the lockout to be investigated. The account was then successfully unlocked using **Active Directory Users and Computers**, and normal user authentication was restored. This exercise provided practical experience in monitoring security events, responding to account lockouts, and performing common administrative recovery tasks within an enterprise Active Directory environment.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_06_1.png)

![Screenshot 2](IAM_Lab_06_2.png)

![Screenshot 3](IAM_Lab_06_3.png)

