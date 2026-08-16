# **Active Directory Lab 04** 

# **Configuring Shared Folders and Access Permissions in Active Directory** 

# **Objective** 

The objective of this lab was to configure secure shared folders in a Windows Server environment using Active Directory security groups. The lab demonstrated how to create shared folders, configure both Share and NTFS permissions, and verify that users could access only the resources assigned to their departmental roles. This exercise provided practical experience in implementing secure file sharing and access control based on the principle of **Role-Based Access Control (RBAC)** . 

# **Lab Environment** 

# **Component Details** 

Operating System Windows Server (Domain Controller) Client Machine Windows 11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used Active Directory Users and Computers (ADUC), File Explorer 

# **Step 1: Creating Departmental Shared Folders** 

A new directory named **Shares** was created on the Domain Controller under the * _C:*_ drive. Inside this directory, three departmental folders were created to represent the IT, HR, and Sales departments. 

The resulting folder structure was as follows: 

C:\Shares\ 

├── IT\ ├── HR\ └── Sales\ 

These folders were prepared to serve as centralized shared resources for their respective departments. 

— ~ » ThisPC » Local Disk (0) » Shared Folder » wl @ Search Shared Fe Marne Date riodified Type er Quick access Pal+ **D** esktal”)ownloads SALESHRIT FAIOf2026FAIOf20267/30/2026 OF 5075:07 Ph **P** hM FileFileFile folder **folder** =| Docurnents 



<!-- Start of picture text -->
File Home Share View e<br>J ZI om Cutout dMovetoy % Delete ~ th v| Open ot > 4 cenaSelect all<br>Pin“aesto Quick CopyCe Paste a Copyaste pathshortcut Copycopyto~ to | mGoa (aleeNew =). PropertiesPS Edit SelectInvert selectionnone<br>Clipboard Organize New Open Select<br>€ 4 [BD > Thispc > pee = Search Shared Folder 5)<br>wh Quick access Nae ao| © Permissions for IT x Size<br>Gl% DesktopDownloadsDom HIiTst | | Share PemissionsGroup or user names: HerlzHer<br>[| Documents SR IT_TEAM (MYDOMAIN\IT_TEAM)<br>(=| Pictures<br>[This Pc<br>Gi CD Drive (D1) SSS_X6E<br>i Network Add. Remove<br>Petmissions for IT_TEAM Allow Deny<br>Full Control Mw Oo<br>Change Oo<br>Read Oo<br>3items 1 item selected =I-<br>(ee Apply WindowsWindowsServerLicense2019 Standardvalid forEvalu175<br>Build 1763.rs5_release,180914<br>hi € | a © Fl te Fo20065:15 PM 4<br><!-- End of picture text -->



<!-- Start of picture text -->
| Disk @@\—— oe ts = 2 seed Fol<br>Ge Permissions far IT ~*~<br>OG Security<br>Gr Object name: = C:\Shared Folder'|T<br>Group or user names:<br>5% CREATOR OWNER<br>SR SYSTEM<br>S® Administrators (My DOMAIN Administrators]<br>Tq SR IT_TEAM (MYDOMAINSIT_TESM]<br>Pe S® Users (MYDOMAINS Users]<br>0<br>Add... Remove<br>Permissions for IT_TEAM Allow Deny<br>Full comtral oO Ooo oa<br>Modity O O<br>Read & execute oO<br>Fo List folder contents oO<br>cl Read O y<br><!-- End of picture text -->



<!-- Start of picture text -->
gj = IIT = Qo x<br>| Fite | Home Share View e<br>| 5 & Cut Bi Move to ~ | 9€ Delete © Sar y. JOpen~ -})Selectall<br>.’inBkto Quicl m SDEY Paste— WWi] CopyPaste shortcut path == Gastar - =fELE Pel 5 al bd Properscsage Edit FE SelectInvert selection none<br>Clipboard Organize New Open Select<br>€ v > ThisPC » Local Disk (C:) >» Shared Folder > IT vd Search IT Pp<br>Name 3 Date modified Type Size<br>wr Quick access<br>Bl Deskesktop =| testo 7/30/2026 5:47 PM Text Document 1KB<br>4b Downloads<br>|=) Documents<br>©) Pictures<br>[5 This PC<br>of CD Drive (D:) SSS_X6<br>oo Network<br>litem  litemselected 71 bytes State:@& Shared He<br>Windows Server 2019 Stan<br>Windows License va<br>@ 172.16.0.1 x a5 a i) x<br>< 4 G @ »> Network > 1721601 > Search 172.16.0. Q<br>WN Sort » S— View ~ eee C3) Details<br>aa Downloads hr it;<br>= Documents — —<br>PR Pictures netlogon sales<br>® Music 2 re<br>iare Videos sysvol¥<br>——er<br>WB This PC<br>mt CD Drive (D:) CC<br>m= CD Drive (E:) 20.<br>> Si Network<br><!-- End of picture text -->

# **Step 5: Verifying Access as an HR User** 

The client machine was then logged in using the **jane.smith** account, which belongs to the **HR_Team** security group. 

The following access tests were completed: 

# **Shared Folder Result** 

\\172.16.0.1\HR Access Granted 

\\172.16.0.1\IT Access Denied 

\\172.16.0.1\Sales Access Denied 

The successful access to the HR shared folder confirmed that permissions were correctly assigned based on departmental membership. 

# **Result** 

The HR user was able to access only the HR shared folder while access to other departments remained restricted. 

# **Step 6: Verifying Access as a Sales User** 

The client machine was logged in using the **bob.wilson** account, a member of the **Sales_Team** security group. 

The following access results were observed: 

# **Shared Folder Result** 

\\172.16.0.1\Sales Access Granted 

\\172.16.0.1\IT Access Denied 

\\172.16.0.1\HR Access Denied 

The test confirmed that the Sales department user could access only the Sales shared folder. 

# **Result** 

Department-specific access control was successfully enforced for the Sales department. 

**Step 7: Verifying Access as the Domain Administrator** 

Finally, the Windows 11 client was logged in using the **mydomain\Administrator** account. Access tests were performed on all departmental shared folders. 

The following results were observed: 

# **Shared Folder Result** 

\\172.16.0.1\IT Access Granted \\172.16.0.1\HR Access Granted \\172.16.0.1\Sales Access Granted 

The administrator account had unrestricted access to all shared resources because it is a member of the **Domain Admins** group, which possesses full administrative privileges across the domain. 

# **Result** 

The Domain Administrator successfully accessed all shared folders, confirming that administrative privileges override departmental restrictions. 

# **Conclusion** 

This lab demonstrated the implementation of secure file sharing in a Windows Server environment using Active Directory security groups. Department-specific shared folders were successfully created, and both Share and NTFS permissions were configured to enforce **Role-Based Access Control (RBAC)** . Access testing confirmed that users could access only the folders assigned to their respective departments, while unauthorized access attempts were denied. The Domain Administrator retained unrestricted access to all shared resources, illustrating the hierarchy of administrative privileges within Active Directory. This exercise reinforced the importance of combining Share and NTFS permissions to implement secure and centralized file access management in enterprise environments. 

