**Active Directory Lab 05**

**Automating Active Directory User Management with PowerShell**

**Objective**

The objective of this lab was to learn how to automate Active Directory administration using **PowerShell**. The lab focused on creating multiple user accounts through a PowerShell script and generating user reports by exporting Active Directory information to CSV files. This exercise demonstrated how automation reduces repetitive administrative tasks and improves efficiency in enterprise environments.

**Lab Environment**

| **Component** | **Details** |
|----|----|
| Operating System | Windows Server (Domain Controller) |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | Windows PowerShell ISE, Active Directory Module, Active Directory Users and Computers (ADUC) |

**Step 1: Launching Windows PowerShell ISE**

Windows PowerShell ISE was opened on the Domain Controller with administrative privileges. The scripting environment provided a script editor for writing PowerShell code and an integrated console for executing and testing commands.

The environment was prepared to automate Active Directory administrative tasks.

**Result**

PowerShell ISE was successfully launched with administrator privileges.

**Step 2: Creating Multiple Active Directory Users Using PowerShell**

A PowerShell script was written to automate the creation of multiple Active Directory user accounts. The script generated ten user accounts named **User1** through **User10**. Each account was assigned the password **P@ssw0rd123**, enabled immediately after creation, and configured with a User Principal Name (UPN) under the **mydomain.com** domain.

The script displayed progress messages during execution, confirming the successful creation of each user account.

**Result**

The PowerShell script successfully created ten Active Directory user accounts automatically, demonstrating the effectiveness of automation in reducing repetitive administrative tasks.

**Screenshot 2:** *PowerShell Script Execution*

**Step 3: Saving the PowerShell Script**

The completed PowerShell script was saved on the Administrator Desktop using the filename **Day5_CreateUsers.ps1**. Saving the script allows it to be reused whenever multiple user accounts need to be created in the future.

**Result**

The automation script was successfully saved for future use.

**Step 4: Executing the Automation Script**

The saved script was executed within Windows PowerShell ISE. During execution, the console displayed a confirmation message for every newly created user account, followed by a completion message indicating that all users had been created successfully.

**Result**

The script executed successfully without errors and created all ten user accounts in Active Directory.

**Screenshot 4:** *Successful Script Output*

**Step 5: Verifying User Creation**

After executing the script, the **Active Directory Users and Computers (ADUC)** console was opened to verify the results. The newly created user accounts (**User1** through **User10**) were present within the Active Directory domain, confirming that the automation process completed successfully.

**Result**

All automatically generated user accounts were successfully verified in Active Directory.

**Screenshot 5:** *Verification of Created Users in ADUC*

**Step 6: Exporting Active Directory Users to CSV**

PowerShell was used to export all user accounts from the Active Directory domain into a CSV file. The generated report contained information for every user account present in the domain, including the Administrator account, previously created departmental users, and the newly created automated user accounts.

The exported file was saved as **AllUsers.csv** on the Administrator Desktop.

**Result**

A complete Active Directory user inventory was successfully exported to a CSV file for reporting purposes.

**Screenshot 6:** *AllUsers.csv Report*

**Step 7: Generating a Detailed User Report**

A second PowerShell command was executed to generate a more detailed report containing selected user attributes such as **Name**, **SamAccountName**, **Enabled Status**, **Last Logon Date**, and **Department**. The filtered information was exported to **UserReport.csv**, providing a cleaner and more organized report for administrative review.

**Result**

A detailed Active Directory user report containing selected account attributes was successfully generated and exported.

**Screenshot 7:** *UserReport.csv*

**Conclusion**

This lab demonstrated the use of **PowerShell automation** for managing Active Directory users in a Windows Server environment. A PowerShell script was successfully developed and executed to create multiple user accounts automatically, significantly reducing manual administrative effort. The lab also demonstrated how PowerShell can be used to generate comprehensive user reports by exporting Active Directory information into CSV files. Overall, this exercise highlighted the importance of automation in enterprise system administration, improving efficiency, consistency, and scalability while simplifying routine identity management tasks.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_05_1.png)

![Screenshot 2](IAM_Lab_05_2.png)

![Screenshot 3](IAM_Lab_05_3.png)

![Screenshot 4](IAM_Lab_05_4.png)

![Screenshot 5](IAM_Lab_05_5.png)

