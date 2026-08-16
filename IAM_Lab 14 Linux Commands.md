# **Linux Lab 14** 

# **Linux Command-Line Fundamentals – File System Navigation, File Management & Permissions** 

# **Objective** 

The objective of this lab was to develop practical Linux command-line skills by working with directories, files, file permissions, and file ownership. 

The lab focused on using basic Linux commands such as pwd, ls, cd, mkdir, touch, cp, mv, rm, chmod, and chown. These commands provide the foundation for Linux system administration and are frequently used when working with servers, logs, permissions, and security-related tasks. 

# **Lab Environment** 

|**Component**|**Details**|
|---|---|
|Linux Machine|Ubuntu-Lab|
|Operating System|Ubuntu Linux|
|Linux User|labuser|
|Domain Controller|DC-Server|
|User Password|P@ssw0rd123|
|Terminal|Linux Terminal|



Commands Practiced pwd, ls, cd, mkdir, touch, cp, mv, rm, chmod, chown 

Whuntu 26.84 LTS ubuntu-lab ttyl Wountu-lab login: labuser Password: Welcome to Ubuntu 26.44 LTS (GNU/Linux 7.@.@-14-generic ~86_64) * Documentation: httos://docs.ubuntu.com * Management: httos://landscape.canonical.com 4a Support: https: //ubuntu.campro System information as af Mon Aug 18 86:12:17 AM UTC 2826 System load: 9.56 Processes: 123 Memory usage: 13% IPv4 address for enpa@sd: 172.16.4.186 Suap usage: Ox Expanded Security Maintenance for Applications is not enabled. @ updates can be applied immediately. Enable ESM Apos to receive additional future security updates. See https://ubuntu.com’esm or run: sudo pra status 

# **Part 2: Linux File System Navigation** 

# **Step 1: Display the Current Working Directory** 

# **Command** 

pwd 

# **Expected Output** 

/home/labuser 

# **Observation** 

The pwd command displays the **current working directory** . 

In this case, the user is located inside: 

/home/labuser 

# **Result** 

The current working directory was successfully identified. 

**Screenshot 2:** pwd command showing /home/labuser 



# **Step 2: List Files Including Hidden Files** 

# **Command** 

ls -la 

# **Observation** 

The command displays files and directories, including hidden files. 

Example: 

drwxr-xr-x 

drwxr-xr-x 

-rw-r--r-- 

- -rw-r--r-- 

- -rw-r--r-- 

Important information displayed includes: 

- File permissions 

- Number of links 

- Owner 

- Group 

- File size 

- Modification date 

- File name 

# **Permission Symbols** 

# **Symbol Meaning** 

- Regular file 

- d Directory 

- l Symbolic link 

- r Read 

- w Write 

- x Execute 

# **Result** 

labuser@ubuntu-lab:"£ ls -la total 32 druwxr-x--4 labuser labuser 4696 Aug 9 @B:f8 drwxr-xr-* 3 root root 4096 Aug 9 @a:e4 -Pu------1 labuser labuser 214 Aug 9 8:28 .bash_history -Pu-r--p-1 labuser labuser 228 Feb 139 12:16 .bash_logout -pu-p--r-1 labuser labuser 3771 Feb 13 12:16 .bashre drux-----2 labuser labuser 4896 Aug 9 68:69 -pu-r--r-1 labuser labuser 887 Feb 13 12:16 .profile drwx-----2 labuser labuser 4896 Aug 9 @a:a9 labuser@ubuntu-lab: S$ 



<!-- Start of picture text -->
labuser@gubuntu-lab:"$ cd ?<br>labuser@ubuntu-lab:/$ pwd<br>labuser@ubuntu-lab:7 _<br><!-- End of picture text -->

labuser@ubuntu-lab:/% ls bin labuser@ubuntu-lab:/$ _ 

lib lib64 

sbin 

Swap. img 



<!-- Start of picture text -->
labuser@ubuntu-lab:/% cd /yvar<br>labuser@ubuntu-lab:/vars ls<br>lack run<br><!-- End of picture text -->

labuser@ubuntu-lab:/$ cd /var/log labuser@ubuntu-lab:=, m— ore -, “| so rs“var/=e logsseed 



<!-- Start of picture text -->
abuser@ubuntu-lab:/var/log¢ ls<br>;EADME apport.log auth. log btmp cloud-init-output. log dmesg.@ kern. log lastlog syslog<br>lternatives. log bootstrap. log cloud-init. log dmesg dpkg. log wtmp<br>abuser@ubuntu-lab:/var/log$ ls -la<br>otal 1448<br>drwxrwxr-x 11 root syslog 4096 Aug 16 68:11<br>drwxr-xr-x 13 root root 4096 Aug 9 08:08<br>PUXPUXPUX 1 root root 39 Apr 20 18:66 README -> ../../usr/share/doc/systemd/README. logs<br>rw-P--P-- 1 root root 28899 Apr 20 18:12 alternatives.log<br>rw-r----- 1 root adm @ Aug 9 08:08 apport. log<br>drwxr-xP-x 2 root root 4096 Aug 39 88:64<br>rw-P----- 1 syslog adm 4281 Aug 16 68:17 auth. log<br>rw-r--r-- 1 root root 87406 Apr 206 18:65 bootstrap.log<br>rw-Pw---- 1 root utmp 6 Apr 2@ 18:05 btmp<br>Irwxr - x= - = 2 _chrony _chrony 4096 Aug 9 88:68<br>rw-P----- 1 root adm 4163 Aug 9 68:69 cloud-init-output.log<br>rw-P----- 1 syslog adm 96256 Aug 9 08:09 cloud-init.log<br>irwxr -xP-x 2 root root 4096 Apr 16 17:56<br>rw-P----- 1 root adm 54856 Aug 16 68:11 dmesg<br>rw-P----- 1 root adm 54116 Aug 9 08:68 dmesg.@<br>rw-P--P-- 1 root root 660033 Aug 9 08:05 dpkg. log<br>IP WXPWX - - - 4 root adm 4096 Aug 9 88:65<br>Irwxr-sr-x+ 3 root systemd- journal 4096 Aug 9 68:08<br>rw-P----- 1 syslog adm 120084 Aug 10 08:12 kern. log<br>drwxr- xP -x 2 landscape landscape 4096 Apr 20 18:22<br>rw-Pu-r-- 1 root utmp @ Apr 2@ 18:05 lastlog<br>Jrwx------ 2 root root 4096 Apr 26 18:06<br>rw-P----- 1 syslog adm 291141 Aug 10 98:20 syslog<br>Irwxr-xP-% 2 root root 4096 Aug 16 68:11<br>drwxr-x--- 2 root adm 4096 Aug 9 88:08<br>rw-ruw-r-- 1 root utmp 768 Aug 16 08:11 wtmp<br>abuser@ubuntu-lab:/var/ logs _<br><!-- End of picture text -->

labuser@ubuntu-lab:var-logé cd ™ labuser@ubuntu-lab:"$ _ 

abuser@ubuntu-lab:"s pwd “home labuser 

; 

> labuser@ubuntu-lab:"S$ mkdir mytolder 

> labuser@ubuntu-lab:"$s 1s labuser@ubuntu-lab:"s _ 

abuser@ubuntu-lab:"$ touch myfile.txt abuser@ubuntu-lag:“$ Ls nyfile.txt abuser@ubuntu-lag: “$s 

abuser@ubuntu-lab:"$ co mytile.tet mytile_copy.txt abuser@ubuntu-lab:"s 1s natile.tsxt myfile_copy.txt abuser@ubuntu-lab: $ 



<!-- Start of picture text -->
abuser@ubuntu-lab:“$ my myfile_copy.txt /tmp/<br>abuser@ubuntu- lab: ~$<br>abuser@ubuntu-lab:“$ ls /tmp/<br>myfile.txt<br>nyf ile_copy.txt<br>a<br><!-- End of picture text -->

abuser@ubuntu-lab:“$ my myfile_copy.txt /tmp/ abuser@ubuntu- lab: ~$ abuser@ubuntu-lab:“$ ls /tmp/ myfile.txt nyf ile_copy.txt a 

labuser@ubuntu-lab:"$ touch mytile.tst labuser@ubuntu-lab:"s ls mytile.tet labuser@gubuntu-lab:"¢ pm mytile.txt labuser@ubuntu-lab:“# Is labuser@ubuntu-lab:"s 

labuser@ubuntu-lab:"$ touch myfile.txt labuser@ubuntu-lab:"$ ls -1 myfile.txt -ru-ruw-p-1 labuser labuser @ Aug 16 88:36 mytile.txt labuser@ubuntu-lab:"s 

labuser@ubuntu-lab:"$ chmod 755 mytile.txt labuser@ubuntu-labp:"$ ls -1l mytile.txt -ruxr-xe-x 1 labuser labuser @ Aug 18 88:3a@ myfile.txt labuser@ubuntu-lab: $ 

abuser@ubuntu-lab:"$ chown labuser: labuser myfile.txt abuser@ubuntu-lap:"“s ls -1l mytile.tet ruwxr-xe-x 1 labuser labuser @ Aug 1@ @@:5@ mytile.txt abuser@ubuntu-lab:"$ _ 

|**Command**|**Purpose**|
|---|---|
|cd /|Navigates to the root directory|
|cd /var/log|Navigates to the log directory|
|cd ~|Returns to the user's home directory|
|mkdir myfolder|Creates a directory|
|touch myfle.txt|Creates an empty fle|
|cp|Copies a fle|
|mv|Moves a fle|
|rm|Removes a fle|
|ls -l|Displays detailed fle information|
|chmod|Changes fle permissions|
|chown|Changes fle ownership|



# **Troubleshooting / Observations** 

|**Task**|**Observation**|**Result**|
|---|---|---|
|pwd|Displayed /home/labuser|✅Successful|
|ls -la|Displayed fles and permissions|✅Successful|



# **Task Observation** 

# **Result** 

|cd /|Navigated to root|✅Successful|
|---|---|---|
|cd /var/log|Accessed system logs|✅Successful|
|cd ~|Returned to home directory|✅Successful|
|mkdir|Created myfolder|✅Successful|
|touch|Created myfle.txt|✅Successful|
|cp|Created fle copy|✅Successful|
|mv|Moved fle to /tmp|✅Successful|
|rm|Deleted fle|✅Successful|
|chmod 755|Changed fle permissions|✅Successful|
|chown|Set ownership|✅Successful|



# **Key Takeaways** 

# **1. Linux File System Navigation** 

Linux uses a hierarchical file system beginning at: 

/ 

The user's home directory was: 

/home/labuser 

and system logs were located under: 

/var/log 

# **2. File Permissions** 

Linux permissions use three primary categories: 

User → Group → Others 

For example: 

-rwxr-xr-x 

means: 

User:   rwx 

Group:  r-x 

Others: r-x 

# **3. Numeric Permissions** 

The chmod 755 command uses numeric permission values: 

7 = rwx 

5 = r-x 

5 = r-x 

Therefore: 

755 = rwxr-xr-x 

# **4. File Ownership** 

Linux files have an owner and group. 

Example: 

labuser labuser 

The chown command can be used to change ownership. 

# **Skills Demonstrated** 

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

# **Conclusion** 

This lab provided hands-on experience with fundamental Linux command-line operations. The exercises covered navigating the Linux file system, viewing files and hidden files, creating and managing directories and files, copying and moving files, deleting files, and working with Linux file permissions and ownership. 

The lab also provided practical exposure to the /var/log directory, which is particularly important in cybersecurity because Linux system and authentication logs can be analyzed during security monitoring and incident investigations. 

By completing this lab, practical skills were developed in **Linux administration, file system management, permission management, ownership management, and command-line navigation** , providing a foundation for further Linux and cybersecurity labs. 

