# **Active Directory Lab 01** 

# **Creating Organizational Units (OUs) and Users in Active Directory** 

# **Objective** 

The objective of this lab was to understand the basic administration of Active Directory by creating Organizational Units (OUs) and manually adding user accounts within a Windows Server domain environment. The lab also demonstrated how to organize users into departmental OUs and configure account properties such as password settings. This exercise provided practical experience with the Active Directory Users and Computers (ADUC) management console, which is widely used in enterprise environments for identity and access management. 

# **Lab Environment** 

# **Component Details** 

Operating System Windows Server (Domain Controller) Client Machine Windows 10/11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used Active Directory Users and Computers (ADUC) 

# **Step 1: Starting the Virtual Machines** 



<!-- Start of picture text -->
ies Server Manager - x<br>Server Manager » Dashboard = ©) | P Manage |e) View _ Help<br>Active Directory Administrative Center<br>Active Directory Domains and Trusts<br>fs Dashboard WELCOME TO SERVER MANAGER Active Directory Module for Windows PowerShell<br>EB Local Server Active Directory Sites and Services<br>ig_igi AllAD ServersDs @ ContigureConfiqureY thistnis local!ocal seser ActivlDirectoryADS! Edit Users and Computers<br>eea DNS QUICK START Component Services<br>.Mi File and Storage Services > < AGGAdd rolesTOlES ailG@and featuresledalures ComputerDefragment and Management Optimize Drives<br>3 Add other servers to man Disk Cleanup<br>DNS<br>SNE 4 Create a server group Event Viewer<br>Group Policy Management<br>5 Connect this server to clo iSCSI Initiator<br>Local Security Policy<br>LEARN MORE Microsoft Azure Services<br>ODBC Data Sources (32-bit)<br>ROLES AND SERVER GROUPS ODBC DataaaipameiaaiensS (64-bit)<br>Roles:3 | Server groups: 1 | Servers total: 1 PHeSTEE STE<br>Print Management<br>ig AD DS 1 3 DNS Recovery Drive<br>Registry Editor<br>(6) Manageability ® Manageability Resource Monitor<br>Events Events SS<br>Services Services SystemSystem ConfigurationInformation<br>Performance Performance Task Scheduler<br>BPA results BPA results Windows Defender Firewall with Advanced Security<br>Windows Memory Diagnostic<br>_PI »0 aAi e B & = Fl Ie 7/27/20263:30 PM a<br><!-- End of picture text -->



<!-- Start of picture text -->
Fix<br>Server Manager » Dashboard ~ © | FP Manage Tools View Help<br>—=1 pee ieay| GFFile ActiveActionDirectoryViewUsersHelp and Computers - o x<br>LMis Local Sei @eo\MIGBIBmMZar ae7<br>in&,ig! AllAD Server DS activeal Saved Directory QueriesUsers and Com|| @mydomain.c...Name= TypeDomain Description<br>— DNS FantDelegate Control... Folderolder to to store yourst fi favo...<br>MiG File and § Find...<br>Change Domain...<br>Change Domain Controller...<br>Raise domain functional level...<br>Operations Masters...<br>New > Computer<br>All Tasks > Contact Hide<br>Refresh Soon<br>InetOrgPerson<br>re TSS msDS-ShadowPrincipalContainer<br>Help mslmaging-PSPs<br>MSMQ Queue Alias<br>Organizational Unit<br>Printer<br>User<br>< 2 Shared Folder<br>Creates a new item in this container.<br>ervices @rvices<br>Performance Performance<br>BPA results BPA results<br>a ©Oo tossFt @ BB ss al Ste cram3:33 PM<br><!-- End of picture text -->

To organize the Active Directory environment, several Organizational Units (OUs) were created under the domain **mydomain.com** . Separate OUs were created for 

administrators, employees, and groups. Within the **_EMPLOYEES** Organizational Unit, additional child OUs were created to represent different organizational departments including **IT** , **HR** , and **Sales** . 

The resulting Active Directory structure was organized as follows: 

mydomain.com │ ├── _ADMINS │ ├── _EMPLOYEES │     ├── IT │     ├── HR │     └── Sales │ └── _GROUPS 

# **Organizational Unit Structure** 

# **Parent OU Child OU** 

mydomain.com _ADMINS 

mydomain.com _EMPLOYEES _EMPLOYEES IT _EMPLOYEES HR _EMPLOYEES Sales mydomain.com _GROUPS 

# **Result** 

The Organizational Unit hierarchy was successfully created according to the planned Active Directory structure, enabling proper administrative organization of departmental resources. 



<!-- Start of picture text -->
Trax<br>Server Manager * Dashboard ~@ 1 P Manage Tools View Help<br>BiHH Dashboahi DDFileActiveAction Directory UsersView Help and Computers - Oo x<br>L Local Set eo\ami¢O|\XSeB\Em|SeeToRa _ _ - =<br>aaje All SSIS Dl Active Directory Users and Com|) Name Type Description<br>igh AD DS *) Saved Queries<br>& DNS v mydomain.com There are no itemsto show in this view.<br>. a) _ADMINS<br>Mi Fileand$ = y 3} EMPLOYEES<br>a) IT<br>a) SALES<br>a) HR<br>a] _GROUPS<br>+ Builtin<br>=| Computers<br>3 Domain Controllers<br>| ForeignSecurityPrincipal: Hide<br>“| Managed Service Accour<br>_) Users<br>< ><br>ervices ervices<br>Performance Performance<br>BPA results BPA results<br>= ©O Ls&i eC & & 2 © Fal Ie 7/27/20263:41 PM ul<br><!-- End of picture text -->



<!-- Start of picture text -->
| New Object - User ~<br>g Create in: = mydomain.com/_EMPLOYEES/IT on<br>ms ti<br>oe<br>User logon name:<br>User logon name (pre-Windows 2000):<br><!-- End of picture text -->



<!-- Start of picture text -->
neEEEEEEEEEEEEEEEEEEEEEEEEETLTLLCOC—S<br><1 oDicocton ee caer ace — o x<br>Ser) | New Object - User x<br>alverve’Se y % Create in: _mydomain.com/_EMPLOYEES/IT jon -<br>DS<br>' ms to show in this view.<br>(C1 User must change password at next logon<br>(User cannot change password<br>Passwordnever expires:<br>(Account is disabled<br><a cane<br>T Services Services<br><!-- End of picture text -->



<!-- Start of picture text -->
i<br>Recvcleein Q Kearch for apps, settings, and documents<br>Pinned All ><br>Edge Outlook Microsoft Store Settings Photos Calculator<br>GQ & ® +<br>Clock Notepad Paint Snipping Tool File Explorer<br>Recommended More ><br>. S john doe 0)<br>>.<br>aiasQu5BE@CB ~ CV®©oa) ipso4:37 AM<br><!-- End of picture text -->

