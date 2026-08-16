# **Active Directory Lab 03** 

# **Delegating Password Reset Permissions in Active Directory** 

# **Objective** 

The objective of this lab was to understand the concept of **delegation in Active Directory** by assigning limited administrative privileges to a security group. The lab demonstrated how to delegate password reset permissions to the **IT_Team** security group, verify the delegated permissions, test password reset functionality using the graphical interface, and validate the principle of **Least Privilege** by confirming that unauthorized administrative actions were restricted. 

# **Lab Environment** 

# **Component Details** 

Operating System Windows Server (Domain Controller) 

Client Machine Windows 11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used Active Directory Users and Computers (ADUC) 

# **Step 1: Delegating Password Reset Permissions** 

The **Active Directory Users and Computers (ADUC)** console was opened on the Domain Controller, and the **Delegate Control Wizard** was launched for the **_EMPLOYEES** Organizational Unit. The **IT_Team** security group was selected as the delegated group. 

A custom delegation task was configured for **User objects** , and the following permissions were assigned: 

- Reset Password 

- Read User Information 

- Write User Information 

These permissions allowed members of the **IT_Team** security group to perform password resets and update user information without granting them full administrative privileges. 

**Result** 



<!-- Start of picture text -->
ee<br>Bp fictive Disectoms leone ood Conuoubose<br>d Delegation of Control Wizard x<br>sal Ser @ | Select Users, Cormputers, or Groups x i?<br>Serve a ,<br>G Select this object type:<br>DS || |Users. Groups, of Built-in security principals Object Tynes...<br>IS “ From this location:<br>Enter the object names to select (examples):<br>i TEAM Check Names<br>Advanced... Cancel<br>< Back Next > Cancel Help<br><!-- End of picture text -->



<!-- Start of picture text -->
DC<br>boa | Delegation of Control Wizard x<br>Ser é Tasks to Delegate<br>vel ‘You can select common tasks or customize your own. |<br>s<br>CO Delegate the following common tasks:<br>(1 Create, delete, and manage user accounts a<br>nd C Reset user passwords and force password change at next logon<br>C Read all user information<br>CO Create, delete and manage groups<br>(1 Modify the membership of 4 group<br>CO Manage Group Policy links<br>CO Generate Resultant Set of Policy (Planning) v<br>< ><br>@ Create a custom task to delegate<br>< Back. Cancel Help<br><!-- End of picture text -->



<!-- Start of picture text -->
Delegation of Control Wizard ~<br>Active Directory Object Type f<br>Indicate the scope of the task you want to delegate. 1<br>Delegate control of:<br>(©) This tolder, existing objects in this folder, and creation of new objects in this folder<br>(@) Only the following objects in the folder:<br>L] Site Settings objects A<br>[] Sites Container objects<br>(J Subnet objects<br>[_] Subnets Container objects<br>(J Trusted Domain objects<br>User objects v<br>(_] Create selected objects in this folder<br>(_] Delete selected objects in this folder<br>< Back Cancel Help<br><!-- End of picture text -->



<!-- Start of picture text -->
| Delegation of Control Wizard am<br>Permissions i<br>Select the permissions you want to delegate. 7<br>Show these permissions:<br>General<br>(_] Property-specific<br>(_] Creationédeletion of specific child objects<br>Permissions:<br>-<br>CL] Send as<br>L] Receive as<br>Read and write general information<br>(_] Read and write account restrictions<br>(J Read and write logon information nv<br>< Back Cancel Help<br><!-- End of picture text -->



<!-- Start of picture text -->
ee<br>boa| @FileActiveAction Directory UsersWiew Help and Computers - Oo 4<br>| lesSer aml— o|\S a@S\b ampml on,® t| -EMPLOYEES PropertiesP ? * |.<br>eve3S | Active Directory Users and Com|| hare Type General Managed By Object3 SecurityF COM+ Attribute Editorq -<br>i Saved Queries [Bl HR Orga Group of user names:<br>¥ Gd tiydomain.carm in Orgat | S& CREATOR OWNER A<br>Lal ao3) ADMINS —_iS SALES Orgat | SB SELF<br>a EMPLOYEES 82, Authenticated Users<br>ig) GROUPS SR SYSTEM<br>(5) Builtin SR IT_TEAM (MY DOMAINSIT_TEAM]<br>| Computers SI. Domain Admins (M'Y’DOMAIN'\D omain Admins] e<br>au Domain Controllers Add. Remove<br>Lo) ForeignSecurityPrincipal:<br>i Keys Permissions for IT_TEAM Allow Dery<br>a* Last’ndFoundoun pune Create all child objects O— — “<br>Lo) Managed Service Accour . .<br>= Delete all child objects O<br>LJ) Program Data . .<br>= Generate resultant set of policy [logging] O O<br>Lo)= Systern1 Generate resultant set of policy. [planning]. Oo] O<br>a NTDSgers Quotas Special permissions ov<br>() TPM Devices For special permissions or advanced settings. click Advanced<br>Advanced.<br>Cancel Apply Help<br><><br>]| Services | | Services |<br><!-- End of picture text -->



<!-- Start of picture text -->
Server Manager » Dashboard ~@ 1 P— Manage Toots View Help<br>— BF Active Directory Users and Computers - a x<br>UES File Action View Help<br>U Local Ser eo|amlSire ¢O|\XOGSB/Em|a . %<br>lesimi©  All AD Serve DS active2 Sve Directory QueriesUsers and Com|| Name3 charlie brown TypeUsertear aeDescription<br>=MB pns | ¥ Ha mydornain.com=i _ADMINS aIrTcoe<br>Fileand{ — v &j EMPLOYEESHR da t 0.2 group...<br>sir Name Mappings...<br>a] SALES Disable Account<br>@] GROUPS Reset Password...<br>|) Builtin Move<br>9) Computers<br>3] Domain Controllers Open Home Page<br>5] ForeignSecurityPrincipal Send Mail Ride<br>|]J KeysLost&ndFound All Tasks ><br>5] Managed Service Accour Cut<br>5 Program Data Delete<br>Sl System an<br>| Users<br>|] NTDS Quotas Properties<br>3] TPM Devices<br>Help<br>«< ><br>Renames the current selection,<br>rvICes ervICes<br>Performance Performance<br>BPA results BPA results<br>a ©Sowt+ @ BB ss 2? © te cro20563:02 PM UW<br><!-- End of picture text -->



<!-- Start of picture text -->
te7%<br>Pinned All ><br>A<br>Mileiressenit ’ a<br>Edge Outlook Microsoft Store Settings Photos Calculator<br>=5s oy#®# > BF=<br>Clock Notepad Paint Snipping Tool File Explorer<br>» |<br>q Recommendeds jane smith Show hiddenMoreiconsay> )<br>LD EE EE eee _ eee<br>4]7~QuBe@CB—_ » am “aN BV) &®wea Fro20262:47 AM &id<br><!-- End of picture text -->

# **Step 4: Verifying Delegation Limitations** 

To verify that delegation followed the **Least Privilege** principle, an attempt was made to delete an existing user account while logged in as **john.doe** . The operation failed because the delegated permissions only allowed password resets and limited user management operations. 

This confirmed that administrative privileges were restricted according to the delegated permissions and that users could not perform unauthorized actions. 

# **Result** 

The delete operation was denied, confirming that only the delegated permissions were available to the **IT_Team** security group. 

# **Step 5: Testing Delegation Scope** 

To verify the scope of the delegated permissions, another user account located in the **Sales** Organizational Unit ( **bob.wilson** ) was selected. Using the delegated account, the password was successfully reset through the **Reset Password** option in Active Directory Users and Computers. 

This demonstrated that the delegation applied to the parent **_EMPLOYEES** Organizational Unit, allowing delegated permissions to be inherited by all child Organizational Units, including **IT** , **HR** , and **Sales** . 

# **Result** 

The password reset operation was successfully completed for a user located in a different departmental Organizational Unit, confirming that delegation was inherited across all child OUs. 

# **Conclusion** 

This lab demonstrated the implementation of **delegation in Active Directory** by assigning limited administrative privileges to the **IT_Team** security group. Password reset permissions were successfully delegated and verified using the Active Directory Users and Computers console. Members of the delegated group were able to reset passwords for users across the **_EMPLOYEES** Organizational Unit while remaining restricted from performing higher-privileged administrative actions such as deleting user accounts. The lab highlighted the practical application of the **Least Privilege** principle and demonstrated how delegation enables secure distribution of administrative responsibilities in enterprise Active Directory environments. 

