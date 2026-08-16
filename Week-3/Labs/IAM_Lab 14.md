**Linux Lab 14**

**Linux Command-Line Fundamentals – File System Navigation, File Management & Permissions**

**Objective**

The objective of this lab was to develop practical Linux command-line skills by working with directories, files, file permissions, and file ownership.

The lab focused on using basic Linux commands such as pwd, ls, cd, mkdir, touch, cp, mv, rm, chmod, and chown. These commands provide the foundation for Linux system administration and are frequently used when working with servers, logs, permissions, and security-related tasks.

**Lab Environment**

| **Component** | **Details** |
|--------------------|-----------------------------------------------------|
| Linux Machine | Ubuntu-Lab |
| Operating System | Ubuntu Linux |
| Linux User | labuser |
| Domain Controller | DC-Server |
| User Password | P@ssw0rd123 |
| Terminal | Linux Terminal |
| Commands Practiced | pwd, ls, cd, mkdir, touch, cp, mv, rm, chmod, chown |

**Part 1: Starting the Virtual Machines**

**Step 0: Start Your VMs**

**Procedure**

1. Started the **DC-Server** virtual machine.

2. Waited for the server to finish booting.

3. Logged in using:

Username: mydomain\Administrator

4. Started the **Ubuntu-Lab** virtual machine.

5. Logged in using:

Username: labuser

Password: P@ssw0rd123

**Expected Terminal**

After logging in, the terminal should display something similar to:

labuser@ubuntu-lab:~\$

**Result**

The Ubuntu-Lab VM was successfully started and the labuser account was successfully logged in.

**Screenshot 1:** Ubuntu terminal showing labuser@ubuntu-lab:~\$ 

**Part 2: Linux File System Navigation**

**Step 1: Display the Current Working Directory**

**Command**

pwd

**Expected Output**

/home/labuser

**Observation**

The pwd command displays the **current working directory**.

In this case, the user is located inside:

/home/labuser

**Result**

The current working directory was successfully identified.

**Screenshot 2:** pwd command showing /home/labuser

**Step 2: List Files Including Hidden Files**

**Command**

ls -la

**Observation**

The command displays files and directories, including hidden files.

Example:

drwxr-xr-x

drwxr-xr-x

-rw-r--r--

-rw-r--r--

-rw-r--r--

Important information displayed includes:

- File permissions

- Number of links

- Owner

- Group

- File size

- Modification date

- File name

**Permission Symbols**

| **Symbol** | **Meaning** |
|------------|---------------|
| \- | Regular file |
| d | Directory |
| l | Symbolic link |
| r | Read |
| w | Write |
| x | Execute |

**Result**

The contents of the home directory, including hidden files, were successfully displayed.

**Screenshot 3:** ls -la output

**Step 3: Navigate to the Root Directory**

**Command**

cd /

Then:

pwd

**Expected Output**

/

The / directory represents the **root directory** of the Linux file system.

Next, execute:

ls

**Expected Directories**

You may see directories such as:

bin

boot

dev

etc

home

lib

media

mnt

opt

proc

root

run

sbin

srv

sys

tmp

usr

var

**Observation**

The root directory contains the main directory structure of the Linux operating system.

**Result**

Successfully navigated from the user's home directory to the Linux root directory.

**Step 4: Navigate to /var/log**

**Command**

cd /var/log

Then:

pwd

**Expected Output**

/var/log

Next:

ls -la

**Observation**

The /var/log directory contains system and application logs.

Depending on the Ubuntu version and configuration, files may include:

auth.log

syslog

kern.log

dpkg.log

**Result**

Successfully navigated to the Linux log directory and inspected its contents.

**Step 5: Return to the Home Directory**

**Command**

cd ~

Then:

pwd

**Expected Output**

/home/labuser

**Observation**

The ~ symbol represents the current user's home directory.

For labuser:

~ = /home/labuser

**Result**

Successfully returned to the user's home directory.

**Part 3: File and Directory Management**

**Step 6: Create a Directory**

**Command**

mkdir myfolder

Then:

ls

**Observation**

A new directory named:

myfolder

appeared in the home directory.

**Result**

A directory was successfully created using mkdir.

**Step 7: Create an Empty File**

**Command**

touch myfile.txt

Then:

ls

**Observation**

A new empty file named:

myfile.txt

was created.

**Result**

Successfully created an empty file using touch.

**Step 8: Copy a File**

**Command**

cp myfile.txt myfile_copy.txt

Then:

ls

**Observation**

Two files were now present:

myfile.txt

myfile_copy.txt

The cp command created a copy of the original file.

**Result**

The file was successfully copied.

**Step 9: Move a File**

**Command**

mv myfile_copy.txt /tmp/

Then verify:

ls

The copied file should no longer appear in the home directory.

Next:

ls /tmp/

**Observation**

myfile_copy.txt was moved from /home/labuser to /tmp.

**Result**

The file was successfully moved to the /tmp directory.

**Step 10: Remove a File**

**Command**

rm myfile.txt

Then:

ls

**Observation**

The myfile.txt file was removed from the home directory.

**Result**

The file was successfully deleted using the rm command.

**Part 4: Linux File Permissions**

**Step 11: Create a New File and Check Permissions**

Since myfile.txt was deleted in the previous step, create it again:

touch myfile.txt

Then:

ls -l myfile.txt

**Expected Output**

The output should be similar to:

-rw-r--r-- 1 labuser labuser 0 Aug 10 10:15 myfile.txt

**Permission Breakdown**

-rw-r--r--

│

├── rw- → User/Owner

├── r-- → Group

└── r-- → Others

| **Permission** | **Meaning** |
|----------------|-------------------------|
| \- | Regular file |
| rw- | User can read and write |
| r-- | Group can read |
| r-- | Others can read |

**Observation**

The file owner is labuser, and the default permissions allow the owner to read/write while group and other users have read-only access.

**Result**

File permissions and ownership were successfully inspected.

**Step 12: Change File Permissions Using chmod**

**Command**

chmod 755 myfile.txt

Then:

ls -l myfile.txt

**Expected Output**

-rwxr-xr-x 1 labuser labuser 0 Aug 10 10:15 myfile.txt

**Understanding 755**

The permission value is:

755

It can be divided into:

7 5 5

│ │ │

User Group Others

| **Number** | **Permission** | **Meaning** |
|------------|----------------|----------------------|
| 7 | rwx | Read, Write, Execute |
| 5 | r-x | Read, Execute |
| 5 | r-x | Read, Execute |

**Observation**

The chmod command changed the file permissions so that:

- Owner → Read, Write, Execute

- Group → Read, Execute

- Others → Read, Execute

**Result**

File permissions were successfully modified using chmod.

**Step 13: Change File Ownership Using chown**

**Command**

chown labuser:labuser myfile.txt

**Observation**

The command ensures that:

Owner: labuser

Group: labuser

The ownership was already expected to be configured this way because the file was created by labuser, but the command provided practical experience with ownership management.

**Result**

The file ownership was successfully verified/set to:

labuser:labuser

**Command Summary**

| **Command** | **Purpose** |
|------------------|----------------------------------------|
| pwd | Displays the current working directory |
| ls -la | Lists files including hidden files |
| cd / | Navigates to the root directory |
| cd /var/log | Navigates to the log directory |
| cd ~ | Returns to the user's home directory |
| mkdir myfolder | Creates a directory |
| touch myfile.txt | Creates an empty file |
| cp | Copies a file |
| mv | Moves a file |
| rm | Removes a file |
| ls -l | Displays detailed file information |
| chmod | Changes file permissions |
| chown | Changes file ownership |

**Troubleshooting / Observations**

| **Task** | **Observation** | **Result** |
|-------------|---------------------------------|---------------|
| pwd | Displayed /home/labuser | ✅ Successful |
| ls -la | Displayed files and permissions | ✅ Successful |
| cd / | Navigated to root | ✅ Successful |
| cd /var/log | Accessed system logs | ✅ Successful |
| cd ~ | Returned to home directory | ✅ Successful |
| mkdir | Created myfolder | ✅ Successful |
| touch | Created myfile.txt | ✅ Successful |
| cp | Created file copy | ✅ Successful |
| mv | Moved file to /tmp | ✅ Successful |
| rm | Deleted file | ✅ Successful |
| chmod 755 | Changed file permissions | ✅ Successful |
| chown | Set ownership | ✅ Successful |

**Key Takeaways**

**1. Linux File System Navigation**

Linux uses a hierarchical file system beginning at:

/

The user's home directory was:

/home/labuser

and system logs were located under:

/var/log

**2. File Permissions**

Linux permissions use three primary categories:

User → Group → Others

For example:

-rwxr-xr-x

means:

User: rwx

Group: r-x

Others: r-x

**3. Numeric Permissions**

The chmod 755 command uses numeric permission values:

7 = rwx

5 = r-x

5 = r-x

Therefore:

755 = rwxr-xr-x

**4. File Ownership**

Linux files have an owner and group.

Example:

labuser labuser

The chown command can be used to change ownership.

**Skills Demonstrated**

- Linux Command Line

- Linux File System Navigation

- File and Directory Management

- Linux File Permissions

- Linux File Ownership

- chmod

- chown

- ls

- cd

- pwd

- mkdir

- touch

- cp

- mv

- rm

- Linux Log Directory Analysis

- Basic Linux System Administration

**Conclusion**

This lab provided hands-on experience with fundamental Linux command-line operations. The exercises covered navigating the Linux file system, viewing files and hidden files, creating and managing directories and files, copying and moving files, deleting files, and working with Linux file permissions and ownership.

The lab also provided practical exposure to the /var/log directory, which is particularly important in cybersecurity because Linux system and authentication logs can be analyzed during security monitoring and incident investigations.

By completing this lab, practical skills were developed in **Linux administration, file system management, permission management, ownership management, and command-line navigation**, providing a foundation for further Linux and cybersecurity labs.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_14_1.png)

![Screenshot 2](IAM_Lab_14_2.png)

![Screenshot 3](IAM_Lab_14_3.png)

![Screenshot 4](IAM_Lab_14_4.png)

![Screenshot 5](IAM_Lab_14_5.png)

![Screenshot 6](IAM_Lab_14_6.png)

![Screenshot 7](IAM_Lab_14_7.png)

![Screenshot 8](IAM_Lab_14_8.png)

![Screenshot 9](IAM_Lab_14_9.png)

![Screenshot 10](IAM_Lab_14_10.png)

![Screenshot 11](IAM_Lab_14_11.png)

![Screenshot 12](IAM_Lab_14_12.png)

![Screenshot 13](IAM_Lab_14_13.png)

![Screenshot 14](IAM_Lab_14_14.png)

![Screenshot 15](IAM_Lab_14_15.png)

![Screenshot 16](IAM_Lab_14_16.png)

![Screenshot 17](IAM_Lab_14_17.png)

![Screenshot 18](IAM_Lab_14_18.png)

