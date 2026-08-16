**IAM Lab 18 — Linux Bash Scripting for Security Monitoring and Failed Login Analysis**

**Objective**

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

**Lab Environment**

| **Component** | **Details** |
|--------------------|----------------------------------------|
| Ubuntu-Lab | Ubuntu Linux |
| Ubuntu User | labuser |
| Shell | Bash |
| Authentication Log | /var/log/auth.log |
| Script Editor | Nano |
| Main Purpose | Linux Security Monitoring & Automation |

**Step 0: Start the VM**

**Procedure**

1. Started **Ubuntu-Lab**.

2. Logged in using:

Username: labuser

Password: P@ssw0rd123

3. Opened the terminal.

**Result**

The Ubuntu-Lab virtual machine was successfully started and the terminal was ready for Bash scripting activities.

**Step 1: Script 1 – Check Failed Logins**

**1.1 Create the Script File**

**Command**

nano check_failed_logins.sh

**Purpose**

The nano command opens the Nano text editor and creates a new Bash script named:

check_failed_logins.sh

This script will be used to identify the most recent failed login attempts recorded in the authentication log.

**1.2 Write the Script**

Enter the following script:

\#!/bin/bash

\# ============================================

\# SCRIPT: check_failed_logins.sh

\# AUTHOR: Jeal Patel

\# DATE: August 2026

\# PURPOSE: Show the last 10 failed login attempts

\# ============================================

echo "=========================================="

echo " FAILED LOGIN REPORT"

echo "=========================================="

echo ""

echo "The last 10 failed login attempts:"

echo ""

sudo grep "Failed password" /var/log/auth.log \| tail -10

echo ""

echo "=========================================="

echo " END OF REPORT"

echo "=========================================="

**What This Script Does**

The script:

1. Displays a report heading.

2. Reads /var/log/auth.log.

3. Searches for the phrase:

Failed password

4. Uses tail -10 to display the last 10 matching events.

5. Displays an ending message.

**1.3 Save the Script**

In Nano:

| **Key** | **Action** |
|----------|-------------------|
| Ctrl + X | Exit Nano |
| Y | Confirm saving |
| Enter | Keep the filename |

**1.4 Make the Script Executable**

**Command**

chmod +x check_failed_logins.sh

**Purpose**

The chmod +x command adds execute permission to the script.

Without executable permission, the script cannot normally be launched using:

./check_failed_logins.sh

**1.5 Run the Script**

**Command**

./check_failed_logins.sh

**Expected Output**

You may see output similar to:

==========================================

FAILED LOGIN REPORT

==========================================

The last 10 failed login attempts:

Aug 13 10:05:23 ubuntu-lab sshd\[5678\]: Failed password for labuser from 172.16.0.50 port 54323 ssh2

Aug 13 10:05:34 ubuntu-lab sshd\[5679\]: Failed password for labuser from 172.16.0.50 port 54324 ssh2

==========================================

END OF REPORT

==========================================

**What It Means**

The command:

sudo grep "Failed password" /var/log/auth.log \| tail -10

performs two main operations.

| **Command** | **Purpose** |
|-------------|------------------------------------------------------------|
| grep | Searches the authentication log for failed password events |
| tail -10 | Displays the last 10 matching events |
| sudo | Provides elevated permission to read the log if required |

**Security Relevance**

Failed authentication attempts may indicate:

- Incorrect passwords

- Password guessing

- Brute-force attacks

- Unauthorized access attempts

- Suspicious SSH activity

**Result**

The script was created, made executable, and used to search the authentication log for recent failed login attempts.

**Step 2: Script 2 – Count Failed Logins by IP**

**2.1 Create the Script File**

**Command**

nano count_failed_by_ip.sh

**Purpose**

This script analyzes failed authentication attempts and counts how many attempts originated from each IP address.

**2.2 Write the Script**

Enter:

\#!/bin/bash

\# ============================================

\# SCRIPT: count_failed_by_ip.sh

\# AUTHOR: Jeal Patel

\# DATE: August 2026

\# PURPOSE: Count failed login attempts by IP address

\# ============================================

echo "=========================================="

echo " FAILED LOGINS BY IP"

echo "=========================================="

echo ""

echo " IP Address \| Attempts"

echo "------------------------------------------"

sudo grep "Failed password" /var/log/auth.log \| awk '{print \$11}' \| sort \| uniq -c \| sort -nr

echo "=========================================="

echo " END OF REPORT"

echo "=========================================="

**2.3 Save the Script**

Use:

Ctrl + X

Y

Enter

**2.4 Make the Script Executable**

**Command**

chmod +x count_failed_by_ip.sh

**2.5 Run the Script**

**Command**

./count_failed_by_ip.sh

**Expected Output**

==========================================

FAILED LOGINS BY IP

==========================================

IP Address \| Attempts

------------------------------------------

4 172.16.0.50

1 192.168.1.100

==========================================

END OF REPORT

==========================================

The exact results depend on the authentication events present on the Ubuntu system.

**What the Command Does**

The main command is:

sudo grep "Failed password" /var/log/auth.log \| awk '{print \$11}' \| sort \| uniq -c \| sort -nr

The processing flow is:

Authentication Log

↓

grep "Failed password"

↓

Extract IP using awk

↓

sort

↓

Count duplicates using uniq -c

↓

sort by number

↓

Display results

**Command Breakdown**

| **Command** | **Purpose** |
|-------------|----------------------------------------|
| grep | Finds failed password events |
| awk | Extracts a specific field from the log |
| sort | Sorts IP addresses |
| uniq -c | Counts repeated IP addresses |
| sort -nr | Sorts counts from highest to lowest |

**Security Relevance**

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

**Result**

The failed login events were processed and grouped according to their source IP addresses.

**Step 3: Script 3 – Check System Status**

**3.1 Create the Script File**

**Command**

nano system_health.sh

**Purpose**

The purpose of this script is to perform a quick health check of the Ubuntu system.

It collects information about:

- System uptime

- Memory usage

- Disk usage

- Active/listening network connections

**3.2 Write the Script**

Enter:

\#!/bin/bash

\# ============================================

\# SCRIPT: system_health.sh

\# AUTHOR: Jeal Patel

\# DATE: August 2026

\# PURPOSE: Quick system health check

\# ============================================

echo "=========================================="

echo " SYSTEM HEALTH CHECK"

echo "=========================================="

echo ""

echo "1. Uptime:"

uptime

echo ""

echo "2. Memory Usage:"

free -h

echo ""

echo "3. Disk Usage:"

df -h

echo ""

echo "4. Active Connections:"

ss -tulpn \| head -10

echo ""

echo "=========================================="

echo " END OF REPORT"

echo "=========================================="

**3.3 Save, Make Executable and Run**

**Make Executable**

chmod +x system_health.sh

**Run**

./system_health.sh

**What the Script Checks**

**1. System Uptime**

Command:

uptime

This displays how long the system has been running and provides load information.

**2. Memory Usage**

Command:

free -h

The -h option displays memory values in a human-readable format.

It provides information about:

- Total memory

- Used memory

- Available memory

- Swap memory

**3. Disk Usage**

Command:

df -h

This displays disk-space usage for the filesystem.

It can help identify whether a system is running low on available disk space.

**4. Active Connections**

Command:

ss -tulpn \| head -10

This displays network sockets and listening services.

Options:

| **Option** | **Meaning** |
|------------|-----------------------------------|
| -t | TCP |
| -u | UDP |
| -l | Listening |
| -p | Show process |
| -n | Display numerical addresses/ports |

head -10 limits the displayed output to the first 10 lines.

**Result**

The system health script was successfully created and used to collect basic information about uptime, memory, disk usage, and network connections.

**Step 4: Script 4 – Failed Login Alert**

**4.1 Create the Script File**

**Command**

nano alert_failed_logins.sh

**Purpose**

The purpose of this script is to detect a high number of failed login attempts and generate an alert when the configured threshold is exceeded.

This introduces the concept of basic automated security detection.

**4.2 Write the Script**

Enter:

\#!/bin/bash

\# ============================================

\# SCRIPT: alert_failed_logins.sh

\# AUTHOR: Jeal Patel

\# DATE: August 2026

\# PURPOSE: Alert if there are more than 10 failed logins

\# ============================================

\# Count failed logins

FAILED_COUNT=\$(sudo grep "Failed password" /var/log/auth.log \| tail -100 \| wc -l)

echo "Failed logins in the last 100 attempts: \$FAILED_COUNT"

if \[ \$FAILED_COUNT -gt 10 \]; then

echo " ALERT: High number of failed login attempts detected!"

echo "Please investigate immediately."

else

echo " No unusual activity detected."

fi

**4.3 Save, Make Executable and Run**

**Make Executable**

chmod +x alert_failed_logins.sh

**Run**

./alert_failed_logins.sh

**Expected Output**

If the number of failed attempts is below the threshold:

Failed logins in the last 100 attempts: 5

No unusual activity detected.

If the number is greater than 10:

Failed logins in the last 100 attempts: 15

ALERT: High number of failed login attempts detected!

Please investigate immediately.

**What the Alert Script Does**

The following command counts matching failed-login entries:

FAILED_COUNT=\$(sudo grep "Failed password" /var/log/auth.log \| tail -100 \| wc -l)

The result is stored in the variable:

FAILED_COUNT

The script then checks:

if \[ \$FAILED_COUNT -gt 10 \]; then

Here:

| **Element** | **Meaning** |
|----------------|-------------------------------|
| if | Starts a condition |
| \$FAILED_COUNT | Number of failed login events |
| -gt | Greater than |
| 10 | Alert threshold |

Therefore:

Failed Login Count

↓

Is count \> 10?

↓

┌───┴───┐

YES NO

↓ ↓

ALERT Normal

**Important Note**

The script currently checks the **last 100 matching failed-login records**, not strictly the failed logins that occurred within the last hour.

Therefore, the output:

Failed logins in the last 100 attempts

is more accurate than describing it as:

Failed logins in the last hour

A true one-hour detection would require filtering log entries according to their timestamps.

**Result**

The script successfully demonstrates basic threshold-based security alerting using Bash conditional logic.

**Troubleshooting Flow**

This lab can be remembered as a simple security-monitoring workflow:

1\. Identify Failed Login Events

↓

grep "Failed password" /var/log/auth.log

2\. View Recent Events

↓

tail -10

3\. Identify Source IPs

↓

awk + sort + uniq

4\. Check System Health

↓

uptime + free + df

5\. Check Network Services

↓

ss -tulpn

6\. Generate Security Alert

↓

if condition

**Easy Memory Trick**

Think:

**Find → Filter → Count → Check → Alert**

or:

"Find suspicious events → identify their source → measure their frequency → check the system → generate an alert."

This is a useful foundation for SOC monitoring.

**Expected Results Summary**

| **Test / Script** | **Expected Result** | **What It Proves** |
|----|----|----|
| check_failed_logins.sh | Failed login entries displayed | Authentication log analysis |
| count_failed_by_ip.sh | IP addresses and counts displayed | Source IP analysis |
| system_health.sh | Uptime, RAM, disk and connections displayed | System health monitoring |
| alert_failed_logins.sh | Alert or normal-activity message | Basic security detection |
| chmod +x | Script becomes executable | Linux permissions |
| grep | Matching log events found | Log filtering |
| awk | Required field extracted | Log parsing |
| sort + uniq | Repeated IPs counted | Event aggregation |
| wc -l | Number of matching events counted | Event counting |
| ss -tulpn | Listening sockets displayed | Network exposure analysis |

**Cybersecurity Relevance**

This lab is directly useful for basic **SOC operations, Linux security monitoring, incident detection, and Blue Team activities**.

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

│ ↓

│ Failed Login Events

│ ↓

│ grep + awk

│ ↓

│ Source IP Analysis

│ ↓

│ sort + uniq

│ ↓

│ Count Attempts

│ ↓

│ Threshold Check

│ ↓

└── Security Alert

This basic workflow demonstrates the same general concept used in larger security-monitoring environments:

Log Collection

↓

Log Filtering

↓

Event Analysis

↓

Detection Logic

↓

Alert

↓

Investigation

**Practical Learning Outcomes**

After completing this lab, the following concepts were practiced:

1. Creating Bash scripts using Nano.

2. Understanding the Bash shebang \#!/bin/bash.

3. Assigning execute permissions using chmod +x.

4. Running scripts using ./script.sh.

5. Searching Linux authentication logs using grep.

6. Extracting log fields using awk.

7. Counting repeated events using uniq -c.

8. Sorting security events using sort.

9. Counting log entries using wc -l.

10. Checking Linux system health using standard commands.

11. Checking network sockets using ss.

12. Using Bash variables.

13. Using conditional statements for basic detection.

14. Understanding how scripting can automate SOC monitoring tasks.

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

These scripting skills provide a strong foundation for further learning in **SOC operations, SIEM, incident response, Linux security, log analysis, and Blue Team cybersecurity**.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_18_1.png)

![Screenshot 2](IAM_Lab_18_2.png)

![Screenshot 3](IAM_Lab_18_3.png)

![Screenshot 4](IAM_Lab_18_4.png)

![Screenshot 5](IAM_Lab_18_5.png)

![Screenshot 6](IAM_Lab_18_6.png)

![Screenshot 7](IAM_Lab_18_7.png)

![Screenshot 8](IAM_Lab_18_8.png)

![Screenshot 9](IAM_Lab_18_9.png)

![Screenshot 10](IAM_Lab_18_10.png)

![Screenshot 11](IAM_Lab_18_11.png)

![Screenshot 12](IAM_Lab_18_12.png)

