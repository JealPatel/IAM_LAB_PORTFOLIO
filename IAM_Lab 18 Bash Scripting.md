# **IAM Lab 18 — Linux Bash Scripting for Security Monitoring and Failed Login Analysis** 

# **Objective** 

The objective of this lab is to practice basic Linux Bash scripting for cybersecurity monitoring and automation using: 

- grep 

- awk 

- tail 

- sort 

- uniq 

- wc 

- uptime 

- free 

- df 

- ss 

- Bash variables and conditional statements 

The lab helps understand how Bash scripts can be used to automate security monitoring tasks such as: 

- Detecting failed login attempts 

- Identifying source IP addresses 

- Checking system health 

- Monitoring network connections 

- Generating basic security alerts 

# **Lab Environment** 

**Component Details** Ubuntu-Lab Ubuntu Linux Ubuntu User labuser Shell Bash Authentication Log /var/log/auth.log Script Editor Nano Main Purpose Linux Security Monitoring & Automation 

# **Step 0: Start the VM** 

# **Procedure** 

1. Started **Ubuntu-Lab** . 

2. Logged in using: 

Username: labuser 

Password: P@ssw0rd123 

3. Opened the terminal. 

# **Result** 

The Ubuntu-Lab virtual machine was successfully started and the terminal was ready for Bash scripting activities. 

# **Step 1: Script 1 – Check Failed Logins** 

# **1.1 Create the Script File** 

# **Command** 

nano check_failed_logins.sh 

# **Purpose** 

The nano command opens the Nano text editor and creates a new Bash script named: 

check_failed_logins.sh 

This script will be used to identify the most recent failed login attempts recorded in the authentication log. 

# **1.2 Write the Script** 

Enter the following script: 

#!/bin/bash 

# ============================================ 

# SCRIPT: check_failed_logins.sh 

# AUTHOR: Jeal Patel 

# DATE: August 2026 

# PURPOSE: Show the last 10 failed login attempts 

# ============================================ 

echo "==========================================" 

echo "     FAILED LOGIN REPORT" 

echo "==========================================" echo "" echo "The last 10 failed login attempts:" echo "" 

sudo grep "Failed password" /var/log/auth.log | tail -10 

echo "" echo "==========================================" echo "     END OF REPORT" echo "==========================================" 



<!-- Start of picture text -->
GNU nano o.7.1<br>#!“bin-bash<br>|: fanhelanatalananenhaanintantenantanian antenatal asiaaienbasiaetantantaatantantataatanasiastae beatae<br>e#AUthor: Jeal Patel<br>A@Script: For checking failed logins<br>|: fanhelanatalananenhaanintantenantanian antenatal asiaaienbasiaetantantaatantantataatanasiastae beatae<br>“failed Login report"<br>"The Last 16 Failed Login Report<br>sudo "Failed Password" /var/log/auth.log -16<br><!-- End of picture text -->

labuser@ubuntu-lab:"$ chmod +*% check_tailed_logins.sh labuser@ubuntu-lab:"$ ls -lh total 8.4K -puxruee1 labuser labuser 326 Aug 14 66:25 -Puxr-epL labuser labuser A Aug 18 88:38 druxruxe-* 2@ labuser labuser 4.8K Aug 16 98:23 labuser@ubuntu-lab:"$ 



<!-- Start of picture text -->
labuser@ubuntu-lab:~$ ./check_failed_logins.sh<br><!-- End of picture text -->

failed Login report 

The Last 10 Failed Login Report 2026-@8-11710:54:32.023209+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 2026-08-11T11:10:30.916302+00:6@ ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 2026-@8-117T11:12:48.028454+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 2026-@8-11T11:13:07.3439435+00:08 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 2026-@8-117T11:14:09.570683+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. 2026 -68-117T11:15:58.569316+00:6@ ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 2026-@8-14706:30:59.157880+00:60 ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. 2026 -68-14706:33:60.653775+00:6@ ubuntu-lab sudo: labuser : TTY=/dev/tty1 ; PWD=/home/labuser ; USER=root ; COMMAND=/usr/bin/grep Failed Password /var/log/auth. log 

Jabuser@ubuntu-lab:~$ 

# **Step 2: Script 2 – Count Failed Logins by IP** 

# **2.1 Create the Script File** 

# **Command** 

nano count_failed_by_ip.sh 

# **Purpose** 

This script analyzes failed authentication attempts and counts how many attempts originated from each IP address. 

# **2.2 Write the Script** 

Enter: 

#!/bin/bash 

# ============================================ 

# SCRIPT: count_failed_by_ip.sh 

# AUTHOR: Jeal Patel 

# DATE: August 2026 



<!-- Start of picture text -->
# PURPOSE: Count failed login attempts by IP address<br><!-- End of picture text -->

# ============================================ 

echo "==========================================" 

echo "     FAILED LOGINS BY IP" echo "==========================================" echo "" echo " IP Address       |  Attempts" echo "------------------------------------------" 

sudo grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr 

echo "==========================================" echo "     END OF REPORT" 

echo "==========================================" 



<!-- Start of picture text -->
GNU nano 8.7.4 count _failed_oy_ip.sh<br>#! bin/bash<br>o<br>"The failed Ip Attemots"<br>“TF Attempts"<br><!-- End of picture text -->

labuser@ubuntu-lap:"$ chmod +x count_tailed_by_ip.sh labuser@ubuntu-lab:“ 1s - lh total 12k -ruxruxe-* 1 labuser labuser 336 Aug 14 66:32 check_tailed_logins.sh -puxruxe1 labuser labuser 361 Aug 14 @6:38 count_tailed_by_ip.sh -ruxer-xe-s 1 labuser labuser @ Aug 16 68:38 mytile.txt drwxruse-x 2¢ labpuser labuser 4.8K Aug 1a 68:25 labuser@ubuntu-lab:"$ 

abuser@ubuntu-lab:"s .#count_failed_by_ip.sh he tailed Ip Attempts IP | Attempts 

(sudo: authenticate] Password: NO OF REPORT 

abuser@ubuntu- lab: 

↓ 

Display results 

# **Command Breakdown** 

# **Command Purpose** 

grep Finds failed password events awk Extracts a specific field from the log sort Sorts IP addresses uniq -c Counts repeated IP addresses sort -nr Sorts counts from highest to lowest 

# **Security Relevance** 

If a particular IP address appears repeatedly, it may indicate: 

Multiple Failed Logins 

↓ 

Same Source IP 

↓ 

Possible Password Guessing 

↓ 

Investigate Source 

↓ 

Potential Brute-Force Activity 

# **Result** 

The failed login events were processed and grouped according to their source IP addresses. 

# **Step 3: Script 3 – Check System Status** 

# **3.1 Create the Script File** 

# **Command** 

nano system_health.sh 

# **Purpose** 

The purpose of this script is to perform a quick health check of the Ubuntu system. 

It collects information about: 

- System uptime 

- Memory usage 

- Disk usage 

- Active/listening network connections 

# **3.2 Write the Script** 

Enter: #!/bin/bash 

# ============================================ 

# SCRIPT: system_health.sh 

# AUTHOR: Jeal Patel # DATE: August 2026 # PURPOSE: Quick system health check 

# ============================================ 

echo "==========================================" 

echo "     SYSTEM HEALTH CHECK" echo "==========================================" echo "" 

echo "1. Uptime:" uptime echo "" 

echo "2. Memory Usage:" free -h echo "" 

echo "3. Disk Usage:" df -h echo "" 



<!-- Start of picture text -->
GNU nano 6.7.1 system_health.sh<br>Fl bin¢bash<br>HDATE: 14/08/2026<br>"1. Upt ime"<br>Jot ime<br>"2.Memory Usage"<br>free -h<br>"3. Disk Usage"<br>1f -h<br>“4 Active Connections"<br>BS -tulon - ie<br><!-- End of picture text -->



<!-- Start of picture text -->
labuser@ubuntu-lab:"s chmod +* system_nealth.sh<br>labuser@ubuntu-lab:"$ ls -1h<br>total 16k<br>-ruspuxe-x 1 labuser labuser 336 Aug 14 @6:32 check_failed_logins.sh<br>-ruxpuxe-x 1 labuser labuser 363 Aug 14 @7:26 count_failed_by_ip.sh<br>-Ppuxp-xP-x 1 labuser labuser @ Aug 1@ @8:3@ myfile.txt<br>drwxrwer-* 2 labuser labuser 4.4K Aug 18 8:23<br>-ruxpuxe-x 1 labuser labuser 539 Aug 14 @?:32 system_nealth.sn<br>labuser@ubuntu-lab: "$lab: "$<br><!-- End of picture text -->

labuser@ubuntu-lab:"s chmod +* system_nealth.sh labuser@ubuntu-lab:"$ ls -1h total 16k -ruspuxe-x 1 labuser labuser 336 Aug 14 @6:32 check_failed_logins.sh -ruxpuxe-x 1 labuser labuser 363 Aug 14 @7:26 count_failed_by_ip.sh -Ppuxp-xP-x 1 labuser labuser @ Aug 1@ @8:3@ myfile.txt drwxrwer-* 2 labuser labuser 4.4K Aug 18 8:23 -ruxpuxe-x 1 labuser labuser 539 Aug 14 @?:32 system_nealth.sn labuser@ubuntu-lab: "$lab: "$ 



<!-- Start of picture text -->
abuser@ubuntu-lab:"s ./system_health.sh<br>Sytem Health Checkup<br>1 Uptime<br>O7:ad:28 up 1:46, 1 user, load average: 4.98, 6.95, 9.98<br>F.Memory Usage<br>total used free shared buff/cache available<br>Mem: 1.664 68M i 1.661 1.4Mi SB AML 1.261<br>Swap: 1.8Gi 8B 1.8Gi<br>5. Disk Usage<br>ilesystem Size Used Avail Use# Mounted on<br>Ydeyv/smapper/ubuntu--ve-ubuntu--ly 9.86 4.76 4.76 S18 ¢<br>tmpot s B22M 6 822M 6% /deyv/shm<br>tpt = 622H 8.8K 822M 1% “tmp<br>Ydev/sdae 1.6G 96M 1.66 6% “boot<br>none 1.9M 6 1.64 4% frun‘credentials/gettya@ttyl.service<br>tmpot s 165M 6.8 165M 18 fruneuser/ 1886<br>none 1.6M 6 1.04 6% /runécredentials/systemd-networkd.service<br>none 1.64 6 1.04 8% /run¢credentials/systemd-resolved.service<br>none 1.8M 6 1.64 4% frun/’credentials/systemd- journald.service<br>4.Active Connections<br>Netid State Recv-QO Send-@ Local Address:Port Peer Address:PortProcess<br>udp  UNCONN @ a 127.8.8.54:593 8.8,.8.0r%<br>udp  UNCONN @ a 127.6.6,59%lo:53 8.0,0,0:%<br>udp UNCONN @ a 127.8.6.1:923 8.8.8.0r%<br>Udo UNCONN & a [::1] 1523 [ii] i#<br>tco =LISTEN @ 4096 «6 127.6.8.59%1o0:53 8.8.8.0r%<br>tcp LISTEN @ 4696 0.0.0.0:22 O,8,0.0:%<br>tco =©9LISTEN & 4096 127.6.4.54:53 8.8.8.8r%<br>tcp = =©9LISTEN @ 4096 [::] 122 [ii] ix<br>nd oof Report<br>abuserdubuotiy- lah: s<br><!-- End of picture text -->

# **3. Disk Usage** 

Command: 

df -h 

This displays disk-space usage for the filesystem. 

It can help identify whether a system is running low on available disk space. 

# **4. Active Connections** 

Command: 

ss -tulpn | head -10 

This displays network sockets and listening services. 

Options: 

# **Option Meaning** 

- -t TCP 

- -u UDP 

- -l Listening 

- -p Show process 

- -n Display numerical addresses/ports 

head -10 limits the displayed output to the first 10 lines. 

# **Result** 

The system health script was successfully created and used to collect basic information about uptime, memory, disk usage, and network connections. 

# **Step 4: Script 4 – Failed Login Alert** 

# **4.1 Create the Script File** 

# **Command** 

nano alert_failed_logins.sh 

# **Purpose** 

The purpose of this script is to detect a high number of failed login attempts and generate an alert when the configured threshold is exceeded. 

This introduces the concept of basic automated security detection. 

# **4.2 Write the Script** 

Enter: 

#!/bin/bash 

# ============================================ 

# SCRIPT: alert_failed_logins.sh 

# AUTHOR: Jeal Patel # DATE: August 2026 

# PURPOSE: Alert if there are more than 10 failed logins 

# ============================================ 

# # Count failed logins 

FAILED_COUNT=$(sudo grep "Failed password" /var/log/auth.log | tail -100 | wc -l) 

echo "Failed logins in the last 100 attempts: $FAILED_COUNT" 

if [ $FAILED_COUNT -gt 10 ]; then 

echo " ALERT: High number of failed login attempts detected!" echo "Please investigate immediately." else 

echo " No unusual activity detected." fi 

alert_tailed_logins 

GNU nano 8.7.1 

#!bin“bash 

#Author:Patel Jeal #Date: 14/88/2026 #Purpose: Alert if there are more than 16 failed logins in the last hour FAILEO_COUNT=$"Failed Logins:{sudo $FATLED_COUNT'"Failed Password" /var/log/auth.log -1ea | we -1 

ie “Alert:High Number of failed logins Detected!" "Please investigate immediately." 

"Mo unusual activity." 



<!-- Start of picture text -->
labuser@ubuntu-lab:"$ chmod +x alert_tailed_logins.sh<br>labuser@ubuntu-lab:“$ ls -1h<br>rotal Zak<br>ruxruxe-* 1 labuser labuser 487 Aug 14 @7?:41 alert_tailed_logins.sh<br>ruxruge-% 1 labuser labuser 336 Aug 14 @6:32 check_tailed_logins.sh<br>ruxruee-* 1 labuser labuser 363 Aug 14 @f:26 count ftailed_by_ip.sh ftailed_by_ip.sh<br>ruxr-xe- 1 labuser labuser @ Aug 16 66:98 myftile.txt<br>Iruxruse-* 2 labuser labuser 4.6K Aug 16 88:23<br>PuxkPuxe-* 1 lapuser labuser S39 Aug 14 @7:32 system_health.sh<br>lah eermuhuatiu- Lah:<br><!-- End of picture text -->

labuser@ubuntu-lab:"$ chmod +x alert_tailed_logins.sh labuser@ubuntu-lab:“$ ls -1h 

rotal Zak ruxruxe-* 1 labuser labuser 487 Aug 14 @7?:41 alert_tailed_logins.sh ruxruge-% 1 labuser labuser 336 Aug 14 @6:32 check_tailed_logins.sh ruxruee-* 1 labuser labuser 363 Aug 14 @f:26 count ftailed_by_ip.sh ftailed_by_ip.sh ruxr-xe1 labuser labuser @ Aug 16 66:98 myftile.txt Iruxruse-* 2 labuser labuser 4.6K Aug 16 88:23 PuxkPuxe-* 1 lapuser labuser S39 Aug 14 @7:32 system_health.sh lah eermuhuatiu- Lah: 



<!-- Start of picture text -->
labuser@ubuntu-lab:"# ./alert_tailed_logins.sh<br>[sudo: authenticate] Password:<br>Failed Logins: 13<br>Alert:High Number of failed logins Detected!<br>Please investigate immediately.<br>labuser@ubuntu-lab:lab: $<br><!-- End of picture text -->

labuser@ubuntu-lab:"# ./alert_tailed_logins.sh [sudo: authenticate] Password: Failed Logins: 13 Alert:High Number of failed logins Detected! Please investigate immediately. labuser@ubuntu-lab:lab: $ 

# **What the Alert Script Does** 

The following command counts matching failed-login entries: 

FAILED_COUNT=$(sudo grep "Failed password" /var/log/auth.log | tail -100 | wc -l) The result is stored in the variable: 

FAILED_COUNT 

The script then checks: 

if [ $FAILED_COUNT -gt 10 ]; then 

Here: 

# **Element** 

# **Meaning** 

if Starts a condition 

$FAILED_COUNT Number of failed login events 

-gt Greater than 10 Alert threshold 

Therefore: 

Failed Login Count 

↓ 

Is count > 10? 

↓ ┴ ┌─── ───┐ YES      NO ↓        ↓ 

ALERT    Normal 

# **Important Note** 

The script currently checks the **last 100 matching failed-login records** , not strictly the failed logins that occurred within the last hour. 

Therefore, the output: 

Failed logins in the last 100 attempts 

is more accurate than describing it as: 

Failed logins in the last hour 

A true one-hour detection would require filtering log entries according to their timestamps. 

# **Result** 

The script successfully demonstrates basic threshold-based security alerting using Bash conditional logic. 

# **Troubleshooting Flow** 

This lab can be remembered as a simple security-monitoring workflow: 

1. Identify Failed Login Events 

- ↓ 

grep "Failed password" /var/log/auth.log 

# 2. View Recent Events 

↓ 

tail -10 

3. Identify Source IPs 

- ↓ 

awk + sort + uniq 

# 4. Check System Health 

↓ 

uptime + free + df 

# 5. Check Network Services 

↓ 

ss -tulpn 

# 6. Generate Security Alert 

↓ 

if condition 

# **Easy Memory Trick** 

Think: 

# **Find → Filter → Count → Check → Alert** 

or: 

"Find suspicious events → identify their source → measure their frequency → check the system → generate an alert." 

This is a useful foundation for SOC monitoring. 

# **Expected Results Summary** 

# **Test / Script Expected Result** 

# **What It Proves** 

check_failed_logins.sh Failed login entries displayed 

count_failed_by_ip.sh IP addresses and counts displayed Uptime, RAM, disk and connections system_health.sh displayed alert_failed_logins.sh Alert or normal-activity message chmod +x Script becomes executable grep Matching log events found awk Required field extracted sort + uniq Repeated IPs counted wc -l Number of matching events counted ss -tulpn Listening sockets displayed 

Authentication log analysis Source IP analysis 

System health monitoring 

Basic security detection Linux permissions Log filtering Log parsing Event aggregation Event counting Network exposure analysis 

# **Cybersecurity Relevance** 

# This lab is directly useful for basic **SOC operations, Linux security monitoring, incident detection, and Blue Team activities** . 

A SOC analyst can use similar concepts to investigate questions such as: 

- Are there failed login attempts on the system? 

- How frequently are authentication failures occurring? 

- Which IP addresses are generating failed login attempts? 

- Could repeated attempts indicate a brute-force attack? 

- Is the system experiencing unusual resource usage? 

- Which network services are currently listening? 

- Can repetitive security-monitoring tasks be automated? 

- Can a threshold be used to generate an initial security alert? 

For example: 

Ubuntu-Lab 

│ 

├── /var/log/auth.log 

│        ↓ 

│   Failed Login Events 

│        ↓ 

│   grep + awk │        ↓ 

│   Source IP Analysis 

│        ↓ 

│   sort + uniq │        ↓ 

│   Count Attempts │        ↓ 

│   Threshold Check 

│        ↓ └── Security Alert 

This basic workflow demonstrates the same general concept used in larger securitymonitoring environments: 

Log Collection 

↓ 

Log Filtering 

↓ 

Event Analysis 

- ↓ 

Detection Logic 

- ↓ 

Alert 

- ↓ 

Investigation 

# **Practical Learning Outcomes** 

After completing this lab, the following concepts were practiced: 

1. Creating Bash scripts using Nano. 

2. Understanding the Bash shebang #!/bin/bash. 

3. Assigning execute permissions using chmod +x. 

4. Running scripts using ./script.sh. 

5. Searching Linux authentication logs using grep. 

6. Extracting log fields using awk. 

7. Counting repeated events using uniq -c. 

8. Sorting security events using sort. 

9. Counting log entries using wc -l. 

- 10.Checking Linux system health using standard commands. 

- 11.Checking network sockets using ss. 

- 12.Using Bash variables. 

- 13.Using conditional statements for basic detection. 

- 14.Understanding how scripting can automate SOC monitoring tasks. 

**Conclusion** 

This lab provided practical experience in using Bash scripting for Linux security monitoring and basic automation. 

The first script demonstrated how failed authentication attempts can be identified from Linux authentication logs. The second script extended this analysis by grouping failed attempts according to source IP address. The third script demonstrated how Bash can collect important system-health and network information. Finally, the fourth script introduced threshold-based alerting for potentially suspicious login activity. 

The practical demonstrates an important cybersecurity concept: 

Linux Logs 

↓ 

Bash Commands 

↓ 

Event Analysis 

↓ 

Detection Logic 

↓ 

Security Alert 

These scripting skills provide a strong foundation for further learning in **SOC operations, SIEM, incident response, Linux security, log analysis, and Blue Team cybersecurity** . 

