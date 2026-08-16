**IAM Lab 16 — Linux Service, Process & Network Management**

**Objective**

The objective of this lab was to practice basic Linux **service management, process management, and network socket/port inspection**.

The lab focused on using systemctl to manage services, ps and top to monitor processes, kill to terminate a test process, and ss to identify listening network ports.

These are important Linux administration and cybersecurity skills because a security analyst may need to determine **which services are running, which processes are active, and which network ports are exposed**.

**Lab Environment**

| **Component** | **Details** |
|------------------|---------------|
| Virtual Machine | Ubuntu-Lab |
| Operating System | Ubuntu Linux |
| User | labuser |
| SSH Service | OpenSSH |
| Service Manager | systemd |
| Process Tools | ps, top, kill |
| Network Tool | ss |

**Step 0: Start the VM**

**Procedure**

1. Started the **Ubuntu-Lab** virtual machine.

2. Logged in using:

Username: labuser

Password: P@ssw0rd123

3. Opened the terminal.

The terminal should display something similar to:

labuser@ubuntu-lab:~\$

**Result**

Ubuntu-Lab was successfully started and the labuser account was accessed.

**Step 1: Linux Service Management**

**1.1 Check the SSH Service**

**Command**

sudo systemctl status sshd 

On Ubuntu, the service may be displayed as **ssh.service** even when you use the sshd service name.

**Purpose**

The command checks the current status of the OpenSSH service.

**Important Information**

Look for:

Active: active (running)

This indicates that the SSH service is currently running.

You may also see:

Loaded: ... enabled

which indicates that the service is configured to start automatically during boot.

The **Main PID** identifies the process ID associated with the service.

So here When I check the status then it inactive(dead) so I have to get active by restarting the sshd

And then after I check the status it is active now

**Example**

● ssh.service - OpenSSH Server

Loaded: loaded (...; enabled; ...)

Active: active (running)

**Result**

The SSH service status was successfully checked.

**1.2 Stop the SSH Service**

**Command**

sudo systemctl stop sshd

Then verify:

sudo systemctl status sshd

**Expected Result**

You should see something similar to:

Active: inactive (dead)

**Observation**

The SSH service was stopped.

Because this lab is being performed directly from the Ubuntu VM console, stopping SSH should not disconnect the current terminal session.

**Result**

The SSH service was successfully stopped. 

**1.3 Start the SSH Service**

**Command**

sudo systemctl start sshd

Verify:

sudo systemctl status sshd

**Expected Result**

Active: active (running)

**Observation**

The SSH service became active again.

**Result**

The SSH service was successfully restarted.

**1.4 Restart the SSH Service**

**Command**

sudo systemctl restart sshd

**Purpose**

restart stops the service and starts it again.

This is commonly useful after making changes to a service's configuration.

**Result**

The SSH service was successfully restarted.

**1.5 Enable SSH at Boot**

**Command**

sudo systemctl enable sshd

**Purpose**

The enable command configures the service to start automatically when Linux boots.

**Result**

SSH was configured to start automatically during system startup.

**1.6 Disable SSH at Boot**

**Command**

sudo systemctl disable sshd

**Purpose**

The disable command prevents the service from automatically starting during boot.

**Important**

After completing the exercise, enable SSH again:

sudo systemctl enable sshd

This ensures the lab environment is returned to the expected configuration.

**Result**

The behavior of enabling and disabling services at boot was successfully practiced.

**Step 2: Linux Process Management**

**2.1 List Running Processes**

**Command**

ps aux

**Purpose**

The ps aux command displays currently running processes on the system.

**Important Columns**

| **Column** | **Meaning** |
|------------|-----------------------------------------|
| USER | User who owns the process |
| PID | Process ID |
| %CPU | CPU utilization |
| %MEM | Memory utilization |
| VSZ | Virtual memory size |
| RSS | Resident memory size |
| STAT | Current process state |
| START | Process start time |
| TIME | CPU time used |
| COMMAND | Command/program associated with process |

**Example**

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

root 1 0.0 0.1 101456 8456 ? Ss 10:00 0:01 /sbin/init

labuser 456 0.0 0.2 10524 9672 pts/0 Ss 10:01 0:00 -bash

**Security Relevance**

A security analyst can use process listings to identify:

- Unexpected processes

- Suspicious programs

- High CPU-consuming processes

- Processes running under unexpected users

**Result**

Running Linux processes were successfully listed.

**2.2 Monitor Processes in Real Time**

**Command**

top

**Purpose**

top provides a real-time view of running processes and system resource usage.

**Information to Observe**

- CPU utilization

- Memory utilization

- Running processes

- Process IDs

- Process users

- Process resource consumption

For example:

PID USER %CPU %MEM COMMAND

789 labuser 0.3 0.4 top

456 labuser 0.0 0.5 bash

1 root 0.0 0.4 systemd

**Useful Keys**

| **Key** | **Function** |
|---------|----------------------------|
| q | Quit top |
| k | Send a signal to a process |
| h | Display help |

**Result**

Real-time process monitoring was successfully performed.

**2.3 Find the SSH Process**

**Command**

ps aux \| grep sshd

**Purpose**

This command searches the process list for processes containing sshd.

**Example**

root 1234 0.0 0.1 12345 6789 ? Ss 10:00 0:00 /usr/sbin/sshd -D

The number:

1234

is the process ID in this example.

**⚠️ Important**

Do **not** kill the SSH service/process during the exercise unless you intentionally want to stop SSH.

Instead, use a harmless test process.

**Result**

The SSH-related process was identified using its PID.

**2.4 Understand kill -9**

**Command Structure**

sudo kill -9 PID

For example:

sudo kill -9 1234

**Purpose**

The command sends signal 9 (SIGKILL) to the specified process and forcefully terminates it.

**Important Security Practice**

Never blindly execute:

sudo kill -9 1234

because 1234 is only an example.

Always replace PID with the **actual PID of the test process**.

**2.5 Create and Kill a Test Process**

Instead of killing an important system service, create a harmless test process.

**Step 1 — Create the Process**

sleep 1000 &

The & runs the process in the background.

**Step 2 — Find the Process**

ps aux \| grep sleep

You should see something similar to:

labuser 2345 0.0 0.0 ... sleep 1000

Here:

2345

is the actual PID. 

**Step 3 — Terminate the Test Process**

Use the actual PID:

kill -9 2345

**Observation**

The test sleep process was terminated without affecting important system services.

**Result**

Process identification and termination were successfully practiced.

**Step 3: Check Listening Network Ports**

**3.1 Display Listening Ports**

**Command**

sudo ss -tulpn

**Purpose**

The ss command displays network sockets.

The options used are:

| **Option** | **Meaning** |
|------------|-----------------------------------|
| -t | TCP sockets |
| -u | UDP sockets |
| -l | Listening sockets |
| -p | Show associated processes |
| -n | Display numerical addresses/ports |

**Example Output**

Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port Process

tcp LISTEN 0 128 0.0.0.0:22 0.0.0.0:\* users:(("sshd",pid=1234))

tcp LISTEN 0 128 \[::\]:22 \[::\]:\* users:(("sshd",pid=1234))

**Important Observation**

Port:

22

is commonly associated with **SSH**.

If SSH is running, you may see an entry showing port 22 in the listening state.

**Result**

Listening network ports and their associated processes were successfully identified.

**Security Analysis**

This lab demonstrates three important areas of Linux security monitoring:

**1. Service Monitoring**

Using:

systemctl status

an analyst can determine whether a service is running.

For example:

SSH → active

**2. Process Monitoring**

Using:

ps aux

and:

top

an analyst can inspect currently running processes and resource consumption.

This can help identify potentially suspicious processes.

**3. Network Exposure**

Using:

sudo ss -tulpn

an analyst can determine which ports are listening and which processes are associated with those ports.

For example:

Port 22 → SSH → sshd

This provides a basic connection between:

Service → Process → Port

which is very useful when investigating a Linux system.

**Command Summary**

| **Command** | **Purpose** |
|------------------------|-------------------------------------------|
| systemctl status sshd | Check SSH service status |
| systemctl stop sshd | Stop SSH service |
| systemctl start sshd | Start SSH service |
| systemctl restart sshd | Restart SSH service |
| systemctl enable sshd | Enable service at boot |
| systemctl disable sshd | Disable service at boot |
| ps aux | List running processes |
| top | Monitor processes in real time |
| ps aux \| grep sshd | Find SSH-related processes |
| sleep 1000 & | Create a harmless background test process |
| kill -9 PID | Forcefully terminate a process |
| ss -tulpn | Display listening network sockets |

**Key Takeaways**

**Service Management**

systemctl

is used to manage services controlled by systemd.

**Process Management**

ps

top

kill

can be used to view, monitor, and terminate processes.

**Network Monitoring**

ss

can be used to identify listening ports and associated processes.

**Important Relationship**

A useful way to remember this lab is:

SERVICE

↓

PROCESS

↓

PORT

For example:

SSH Service

↓

sshd Process

↓

TCP Port 22

**Skills Demonstrated**

- Linux Service Management

- systemctl

- systemd

- Linux Process Management

- Process Monitoring

- ps

- top

- kill

- Network Socket Analysis

- TCP/UDP Port Identification

- Listening Port Enumeration

- SSH Service Management

- Basic Linux Security Monitoring

- Basic SOC Investigation

**Conclusion**

This lab provided hands-on experience with Linux service, process, and network management. The SSH service was started, stopped, restarted, enabled, and disabled to understand service lifecycle management.

Running processes were then examined using ps and top, while a harmless sleep process was created and terminated to practice process management safely. Finally, the ss command was used to identify listening network ports and associate them with running services.

These skills are particularly useful in **Linux administration, SOC operations, incident response, and security monitoring**, where analysts may need to determine whether an unexpected service, process, or listening port is present on a system.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_16_1.png)

![Screenshot 2](IAM_Lab_16_2.png)

![Screenshot 3](IAM_Lab_16_3.png)

![Screenshot 4](IAM_Lab_16_4.png)

![Screenshot 5](IAM_Lab_16_5.png)

![Screenshot 6](IAM_Lab_16_6.png)

![Screenshot 7](IAM_Lab_16_7.png)

![Screenshot 8](IAM_Lab_16_8.png)

![Screenshot 9](IAM_Lab_16_9.png)

![Screenshot 10](IAM_Lab_16_10.png)

![Screenshot 11](IAM_Lab_16_11.png)

![Screenshot 12](IAM_Lab_16_12.png)

