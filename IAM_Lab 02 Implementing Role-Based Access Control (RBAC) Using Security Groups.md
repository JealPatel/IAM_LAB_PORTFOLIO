# **Active Directory Lab 02** 

# **Implementing Role-Based Access Control (RBAC) Using Security Groups** 

# **Objective** 

The objective of this lab was to implement **Role-Based Access Control (RBAC)** in an Active Directory environment by creating security groups, assigning users to their respective groups based on departmental roles, and verifying domain authentication through client login. This lab demonstrated how Active Directory security groups simplify user management and provide centralized access control in enterprise environments. 

# **Lab Environment** 

# **Component Details** 

Operating System Windows Server (Domain Controller) Client Machine Windows 11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used Active Directory Users and Computers (ADUC) 

# **Step 1: Creating Security Groups** 

The lab began by opening the **Active Directory Users and Computers (ADUC)** console on the Domain Controller. Inside the **_GROUPS** Organizational Unit, three security groups were created to represent different organizational departments. Each group was configured with a **Global** group scope and **Security** group type to support role-based access management within the domain. 

The following security groups were created: 

- **IT_Team** 

- **HR_Team** 

- **Sales_Team** 

These groups were designed to organize users according to their departmental responsibilities and provide a scalable method for assigning permissions in future administrative tasks. 

**Result** 



<!-- Start of picture text -->
=| Active Directory Users and Computers<br>File Action View Help Ss<br>eo>\aml ¢(O\XOGSBIBm| Rar oe<br>xr = | Active Directory Users and Com]! Name Type Description<br>¥ = Seve Queries Be HR_TEAM Security Group...<br>>me ADMINS. 82——IT_TEAM Securitya Group...<br>~ (fi)= EMPLOYEES ES ASALES——TEAM SecurityoeG bx<br>(ej HR<br>> Hi IT<br>> fy SALES<br>3) _GROUPS<br>» [) Builtin<br><!-- End of picture text -->



<!-- Start of picture text -->
BF Active Directory Users and Computers — O ~<br>i<br>File Action View Help<br>I | | | IT_TEAM Properties ? Es<br>‘| BF Active Directory Users and Corn<br>» (5) Saved Queries General Members MemberOF ManagedBy<br>v Sj mydomain.com<br>> By _ADMINS Members:<br>: ~~ (BE) EMPLOYEES Name Active Directory Domain Services Folder<br>(a) HR a alice johnson mydomain.com/_EMPLOYEESIT<br>IT RR john doe medomain.com EMPLOYEES IT<br>(&) SALES<br>=) GROUPS<br>> P| Builtin<br>> ©) Computers<br>> (&) Domain Controllers<br>> ©) ForeignSecurityPrincipal:<br>> [A Managed Service Accour<br>» (2) Users<br>Add... Remove<br>S e Cancel Apply<br>ervices ervices.<br><!-- End of picture text -->



<!-- Start of picture text -->
: =<br>Other user<br>mydomain\john.doe<br>eccccccccce a ><br>Sign in to: mydomain<br>© MYO How do | sign in to another domain?<br>© Other user @ * O<br><!-- End of picture text -->

This lab demonstrated the implementation of **Role-Based Access Control (RBAC)** using Active Directory security groups. Department-based security groups were successfully created, and users were assigned according to their organizational roles. Group memberships were verified to ensure accurate user assignments, and domain authentication was successfully tested using the Windows 11 client machine. The lab provided practical experience in centralized identity and access management, highlighting how security groups simplify permission management and improve administrative efficiency in enterprise Active Directory environments. 

