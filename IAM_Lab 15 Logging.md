# **IAM Lab 15 — Linux Log Analysis & Authentication Monitoring** 

# **Objective** 

The objective of this lab was to practice **Linux log analysis and authentication monitoring** by examining authentication and system logs, identifying failed and successful SSH login attempts, monitoring logs in real time, and counting failed login attempts by source IP address. 

This lab demonstrates a basic : **SOC/Blue Team workflow** 

**Generate activity → Collect logs → Search logs → Identify suspicious activity → Analyze the source** 

# **Lab Environment** 

**Component Details** Domain Controller DC-Server Windows Client Win11-Client Linux Machine Ubuntu-Lab Linux User labuser Linux IP 172.16.0.100 Windows Client IP 172.16.0.50 Log File /var/log/auth.log System Log /var/log/syslog Log Framework systemd/journalctl Protocol Tested SSH 

**Step 0: Start Your VMs** 

# **Procedure** 

1. Started **DC-Server** . 

2. Logged in using: 

mydomain\Administrator 

3. Started **Ubuntu-Lab** . 

4. Logged in as: 

Username: labuser 

Password: P@ssw0rd123 

5. Started **Win11-Client** . 

6. Logged in using: 

mydomain\Administrator 

# **Result** 

All three virtual machines were successfully started. 

**Step 1: Open Ubuntu Terminal** 



<!-- Start of picture text -->
Wbuntu 26.84 LTS ubuntu-lab tty1<br>lubuntu-lab login: labuser<br>Password:<br>Welcome to Ubuntu 26.64 LTS (GNU/Linux 7.@.@-14-generic x86_64)<br>* Documentation: https://docs.ubuntu.com<br>* Management: https: //landscape.canonical.com<br>*« Support: https: //ubuntu.com/proa<br>System information as of Tue Aug 11 10:50:4@ AM UTC 2026<br>System load: 1.14 Processes: 125<br>Usage of /: 46.1% of 9.75GB Users logged in: i)<br>Memory usage: 14% IPv4 address for enp@s3: 172.16.0.100<br>Swap usage: O%<br>Expanded Security Maintenance for Applications is not enabled.<br>@ updates can be applied immediately.<br>Enable ESM Apps to receive additional future security updates.<br>See https://ubuntu.com/esm or run: sudo pro status<br>labuser@ubuntu-lab:“$ _<br><!-- End of picture text -->

abuser@ubuntu-lab:~$ sudo tail -f /var/log/auth. log (sudo: authenticate] Password: P626-08-11710:56:27.983063+00:60 ubuntu-lab systemd-logind[1258]: New seat seate. PO26-08-11710:50:27.983094+00:00 ubuntu-lab systemd-logind[1258]: Watching system buttons on /dev/input/event@ (Power Button) P026-98-11710:50:27.983097+00:00 ubuntu-lab systemd-logind[1258]: Watching system buttons on /dev/input/event1 (Sleep Button) PO26-08-11710:50:27.983101+00:00 ubuntu-lab systemd-logind[1258]: Watching system buttons on /dev/input/event2 (AT Translated Set 2 keyboard) P626-68-11716:56:41.064249+00:00 ubuntu-lab login: pam_unix(login:session): session opened for user labuser(uid=1600) by labuser(uid=6) P626-08-11T10:56:41.102283+00:00 ubuntu-lab systemd-logind[1258]: New session '1' of user ‘labuser' with class 'user' and type ‘tty’. P626-08-11710:56:41.134319+00:60 ubuntu-lab (systemd): pam_unix(systemd-user:session): session opened for user labuser(uid=100@) by labuser(uid=6) P626-08-11710:56:41.135350+00:00 ubuntu-lab systemd-logind[1258]: New session '2' of user ‘labuser' with class 'manager' and type ‘unspecified’. P026-08-11710:52:20.129894+00:00 ubuntu-lab sudo: pam_unix(sudo:session): session opened for user root(uid=6) by labuser(uid=1000) P626-68-11T16:52:26.136156+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/tail -f /var/log/auth. log 



<!-- Start of picture text -->
labuser@ubuntu-lab:~s sudo grep "Failed Password" /var/log/auth.log<br>2026-08-11710:54:32.023209+00:00 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PHD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth.<br>log<br>labuser@ubuntu-lab:“$<br><!-- End of picture text -->



<!-- Start of picture text -->
labuser@ubuntu-lab:“$ sudo grep "Accepted Password" /var/log/auth. log<br>2626-08-117T10:55:31.540938+00:00 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Accepted Password /var/log/aut<br>Ih. log<br>Jabuser@ubuntu-lab:"$<br><!-- End of picture text -->



<!-- Start of picture text -->
labuser@ubuntu-lab:“$ sudo cat /var/log/syslog | head -20<br>2026-08-09708:68:43.079850+00:00 ubuntu-lab systemd[1]: Queued start job for default target graphical.target.<br>2026-@8-09T08:08:43.080217+00:00 ubuntu-lab kernel: Linux version 7.@.0-14-generic (buildd@lcy@2-amd64-043) (x86_64-linux-gnu-gcec (Ubuntu 15.2.@-16ubuntu1) 15.2<br>.@, GNU ld (GNU Binutils for Ubuntu) 2.46) #14-Ubuntu SMP PREEMPT_DYNAMIC Mon Apr 13 11:09:53 UTC 2026 (Ubuntu 7.0.0-14.14-generic 7.0.0)<br>2026-98-99T08:08:43.080709+00:00 ubuntu-lab kernel: Command line: BOOT_IMAGE=/vmlinuz-7.0.0-14-generic root=/dev/mapper/ubuntu--vg-ubuntu--ly ro crashkerne1l=2G-<br>4G:2026320M, -@8-69T08:08:43.080722+00:064G-32G:512M , 32G-64G: 1024M ubuntu-lab,64G-128G:2048M,kernel:128G-:4096MKERNEL supported cpus:<br>2026-@8-09T08:08:43.080723+00:00 ubuntu-lab kernel: Intel GenuineIntel<br>2026-08-09T88:08:43.080723+00:00 ubuntu-lab kernel: AMD Authent icAMD<br>2026-08-09708:08:43.080723+00:00 ubuntu-lab kernel: Hygon HygonGenuine<br>2626 -68-09T88 :68:43.080724+00:00 ubuntu-lab kernel: Centaur CentaurHauls<br>2626 -@8-69T08:08:43.080724+00:06 ubuntu-lab kernel: zhaoxin Shanghai<br>2026-98-09T08:68:43.680726+00:00 ubuntu-lab kernel: BIOS-provided physical RAM map:<br>2026 -08-09708:08:43.080727+00:00 ubuntu-lab kernel: BIOS-e820: [mem 0xeoQ00G0000000000-0xoR0000000009fbff] System RAM<br>2026-08-09708:08:43.080727+00:00 ubuntu-lab kernel: BIOS-e820: [mem OxeeQQeQ0G0009fCO0-OxeR000R000009TTTT] device reserved<br>2026-@8-09T08:08:43.080727+00:00 ubuntu-lab kernel: BIOS-e820: [gap exeaaeooeeeeeagead -oxa00R0000G00eF fff]<br>2026-08-09T08:08:43.080728+00:00 ubuntu-lab kernel: BIOS-e820: [mem OxeoQQQQ0R000f G000-oxe0000000000f fff] device reserved<br>2026-@8-69T68:08:43.086728+00:00 ubuntu-lab kernel: BIOS-e820: [mem @xeoogg09000190000-ox000000007ffeffff] System RAM<br>2026-08-09T08:08:43.080730+00:00 ubuntu-lab kernel: BIOS-e820: [mem Oxeo0000007f ffo000-oxG00000007fffffff] ACPI data<br>2026-08-69T08:08:43.080730+00:00 ubuntu-lab kernel: BIOS-e820: [gap 9xea9eeQ9G980000000-OxG0000000febf fff]<br>2026-08-09708:08:43.080731+00:00 ubuntu-lab kernel: BIOS-e820: [mem OxeeQQoR0ef eceg000-oxeQ000000feCeefff] device reserved<br>2026-@8-09708:08:43.080731+00:00 ubuntu-lab kernel: BIOS-e820: [gap exeeo99eeefece1000-oxE0000000fedt ffff]<br>2626 -68-09T88 :68:43.080731+00:60 ubuntu-lab kernel: BIOS-e826: [mem oxeog90G00f eedG900-GxEG000000feeOOTff] device reserved<br>Jabuser@ubuntu-lab:"$<br><!-- End of picture text -->



<!-- Start of picture text -->
Aug 11 10:55:31 ubuntu-lab systemd[1]: Finished update-notifier-download.service - Download data for packages that failed at package install time.<br>Aug 11 10:56:00 ubuntu-lab systemd-resolved[850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 10:56:09 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>hug 11 16:56:12 ubuntu-lab systemd-resolved [850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 10:56:19 ubuntu-lab systemd[1589]: launchpadlib-cache-clean.service - Clean up old files in the Launchpadlib cache skipped, unmet condition check Condity<br>Aug 11 10:56:21 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>Aug 11 10:56:25 ubuntu-lab systemd-resolved[850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 16:56:28 ubuntu-lab sudo[1751]: pam_unix(sudo:session): session opened for user root(uid=@) by labuser(uid=1000)<br>Aug 11 10:56:28 ubuntu-lab sudo[1751]: labuser : TTY=/dev/tty1 ; PHD=/home/labuser ; USER=root ; COMMAND=/usr/bin/cat /var/log/sys. log<br>Aug 11 10:56:28 ubuntu-lab sudo[1751]: pam_unix(sudo:session): session closed for user root<br>Aug 11 16:56:34 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>Aug 11 10:56:37 ubuntu-lab systemd-resolved [850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 16:56:46 ubuntu-lab systemd-resolved [850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>Aug 11 10:56:49 ubuntu-lab systemd-resolved[850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 10:56:53 ubuntu-lab sudo[1766]: pam_unix(sudo:session): session opened for user root(uid=0) by labuser(uid=1000)<br>Aug 11 10:56:53 ubuntu-lab sudo[1766]: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/cat /var/log/sys. log<br>Aug 11 10:56:53 ubuntu-lab sudo[1766]: pam_unix(sudo:session): session closed for user root<br>Aug 11 10:56:58 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>hug 11 16:57:01 ubuntu-lab systemd-resolved [850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 10:57:06 ubuntu-lab sudo[1781]: pam_unix(sudo:session): session opened for user root(uid=0) by labuser(uid=1000)<br>Aug 11 10:57:06 ubuntu-lab sudo[1781]): labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/cat /var/log/sys. log<br>Aug 11 10:57:66 ubuntu-lab sudo[1781]: pam_unix(sudo:session): session closed for user root<br>Aug 11 10:57:11 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>Aug 11 10:57:14 ubuntu-lab systemd-resolved [850]: Using degraded feature set TCP instead of UDP for DNS server 172.16.0.1.<br>Aug 11 10:57:23 ubuntu-lab systemd-resolved[850]: Using degraded feature set UDP instead of TCP for DNS server 172.16.0.1.<br>Aug 11 10:57:43 ubuntu-lab sudo[1806]: pam_unix(sudo:session): session opened for user root(uid=@) by labuser(uid=1000)<br>Aug 11 16:57:43 ubuntu-lab sudo[1806]: labuser : TTy=/dev/tty1 ; PHD=/home/labuser ; USER=root ; COMMAND=/usr/bin/cat /var/log/syslog<br>Aug 11 10:57:43 ubuntu-lab sudo [1806]: pam_unix(sudo:session): session closed for user root<br>Aug 11 10:58:15 ubuntu-lab sudo[1820]: pam_unix(sudo:session): session opened for user root(uid=0) by labuser(uid=1000)<br>Aug 11 16:58:15 ubuntu-lab sudo[1820]: labuser : TTY=/dev/tty1 ; PHD=/home/labuser ; USER=root ; COMMAND=/usr/bin/journalctl -xe<br>labuser@ubuntu-lab:~$ “C<br>Jabuser@ubuntu-lab:“$ “C<br>abuser @ubuntu-lab:~$<br><!-- End of picture text -->

This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])? yes Warning: Permanently added '172.16.0.100' (ED25519) to the List of known hosts. Labuser@172.16.0.100's password: Welcome to Ubuntu 26.04 LTS (GNU/Linux 7.0.0-14-generic x86_64) * Documentation: https://docs.ubuntu.com * Management: https: //Landscape.canonical.com * Support: https: //ubuntu.com/pro System information as of Tue Aug 11 11:03:01 AM UTC 2026 System load: 0.08 Processes: 122 Usage of /: 46.1% of 9.75GB Users Logged in: (0) Memory usage: 14% IPv4 address for enp@s3: 172.16.0.100 Swap usage: 0% Expanded Security Maintenance for Applications is not enabled. © updates can be applied immediately. Enable ESM Apps to receive additional future security updates. See https://ubuntu.com/esm or run: sudo pro status :~$| = 4:34 PM =Qsp_Uuegas ~ &@ CYS grir026 

abuser@ubuntu-lab:~$ sudo tail -f /var/log/auth.loglog 2026-08-11710:58:15.108239+00:68 ubuntu-lab sudo: pam_unix(sudo:session): session opened for user root(uid=6) by labuser(uid=1000) 2026-08-11710:58:15.108488+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/journalctl -xe 2026-08-11710:58:23.267574+00:60 ubuntu-lab sudo: pam_unix(sudo:session): session closed for user root 2026-@8-11711:01:53.940919+00:00 ubuntu-lab sshd[1856]: Server listening on 9.6.0.0 port 22. 2026-08-11711:01:53.9472639+00:60 ubuntu-lab sshd[1856]: Server listening on :: port 22. 2026-@8-117T11:09:01.321923+00:08 ubuntu-lab sshd-session[1859]: Accepted password for labuser from 172.16.0.50 port 49674 ssh2 2026-@8-11711:09:01.3336539+00:80 ubuntu-lab sshd-session[1859]: pam_unix(sshd:session): session opened for user labuser(uid=1000) by labuser (uid=0) 2026-08-11711:03:01.437848+00:00 ubuntu-lab systemd-logind[1258]: New session '3' of user ‘labuser' with class ‘user' and type ‘tty’. 2026-@8-117T11:05:00.373528+00:00 ubuntu-lab sudo: pam_unix(sudo:session): session opened for user root(uid=0) by labuser(uid=1000) 2026-08-11711:05:00.384927+00:00 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/tail -f /var/log/auth. log 



<!-- Start of picture text -->
abuser@ubuntu-lab:~$ sudo tail -f /var/log/auth.loglog<br>2026-08-11710:58:15.108239+00:68 ubuntu-lab sudo: pam_unix(sudo:session): session opened for user root(uid=6) by labuser(uid=1000)<br>2026-08-11710:58:15.108488+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/journalctl -xe<br>2026-08-11710:58:23.267574+00:60 ubuntu-lab sudo: pam_unix(sudo:session): session closed for user root<br>2026-@8-11711:01:53.940919+00:00 ubuntu-lab sshd[1856]: Server listening on 9.6.0.0 port 22.<br>2026-08-11711:01:53.9472639+00:60 ubuntu-lab sshd[1856]: Server listening on :: port 22.<br>2026-@8-117T11:09:01.321923+00:08 ubuntu-lab sshd-session[1859]: Accepted password for labuser from 172.16.0.50 port 49674 ssh2<br>2026-@8-11711:09:01.3336539+00:80 ubuntu-lab sshd-session[1859]: pam_unix(sshd:session): session opened for user labuser(uid=1000) by labuser (uid=0)<br>2026-08-11711:03:01.437848+00:00 ubuntu-lab systemd-logind[1258]: New session '3' of user ‘labuser' with class ‘user' and type ‘tty’.<br>2026-@8-117T11:05:00.373528+00:00 ubuntu-lab sudo: pam_unix(sudo:session): session opened for user root(uid=0) by labuser(uid=1000)<br>2026-08-11711:05:00.384927+00:00 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/tail -f /var/log/auth. log<br><!-- End of picture text -->



<!-- Start of picture text -->
2026 -@8-11T11:06:47.907710+00:08 ubuntu-lab systemd-logind[1258]: Session 3 logged out. Waiting for processes to exit.<br>2626-@8-117T11:06:47.919671+00:00 ubuntu-lab systemd-logind[1258]: Removed session 3.<br>2626-@8-11711:07:12.116737+00:00 ubuntu-lab unix_chkpwd [2068]: password check failed for user (labuser)<br>2026-@8-11711:07:12.117585+00:08 ubuntu-lab sshd-session[2006]: pam_unix(sshd:auth): authentication failure; logname= uid=@ euid=6 tty=ssh ruser= rhost=172.16.0<br>-5@  user=labuser<br>2026-@8-117T11:07:13.761289+00:00 ubuntu-lab sshd-session[20@6]: Failed password for labuser from 172.16.@.56 port 55591 ssh2<br><!-- End of picture text -->

## :~$ exit 

Logopt Connection to 172.16.0.100 closed. 

C:\Users\john.doe>ssh Labuser@172.16.0.100 Labuser@172.16.0.100's password: Permission denied, please try again. Labuser@172.16.0.100's password: . allP| Q La -= © 3s | > A ®& & »» **)** oa 8/11/20264:37 PM 



<!-- Start of picture text -->
| labuser@ubuntu-lab:~ x aS |S - 0 x<br>labuser@172.16.0.100's password:<br>Permission denied, please try again.<br>Labuser@172.16.0.100's password:<br>Welcome to Ubuntu 26.04 LTS (GNU/Linux 7.0.0-14-generic x86_64)<br>* Documentation: https://docs.ubuntu.com<br>* Management: https: //landscape.canonical.com<br>* Support: https: //ubuntu.com/pro<br>System information as of Tue Aug 11 11:08:22 AM UTC 2026<br>System load: 0.08 Processes: 130<br>Usage of /: 46.2% of 9.75GB Users logged in: (c}<br>Memory usage: 14% IPv4 address for enp0s3: 172.16.0.100<br>Swap usage: 0%<br>Expanded Security Maintenance for Applications is not enabled.<br>® updates can be applied immediately.<br>Enable ESM Apps to receive additional future security updates.<br>See https://ubuntu.com/esm or run: sudo pro status<br>r<br>Last login: Tue Aug 11 11:03:03 2026 from 172.16.0.50<br>ng |<br>=aQuBZe@Ca= = ~ 8 CMS grinors4:38 PM<br><!-- End of picture text -->

298 User=labuser 2026-08-11T11:07:13.761289+00:00 ubuntu-lab sshd-session[2006]: Failed password for labuser from 172.16.0.5@ port 55591 ssh2 2626-68-117T11:08:22.149921+06:68 ubuntu-lab sshd-session[2@06]: Accepted password for labuser from 172.16.6.5@ port 55591 ssh2 2026-98-11T11:08:22.163017+00:00 ubuntu-lab sshd-session[2006]: pam_unix(sshd:session): session opened for user labuser(uid=1000) by labuser(uid=6) 2026-08-11711:08:22.188922+06:66 ubuntu-lab systemd-logind[1258]: New session '4' of user ‘labuser' with class ‘user' and type ‘tty’. 

labuser@ubuntu-lab:~$ sudo grep "Accepted Password" /var/log/auth.log 2026 -@8-11T10:55:31.540938+00:6@ ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Accepted Password /var/log/aut| lh. log 2026 -@8-11T11:09:47.559676+00:0@ ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Accepted Password /var/log/aut| Ih. log Jabuser@ubuntu-lab:"$ 

labuser@ubuntu-lab:~$ sudo grep "Failed Password" fvar/log/auth.log | awk ‘{print $113' | sort | uniq -c | sort -nr 

labuser@ubuntu-lab:~$ 

**Activity Command Purpose** Real-time authentication sudo tail -f Monitor authentication events monitoring /var/log/auth.log Detect unsuccessful Find failed logins grep "Failed password" authentication grep "Accepted Identify successful Find successful logins password" authentication cat /var/log/syslog | head View system logs Review system events -20 View systemd logs journalctl -xe Review systemd messages Count failed logins grep ... | awk ... Identify repeated source IPs 

# **SOC Analyst Perspective** 

This lab demonstrates a simplified version of what a **SOC Analyst** does during authentication monitoring. 

# **1. Collect** 

Authentication events are generated by the SSH service. 

# **2. Identify** 

The analyst searches for: 

Failed password 

and: 

Accepted password 

# **3. Analyze** 

The analyst examines: 

- Timestamp 

- Username 

- Source IP 

- Authentication result 

- Number of attempts 

# **4. Detect** 

Repeated failed authentication attempts from the same IP could warrant further investigation. 

# **5. Investigate** 

The analyst can determine whether the activity represents: 

Normal user behavior 

OR 

Potential unauthorized access 

OR 

Password-guessing activity 

# **Key Takeaways** 

# **Authentication Logs** 

/var/log/auth.log 

can provide valuable information about authentication-related activity. 

# **Failed Authentication** 

Failed password 

can be searched to identify unsuccessful login attempts. 

# **Successful Authentication** 

Accepted password 

can be searched to identify successful password authentication. 

# **Real-Time Monitoring** 

sudo tail -f /var/log/auth.log 

allows an analyst to observe new authentication events as they occur. 

# **Log Filtering** 

grep can be used to search logs for specific events. 

# **Log Processing** 

Commands such as: 

grep → awk → sort → uniq 

can transform raw logs into useful security information. 

# **Skills Demonstrated** 

- Linux Log Analysis 

- Authentication Monitoring 

- SSH Security Monitoring 

- Linux Command Line 

- grep 

- awk 

- sort 

- uniq 

- tail 

- journalctl 

- System Log Analysis 

- Failed Login Detection 

- Successful Login Verification 

- Source IP Analysis 

- Basic SOC Investigation 

- Security Event Monitoring 

# **Conclusion** 

This lab provided practical experience in analyzing Linux authentication and system logs. Failed and successful SSH login attempts were deliberately generated from the Windows client and then investigated from the Ubuntu system. 

The exercise demonstrated how a SOC analyst can use Linux command-line tools to **identify authentication events, monitor logs in real time, investigate failed login attempts, determine source IP addresses, and count repeated authentication failures** . 

This lab provides a useful foundation for progressing toward **SIEM-based log analysis and SOC alert investigation** , where similar authentication events can be collected centrally and correlated across multiple systems. 

