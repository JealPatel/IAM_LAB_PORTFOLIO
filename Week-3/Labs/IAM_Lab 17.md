**IAM Lab 17 — Linux Network Configuration, DNS & Connectivity Analysis**

**Objective**

The objective of this lab is to practice basic Linux network troubleshooting and analysis using:

- ip addr

- ip route

- ping

- dig

- nslookup

- curl

- ss

The lab helps understand the relationship between **IP addressing, routing, DNS resolution, HTTP connectivity, and listening network ports**.

**Lab Environment**

| **Component** | **Details** |
|---------------|------------------------------------|
| DC-Server | Windows Server / Domain Controller |
| Ubuntu-Lab | Ubuntu Linux |
| Ubuntu User | labuser |
| DC IP | 172.16.0.1 |
| Ubuntu IP | 172.16.0.100 |
| Network | 172.16.0.0/24 |
| Domain | mydomain.com |

**Step 0: Start the VMs**

**Procedure**

1. Started **DC-Server**.

2. Logged in using:

mydomain\Administrator

3. Started **Ubuntu-Lab**.

4. Logged in using:

Username: labuser

Password: P@ssw0rd123

**Result**

Both virtual machines were successfully started.

**Step 1: IP Configuration**

**1.1 Check IP Addresses**

**Command**

ip addr

**Purpose**

The ip addr command displays the network interfaces and IP addresses configured on the Ubuntu system.

You may see something similar to:

lo:

inet 127.0.0.1/8

enp0s3:

inet 172.16.0.100/24

Your interface name may be different, such as:

ens33

enp0s3

eth0

**Important Interfaces**

| **Interface** | **Example IP** | **Purpose** |
|---------------|-----------------|------------------------|
| lo | 127.0.0.1 | Loopback / localhost |
| enp0s3 | 172.16.0.100/24 | Main network interface |

**Understanding /24**

172.16.0.100/24

means the subnet mask is:

255.255.255.0

and the Ubuntu machine belongs to:

172.16.0.0/24

**Result**

The Ubuntu network interface and assigned IP address were successfully identified.

**1.2 Check the Routing Table**

**Command**

ip route

**Example**

default via 172.16.0.1 dev enp0s3

172.16.0.0/24 dev enp0s3 proto kernel scope link src 172.16.0.100

**What It Means**

| **Entry** | **Meaning** |
|------------------------|------------------------------|
| default via 172.16.0.1 | Default gateway |
| 172.16.0.0/24 | Local network |
| dev enp0s3 | Network interface being used |
| src 172.16.0.100 | Ubuntu's source IP |

**Result**

The routing table was successfully examined.

**Step 2: Connectivity Testing**

**2.1 Ping the Domain Controller**

**Command**

ping 172.16.0.1 -c 4

**Example Result**

PING 172.16.0.1 (172.16.0.1) 56(84) bytes of data.

64 bytes from 172.16.0.1: icmp_seq=1 ttl=128 time=0.5 ms

64 bytes from 172.16.0.1: icmp_seq=2 ttl=128 time=0.5 ms

--- 172.16.0.1 ping statistics ---

4 packets transmitted, 4 received, 0% packet loss

**What This Tests**

This checks whether Ubuntu can communicate with the Domain Controller at the network layer.

If you receive:

0% packet loss

the connectivity test is successful.

**Result**

Connectivity between Ubuntu-Lab and DC-Server was successfully tested.

**2.2 Test DNS Resolution**

**Command**

ping mydomain.com -c 4

**Expected Behavior**

If DNS is correctly configured, the hostname should resolve to the DC's IP:

PING mydomain.com (172.16.0.1)

**This Demonstrates**

mydomain.com

↓

DNS Resolution

↓

172.16.0.1

↓

Ping

↓

DC-Server

**Result**

DNS resolution and network connectivity were tested together.

**Step 3: DNS Analysis**

**3.1 Use dig**

**Command**

dig mydomain.com

**Purpose**

dig provides detailed DNS query information.

Look for:

ANSWER SECTION:

mydomain.com. 3600 IN A 172.16.0.1

This indicates that the DNS server returned an **A record** mapping:

mydomain.com → 172.16.0.1

You may also see:

SERVER: 172.16.0.1#53

This indicates the DNS server that answered the query.

**Result**

A detailed DNS query for mydomain.com was successfully performed.

**3.2 Use nslookup**

**Command**

nslookup mydomain.com

**Example**

Server: 172.16.0.1

Address: 172.16.0.1#53

Name: mydomain.com

Address: 172.16.0.1

**Purpose**

nslookup provides a simpler way to test DNS resolution.

**Comparison**

| **Tool** | **Main Use** |
|----------|-----------------------|
| dig | Detailed DNS analysis |
| nslookup | Quick DNS lookup |

**Result**

DNS resolution was successfully verified using nslookup.

**Step 4: HTTP Connectivity Testing**

**4.1 Test HTTP Using IP Address**

**Command**

curl -v http://172.16.0.1

**What -v Means**

-v = verbose

It displays detailed information about the connection and HTTP request.

You may see:

\* Trying 172.16.0.1:80...

\* Connected to 172.16.0.1

\> GET / HTTP/1.1

**Important**

**Don't worry if this fails.**

If your Windows Server does not have an HTTP/web server listening on port 80, you may receive:

Connection refused

or:

Failed to connect

That doesn't necessarily mean your network is broken.

It simply means:

Network connectivity → May be working

HTTP service on port 80 → Not running

**Result**

An HTTP connection attempt to the DC was performed using its IP address.

**4.2 Test HTTP Using Domain Name**

**Command**

curl -v http://mydomain.com

**Purpose**

This test combines:

DNS Resolution

\+

HTTP Connection

The system first needs to resolve:

mydomain.com

↓

172.16.0.1

and then attempt the HTTP connection.

**Result**

HTTP connectivity using the domain name was tested.

**Step 5: Check Listening Ports**

**5.1 Use ss**

**Command**

sudo ss -tulpn

**Purpose**

This command displays network sockets and listening services.

**Options**

| **Option** | **Meaning** |
|------------|--------------------------------|
| -t | TCP |
| -u | UDP |
| -l | Listening |
| -p | Show process |
| -n | Show numerical addresses/ports |

You might see:

Netid State Local Address:Port

tcp LISTEN 0.0.0.0:22

**Port 22**

Port:

22

is normally associated with:

SSH

So if SSH is running:

sshd → TCP → Port 22 → LISTEN

**Important**

Your output **doesn't have to exactly match the worksheet**.

For example, if SSH isn't running, port 22 won't appear.

You can check SSH with:

sudo systemctl status ssh

Then check again:

sudo ss -tulpn

**Result**

Listening ports and associated services were successfully examined.

**🔎 Troubleshooting Flow**

This is probably the **most useful part to remember for your cybersecurity/SOC practice**.

If Ubuntu cannot reach your DC, troubleshoot from the bottom upward:

1\. Check IP

↓

ip addr

2\. Check route

↓

ip route

3\. Check raw connectivity

↓

ping 172.16.0.1

4\. Check DNS

↓

nslookup mydomain.com

dig mydomain.com

5\. Check application connectivity

↓

curl -v http://mydomain.com

6\. Check local listening services

↓

sudo ss -tulpn

**Easy Memory Trick**

Think:

**IP → Route → Ping → DNS → Application → Ports**

or:

**"Can I identify myself → find the path → reach the machine → resolve its name → reach the service → see what's listening?"**

That's a really solid troubleshooting mindset.

**Expected Results Summary**

| **Test** | **Expected Result** | **What It Proves** |
|----|----|----|
| ip addr | 172.16.0.100/24 | IP configuration |
| ip route | Route via 172.16.0.1 | Routing |
| ping 172.16.0.1 | Replies | Network connectivity |
| ping mydomain.com | Resolves to 172.16.0.1 | DNS + connectivity |
| dig mydomain.com | A record returned | Detailed DNS |
| nslookup mydomain.com | IP returned | DNS resolution |
| curl -v http://172.16.0.1 | Depends on HTTP service | Application connectivity |
| curl -v http://mydomain.com | Depends on HTTP service | DNS + HTTP |
| sudo ss -tulpn | Listening sockets | Network exposure |

**Cybersecurity Relevance**

This lab is directly useful for basic **SOC and network troubleshooting**.

An analyst can use these commands to investigate questions such as:

- What IP address does this machine have?

- Which network does it belong to?

- Where is its traffic being routed?

- Can it communicate with the Domain Controller?

- Is DNS resolving correctly?

- Can the machine reach a particular service?

- Which ports are currently exposed?

- Which processes are associated with those ports?

For example:

Ubuntu

172.16.0.100

│

│ ping

↓

DC-Server

172.16.0.1

│

├── DNS : 53

├── SSH : 22 (if enabled)

└── Other services

## 📸 Screenshots

![Screenshot 1](IAM_Lab_17_1.png)

![Screenshot 2](IAM_Lab_17_2.png)

![Screenshot 3](IAM_Lab_17_3.png)

![Screenshot 4](IAM_Lab_17_4.png)

![Screenshot 5](IAM_Lab_17_5.png)

![Screenshot 6](IAM_Lab_17_6.png)

![Screenshot 7](IAM_Lab_17_7.png)

![Screenshot 8](IAM_Lab_17_8.png)

![Screenshot 9](IAM_Lab_17_9.png)

