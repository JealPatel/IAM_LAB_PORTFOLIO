# **Active Directory Lab 05** 

# **Automating Active Directory User Management with PowerShell** 

# **Objective** 

The objective of this lab was to learn how to automate Active Directory administration using **PowerShell** . The lab focused on creating multiple user accounts through a PowerShell script and generating user reports by exporting Active Directory information to CSV files. This exercise demonstrated how automation reduces repetitive administrative tasks and improves efficiency in enterprise environments. 

# **Lab Environment** 

**Component Details** Operating Windows Server (Domain Controller) System Virtualization VMware Workstation / VirtualBox Domain mydomain.com Windows PowerShell ISE, Active Directory Module, Active Directory Users and Tool Used Computers (ADUC) 

# **Step 1: Launching Windows PowerShell ISE** 

Windows PowerShell ISE was opened on the Domain Controller with administrative privileges. The scripting environment provided a script editor for writing PowerShell code and an integrated console for executing and testing commands. 

The environment was prepared to automate Active Directory administrative tasks. 

# **Result** 

PowerShell ISE was successfully launched with administrator privileges. 



<!-- Start of picture text -->
g Administrator: Windows PowerShell [SE<br>File Edit View Tools Debug Add-ons Help<br>Heaué¢ a» #9 >a |e | alBoaon)|&e.<br>| Untitledt.pst* | e<br>1 Write-Host "Starting User Creation" -ForegroundColor Yellow<br>2 Fi..10 ForEach-Object {|<br>3 $username = “User$_"<br>4 $password = ConvertTo-SecureString "“P@ssword123" -AsPlainText -Force<br>5<br>6 New-ADUser -Name $username ~<br>7 -SamAccountName $username *<br>8 -UserPrincipalName "Susername@mydomain.com” *<br>9 -Enabled $true ~<br>10 -AccountPassword Spassword<br>11<br>12 Write-Host "Created User: $usename" -ForegroundColor Blue<br>13 |}<br>14 Write-Host "All 10 users Created Successfully!" -ForegroundColor White<br>15<br>PS C:\Users\Administrator><br><!-- End of picture text -->

5 



<!-- Start of picture text -->
><br><!-- End of picture text -->

PS C:\\Users\Administrator> C:\Users\Admnistrator\Desktop\Days Powershell Scripting.psi Starting User Creation 

Al] 10 users Created Successfully! 

PS C:\Users\Administrator> | 

Zompleted 

Ln” 



<!-- Start of picture text -->
Tea Server Manager Is<br>Server Manager » Dashboard ~@1 PF Manage<br>© Active Directory Users and Computers - oO ~*~<br>aaa Dashboa File Action View Help<br>:— Local Se @*9/SZFl= 4 EXER= BIER|= —|@SBR%, teETO“4<br>Lnfe All Serve = | Active Directory Users and Com!) Name Type Description “A<br>iglHE Ee od= owes Gueriesi BE Group Polic.. Security Group... Mernbers inthis group c...<br>& DNS ¥ a my ADMINS @, Guest User Built-in accountfor que...<br>BE Fil d4 oad ~ ®, Jeal_Patel User<br>i rile an a) EMPLOYEES : . .<br>iS] GROUPS BE Key Admins Security Group... Mernbers of this group...<br>a Builtin Bo krbtgt User Key Distribution Center...<br>©) Computers a, Nisarg_Vade.., User<br>Domain Controllers BE Protected Us. Security Group... Members of this group.<br>15 ForeignSecurityPrincipal: BE RAS and 14... Security Group... Servers in this group cana,<br>(3 Keys BP Read-only O.. Security Group... Members of this group ..<br>©) Lost&ndFound BR Schema Ad. Security Group... Designated administrata..,<br>(4) Managed Service Accour @ Usert User<br>(|) Program Data a User User<br>(|) Systern B, User2 User<br>Users a User3 User<br>(|) NTS Quotas ®, Userd User<br>(| TPM Devices a, Users User<br>a, Useré User<br>a, User? User<br>a, Userd User<br>a Userd User<br>< > we<br>erices erices<br><!-- End of picture text -->



<!-- Start of picture text -->
PS C:\Users\Administrator> Get-ADUser -Filter *|Export-Csyv C:\Users\Administrator\Desktop\Al lusers.csy —NoTypeInformation<br>PS C:\Users\\Administrator><br><!-- End of picture text -->

~ | Allusers - Notepad - x File Edit Format View Help i DistinguishedName”, "Enabled" ,“GivenName”™ , “Name” ,"“ObjectClass”,"ObjectGUID" , “SamAccountName” , "SID", “Surname”, "“UserPrincipalNa “CN=Administrator, CN=Users , DC=mydomain,DC=com", "True", ,"Administrator", "user", "Iefff4d-fb34-4F89-933F -78262e499187" , "Adminis “CN=Guest, CN=Users , DC=mydomain, DC=com","False", ,“Guest", "user" ,"@5026b5b-4e56-43df -9c6c-f320f3caOfef" “Guest” ,"S-1-5-21-24739 "CN=krbtgt, CN=Users ,DC=mydomain,DC=can", "False", ,"krbtgt", "user" ,"955d234e-f79e-4c1b-95b4-b8fc@dée2bbf","krbtgt" ,"S-1-5-21-24 “CN=john doe ,OU=IT ,OU=_EMPLOYEES ,DC=mydomain,DC=com","True","john","john doe" ,"user" ,"ff769d95 -ba69-48f2-bd@b-c6132249e683" ," “CN=jane smith,OU=HR ,OU=_EMPLOYEES, DC=mydomain, DC=com", "True", "jane","jane smith", “user™,"b849978c-f39b-4c39-aa99-efbO729ebdF “CN=charlie broawn,OQU=HR,OU= EMPLOYEES, DC=mydomain,DC=com","True","charlie","“charlie brown" ,“user”,"e51c2f43-45b2-420b-998b-Ge “CN=bob wilson,OU=SALES,OU=_EMPLOYEES,DC=mydomain,DC=com","“False","“bob","bob wilson","“user","8878a2a7 -9359-4168-b1a3-66f96f9c “CN=alice johnson,OQU=IT,OU=_EMPLOYEES, DC=mydomain,DC=com","True","alice","“alice johnson","user” ,"7687cda3-49e0-ded@-8c8c-c2ce “CN=Jeal_Patel,CN=Users ,DC=mydomain, DC=com","“True", ,"“Jeal_Patel", “user” ,"947982e4-d1le6-4c9a-bcc4-6300810b7d65" ,"“jeal.patel”," “CN=Nisarg Vadechiya, CN=Users , DC=mydomain, DC=com", "True", ,"Nisarg Vadechiya", "user", "fcd5cc5c-@dal-da7b-8159-6fa101231166" ,"n “CN=User1,CN=Users , DC=mydomain, DC=com","True", ,“User1", “user” ,"e153a504-8994-41d8- aafb-71b875dc48a8" , “User1" ,"S-1-5-21-247395 “CN=User2,CN=Users ,DC=mydomain,DC=com","True", ,"User2”, "user" ,"348d7a94-673-4daa0-aac3-96dfbaSa3d5d","User2™ ,"S-1-5-21-247395 “CN=User3,CN=Users , DC=mydomain, DC=com","True", ,"User3", "user" ,"c@79efba-4522-4838 - ad6c-daf fb2bb1idca” , “User3" ,"S-1-5-21-247395 “CN=User4, CN=Users , DC=mydomain, DC=com" “True”, ,"“User4" “user” ,“e@0986F8-bb87 -4053-920f -a29daf315184" ,"“Userd™ ,"S-1-5-21-247395 “CN=UserS ,CN=Users , DC=mydomain,DC=com","True", ,"UserS", “user”, “db43f2a5 -e66e-4bd5 -afee-@7c849cccSaf" ,“UserS” ,"S-1-5-21-247395 “CN=User6,CN=Users , DC=mydomain, DC=com" "True", ,"User6", “user” ,"“dd356ff4-9a85 -49d5 -bb69-5 febaS45b8fc" ,"“User6™ ,"S-1-5-21-247395 “CN=User7,CN=Users ,DC=mydomain,DC=com","True", ,"User?", "user", "ef 263eb5 -4db9-48c6-adb7-fe57f1F926dd" “User?” ,"S-1-5-21-247395 “CN=Useré, CN=Users , DC=mydomain, DC=com","True™, ,“User8", “user” ,"28fd555e-6e75 -4715 - aeO7 -3996142ad11e", “Users” ,"S-1-5-21-247395 “CN=User9, CN=Users , DC=mydomain,DC=com","True", ,"User9", "user" ," LedeS8af -273f -4336-b5f2-9386a3808e2a" ,"User9” ,"S-1-5-21-247395 “CN=User16,CN=Users ,DC=mydomain, DC=com", "True", ,“User 10", "user" ,"56fces00-67cd-4414-9c81-e5 1630a936a6" , “User16","S-1-5-21-247 



<!-- Start of picture text -->
I<br><!-- End of picture text -->

# **Conclusion** 

This lab demonstrated the use of **PowerShell automation** for managing Active Directory users in a Windows Server environment. A PowerShell script was successfully developed and executed to create multiple user accounts automatically, significantly reducing manual administrative effort. The lab also demonstrated how PowerShell can be used to generate comprehensive user reports by exporting Active Directory information into CSV files. Overall, this exercise highlighted the importance of automation in enterprise system administration, improving efficiency, consistency, and scalability while simplifying routine identity management tasks. 

