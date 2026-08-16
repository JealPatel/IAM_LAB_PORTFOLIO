# **Active Directory Lab 06** 

# **Account Lockout Policy and User Account Recovery** 

# **Objective** 

The objective of this lab was to understand how Active Directory handles account lockout events after multiple failed login attempts. The lab demonstrated how to trigger an account lockout, identify the corresponding security event in **Event Viewer** , unlock the affected account using **Active Directory Users and Computers (ADUC)** , and verify successful user authentication after the account was restored. 

# **Lab Environment** 

# **Component Details** 

Operating System Windows Server (Domain Controller) 

Client Machine Windows 11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used Active Directory Users and Computers (ADUC), Event Viewer 

# **Step 1: Triggering an Account Lockout** 

The Windows 11 client machine was used to simulate multiple failed authentication attempts. The **john.doe** domain account was selected, and incorrect passwords were entered repeatedly until the configured account lockout threshold was reached. 

After multiple unsuccessful login attempts, the system displayed a message indicating that the account had been locked due to security policy restrictions. 

This exercise demonstrated how Active Directory protects user accounts from password guessing and brute-force attacks by temporarily locking compromised accounts. 

# **Result** 

The **john.doe** user account was successfully locked after exceeding the allowed number of failed login attempts. 

**Screenshot 1:** _Account Lockout Message on Windows 11_ 



<!-- Start of picture text -->
3 )<br>john doe<br>The referenced account is currently locked out and may not<br>be logged on to.<br><!-- End of picture text -->



<!-- Start of picture text -->
a<br>File Action View Help<br>¢9|4 | mm<br>(2) Event Viewer (Local) Security |Nurnberof events: 211 Actions<br>© [ik} WindowsCustom ViewsLogs ¥ Filtered: Log: Security; Source: ; Event ID: 4740, Number of events: 1 Security «<br>(2 Application Keywor.. Date<br>—setup @Audi... 8/1/2026and Time 6:40:55 PM SourceMicros... EventID4740 TaskUser C.. A... &_Y OpenCreateSavedCustomLog...View...<br>& System Import Custom View...<br>& Forwarded Events Clear Log...<br>: Applicationssubscriptions and Servic {@ Event Properties - Event 4740, Microsoft Windows security auditing, x 7 Filter Current Log se<br>Clear Filter<br>General Details [) Properties<br>Is [A user account was locked out, A 88 Find...Fin<br>fed Save Filtered Log File A...<br>Subject: security ID: ose Attach a Task To this: Li.<br>AccountAccount Name: Dco1$ TH Save Filter to Custom ...<br>Logon Domain: MYDOMAIN<br>ID: Ox3E7 Pe rs View la<br>[@ Refresh<br>LogSource:a Name: MicrosoftSecuriny Windows security Logged: 8/1/2026 6:40:55 PM ry Hep ><br>Event ID: 4740 Task Category: User Account Management Event 4740, Microsoft Wind...<br>Level: Information Keywords: Audit Success =| Event Properties<br>User: N/A Computer: DCO1.mydomain.com G) AttachTask To This Ev...<br>pacer itis Id) Save Selected Events...<br>More Information: EventLog Online Help i) Copy »<br>[Gl Refresh<br>Copy Close Help »<br>< ><br>=z ofre @ Bw G © Fal fs eyvame642 PM<br><!-- End of picture text -->



<!-- Start of picture text -->
Server Manager > Dashboard ~@ | PF Manage Tools View Help<br>BF Activ ory r t<br>Bm Dashboa File Action View Help<br>EB Local Ser 9/415 & og x fe) } oo 7 mS<br>Baaa Allshes DF Active Directory Users and Com|) Name john doe Properties ? x<br>tg!& ADDNSDS v Gi Savedmydomain.comQueries @% johalic| PublishedSecurityCertificatesEnvironmentMemberOf PasswordSessions Replication RemoteDialincontrolObject<br>i Fil d4 =| ADMINS Remote Desktop Services Profile COM+ Attribute Editor<br>UW Wesel v 1B) EMPLOYEES General Address 9 Account Profile © Telephones Organization<br>a) HR<br>aj IT User logon name:<br>| GROUPS User logon name (pre-Windows 2000):<br>| Builtin -<br>“| Computers<br>3) Domain Controllers Logon Hours... Log On To... Hide<br>_ ForeignSecurityPrincipal:<br>il4) KeysLostAndFound oO UnlockDirectory account.Domain ThisController. account is currently locked out on this Active<br>5| ManagedPrograrn DataService Accour Account options:.<br>| Systern (User must change password at next logon a<br>a) Users (User cannot change password<br>“| NTDS Quotas Password never expires<br>| TPM Devices (Store password using reversible encryption v<br>Account expires<br>< > @Never<br>: — OBEnd of Monday , August 31, 2026<br>Perfor<br>BPA resi<br>Cancel Kee Help<br>= 20O oy+ @B z = Fl te ory06645 PM<br><!-- End of picture text -->

# **Step 5: Verifying User Authentication** 

After unlocking the account, the Windows 11 client machine was used to log in again using the correct credentials for **john.doe** . 

The authentication completed successfully, confirming that the account had been restored and that the lockout condition had been removed. 

# **Result** 

The user successfully authenticated with the correct password after the account was unlocked. 

# **Conclusion** 

This lab demonstrated the implementation and management of the **Active Directory Account Lockout Policy** . Multiple failed authentication attempts resulted in the successful lockout of a user account, illustrating how Active Directory protects against unauthorized access and brute-force attacks. The associated security event was identified using **Event Viewer (Event ID 4740)** , allowing the source of the lockout to be investigated. The account was then successfully unlocked using **Active Directory Users and Computers** , and normal user authentication was restored. This exercise provided practical experience in monitoring security events, responding to account lockouts, and performing common administrative recovery tasks within an enterprise Active Directory environment. 

