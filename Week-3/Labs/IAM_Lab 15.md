**IAM Lab 15 — Linux Log Analysis & Authentication Monitoring**

**Objective**

The objective of this lab was to practice **Linux log analysis and authentication monitoring** by examining authentication and system logs, identifying failed and successful SSH login attempts, monitoring logs in real time, and counting failed login attempts by source IP address.

This lab demonstrates a basic **SOC/Blue Team workflow**:

**Generate activity → Collect logs → Search logs → Identify suspicious activity → Analyze the source**

**Lab Environment**

| **Component** | **Details** |
|-------------------|--------------------|
| Domain Controller | DC-Server |
| Windows Client | Win11-Client |
| Linux Machine | Ubuntu-Lab |
| Linux User | labuser |
| Linux IP | 172.16.0.100 |
| Windows Client IP | 172.16.0.50 |
| Log File | /var/log/auth.log |
| System Log | /var/log/syslog |
| Log Framework | systemd/journalctl |
| Protocol Tested | SSH |

**Step 0: Start Your VMs**

**Procedure**

1. Started **DC-Server**.

2. Logged in using:

mydomain\Administrator

3. Started **Ubuntu-Lab**.

4. Logged in as:

Username: labuser

Password: P@ssw0rd123

5. Started **Win11-Client**.

6. Logged in using:

mydomain\Administrator

**Result**

All three virtual machines were successfully started.

**Step 1: Open Ubuntu Terminal**

The Ubuntu terminal should display:

labuser@ubuntu-lab:~\$

This indicates that the current user is labuser and the current working directory is the user's home directory.

**Result**

Successfully accessed the Ubuntu terminal.

**Step 2: Practice Viewing Authentication Logs**

**2.1 Monitor Authentication Logs in Real Time**

**Command**

sudo tail -f /var/log/auth.log

**What it does**

The command displays the latest authentication log entries and continuously monitors the file for new entries.

The -f option means **follow**, so new log entries appear as they are generated.

**Example Output**

Aug 11 10:00:01 ubuntu-lab sshd\[1234\]: Failed password for invalid user root from 172.16.0.50 port 54321 ssh2

Aug 11 10:00:02 ubuntu-lab sshd\[1235\]: Accepted password for labuser from 172.16.0.1 port 54322 ssh2

**Important Information**

The log can reveal:

- Authentication result

- Username

- Source IP address

- Source port

- SSH service

- Timestamp

**To Exit**

Press:

Ctrl + C

**Result**

Authentication activity was successfully monitored in real time.

**2.2 Search for Failed Login Attempts**

**Command**

sudo grep "Failed password" /var/log/auth.log

**What it does**

Searches /var/log/auth.log for entries containing:

Failed password

This can be used to identify unsuccessful authentication attempts.

**Example Output**

Aug 11 10:00:01 ubuntu-lab sshd\[1234\]: Failed password for invalid user root from 172.16.0.50 port 54321 ssh2

**Security Observation**

Repeated failed authentication attempts may indicate:

- Incorrect credentials

- A user forgetting their password

- Unauthorized access attempts

- Password guessing activity

**Result**

Failed authentication events were successfully identified.

**2.3 Search for Successful Login Attempts**

**Command**

sudo grep "Accepted password" /var/log/auth.log

**What it does**

Searches the authentication log for successful password-based SSH authentication.

**Example Output**

Aug 11 10:00:02 ubuntu-lab sshd\[1235\]: Accepted password for labuser from 172.16.0.1 port 54322 ssh2

**Security Observation**

Successful authentication logs can help an analyst determine:

- Which account logged in

- When the login occurred

- Where the login originated

- Whether access was successful

**Result**

Successful authentication events were successfully identified.

**2.4 View System Logs**

**Command**

sudo cat /var/log/syslog \| head -20

**What it does**

The command displays the first 20 lines of the system log.

The /var/log/syslog file contains system-related events and messages.

**Result**

System log entries were successfully viewed.

**2.5 View Systemd Logs**

**Command**

sudo journalctl -xe

**What it does**

Displays detailed systemd journal information, including relevant system messages, warnings, and errors.

**To Exit**

Press:

q

**Result**

Systemd journal logs were successfully accessed and reviewed.

**Step 3: Simulate a Failed SSH Login**

This section demonstrates how a failed authentication event can be generated and then detected through logs.

**3.1 Attempt SSH Login from Win11-Client**

On **Win11-Client**, open Command Prompt.

Run:

ssh labuser@172.16.0.100

When prompted for the password, enter an intentionally incorrect password.

For example:

WrongPassword123

**Expected Output**

labuser@172.16.0.100's password:

Permission denied, please try again.

Repeat the failed login attempt approximately **3–4 times** for the exercise.

**Result**

Multiple failed SSH authentication attempts were generated.

**3.2 Detect the Failed Login in Ubuntu Logs**

Return to Ubuntu and run:

sudo grep "Failed password" /var/log/auth.log

**Expected Output**

Example:

Aug 11 10:05:23 ubuntu-lab sshd\[5678\]: Failed password for labuser from 172.16.0.50 port 54323 ssh2

Aug 11 10:05:34 ubuntu-lab sshd\[5679\]: Failed password for labuser from 172.16.0.50 port 54324 ssh2

Aug 11 10:05:45 ubuntu-lab sshd\[5680\]: Failed password for labuser from 172.16.0.50 port 54325 ssh2

**Security Observation**

The failed SSH attempts generated authentication events that could be detected from the Ubuntu authentication logs.

The source IP in this example is:

172.16.0.50

This represents the Win11-Client.

**Result**

The simulated failed authentication attempts were successfully identified in the logs.

**3.3 Monitor Failed Login Attempts in Real Time**

On Ubuntu, run:

sudo tail -f /var/log/auth.log 

Keep this terminal running.

On Win11-Client, perform another unsuccessful SSH login:

ssh labuser@172.16.0.100

Enter an incorrect password. 

**Observation**

A new authentication event should appear on Ubuntu while the login attempt is happening.

This demonstrates:

Win11-Client

↓

SSH Login Attempt

↓

Ubuntu SSH Service

↓

Authentication Event

↓

/var/log/auth.log

↓

SOC Analyst

**To Exit**

Press:

Ctrl + C

**Result**

Authentication activity was successfully observed in real time.

**Step 4: Simulate a Successful SSH Login**

Now test a legitimate authentication attempt.

On Win11-Client:

ssh labuser@172.16.0.100

Enter the correct password:

P@ssw0rd123

**Expected Result**

After successful authentication, you should receive an Ubuntu shell.

For example:

Welcome to Ubuntu

labuser@ubuntu-lab:~\$

**Result**

The SSH authentication was successfully completed.

**Step 4.1: Verify Successful Login in Logs**

On Ubuntu:

sudo grep "Accepted password" /var/log/auth.log

**Example Output**

Aug 11 10:06:00 ubuntu-lab sshd\[5681\]: Accepted password for labuser from 172.16.0.50 port 54326 ssh2 

**Observation**

The successful login was recorded in /var/log/auth.log.

The log provides useful information including:

User: labuser

Source IP: 172.16.0.50

Authentication: Accepted

Service: sshd

**Result**

The successful SSH authentication was successfully verified through log analysis.

**Step 5: Count Failed Logins by IP Address**

**Command**

sudo grep "Failed password" /var/log/auth.log \| awk '{print \$11}' \| sort \| uniq -c \| sort -nr

**Purpose**

This command processes the authentication logs to determine how many failed authentication attempts originated from each IP address.

**Command Breakdown**

| **Command** | **Purpose** |
|----|----|
| grep "Failed password" | Finds failed login events |
| awk '{print \$11}' | Extracts the relevant field containing the IP address in the lab's expected log format |
| sort | Sorts the extracted IP addresses |
| uniq -c | Counts occurrences |
| sort -nr | Sorts counts numerically in descending order |

**Example Output**

5 172.16.0.50

1 192.168.1.100

**Security Interpretation**

The output allows an analyst to quickly identify IP addresses associated with repeated failed authentication attempts.

For example:

5 172.16.0.50

means the IP address 172.16.0.50 generated **5 failed authentication events** in the log data being analyzed.

**Result**

Failed authentication attempts were successfully grouped and counted by source IP address.

**Investigation Summary**

| **Activity** | **Command** | **Purpose** |
|----|----|----|
| Real-time authentication monitoring | sudo tail -f /var/log/auth.log | Monitor authentication events |
| Find failed logins | grep "Failed password" | Detect unsuccessful authentication |
| Find successful logins | grep "Accepted password" | Identify successful authentication |
| View system logs | cat /var/log/syslog \| head -20 | Review system events |
| View systemd logs | journalctl -xe | Review systemd messages |
| Count failed logins | grep ... \| awk ... | Identify repeated source IPs |

**SOC Analyst Perspective**

This lab demonstrates a simplified version of what a **SOC Analyst** does during authentication monitoring.

**1. Collect**

Authentication events are generated by the SSH service.

**2. Identify**

The analyst searches for:

Failed password

and:

Accepted password

**3. Analyze**

The analyst examines:

- Timestamp

- Username

- Source IP

- Authentication result

- Number of attempts

**4. Detect**

Repeated failed authentication attempts from the same IP could warrant further investigation.

**5. Investigate**

The analyst can determine whether the activity represents:

Normal user behavior

OR

Potential unauthorized access

OR

Password-guessing activity

**Key Takeaways**

**Authentication Logs**

/var/log/auth.log

can provide valuable information about authentication-related activity.

**Failed Authentication**

Failed password

can be searched to identify unsuccessful login attempts.

**Successful Authentication**

Accepted password

can be searched to identify successful password authentication.

**Real-Time Monitoring**

sudo tail -f /var/log/auth.log

allows an analyst to observe new authentication events as they occur.

**Log Filtering**

grep can be used to search logs for specific events.

**Log Processing**

Commands such as:

grep → awk → sort → uniq

can transform raw logs into useful security information.

**Skills Demonstrated**

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

**Conclusion**

This lab provided practical experience in analyzing Linux authentication and system logs. Failed and successful SSH login attempts were deliberately generated from the Windows client and then investigated from the Ubuntu system.

The exercise demonstrated how a SOC analyst can use Linux command-line tools to **identify authentication events, monitor logs in real time, investigate failed login attempts, determine source IP addresses, and count repeated authentication failures**.

This lab provides a useful foundation for progressing toward **SIEM-based log analysis and SOC alert investigation**, where similar authentication events can be collected centrally and correlated across multiple systems.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_15_1.png)

![Screenshot 2](IAM_Lab_15_2.png)

![Screenshot 3](IAM_Lab_15_3.png)

![Screenshot 4](IAM_Lab_15_4.png)

![Screenshot 5](IAM_Lab_15_5.png)

![Screenshot 6](IAM_Lab_15_6.png)

![Screenshot 7](IAM_Lab_15_7.png)

![Screenshot 8](IAM_Lab_15_8.png)

![Screenshot 9](IAM_Lab_15_9.png)

![Screenshot 10](IAM_Lab_15_10.png)

![Screenshot 11](IAM_Lab_15_11.png)

![Screenshot 12](IAM_Lab_15_12.png)

![Screenshot 13](IAM_Lab_15_13.png)

![Screenshot 14](IAM_Lab_15_14.png)

