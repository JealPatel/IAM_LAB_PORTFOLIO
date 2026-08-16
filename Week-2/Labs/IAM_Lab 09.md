**Active Directory Lab 9**

**Network Troubleshooting Commands – Practical Implementation**

**Objective**

The objective of this lab was to gain hands-on experience with essential network troubleshooting commands in a Windows environment. The lab involved running various network diagnostic commands on both the Domain Controller and the Windows 11 client to understand network configuration, connectivity, DNS resolution, and active connections. The goal was to develop foundational troubleshooting skills necessary for IAM and SOC roles.

**Lab Environment**

| Component | Details |
|----|----|
| Operating System (DC) | Windows Server 2019 (Domain Controller) |
| Operating System (Client) | Windows 11 Pro |
| Virtualization | Oracle VirtualBox |
| Domain | [mydomain.com](https://mydomain.com/) |
| DC IP Address | 172.16.0.1 |
| Client IP Address | 172.16.0.50 |
| Tools Used | Command Prompt, ipconfig, ping, tracert, nslookup, netstat |

**Step 1: Opening Command Prompt on Win11-Client**

**Procedure:**

1. On **Win11-Client**, clicked the Start Menu.

2. Typed cmd in the search box.

3. Right-clicked **Command Prompt** → selected **Run as administrator**.

4. The Command Prompt window opened with administrative privileges.

**Result:**\
Command Prompt was successfully opened as Administrator on the Windows 11 client.

**Step 2: Running Network Commands on Win11-Client**

The following network commands were executed one by one to understand their output and diagnostic purpose.

**2.1 ipconfig /all**

**Command:**

cmd

ipconfig /all

**Purpose:**\
Displays detailed IP configuration information including IP address, subnet mask, default gateway, DNS servers, and MAC address.

**Output on Win11-Client:**

| Parameter | Value |
|--------------------|-------------------|
| Host Name | Win11-Client |
| Primary DNS Suffix | mydomain.com |
| IPv4 Address | 172.16.0.50  |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 172.16.0.1 |
| DNS Servers | 172.16.0.1 |
| DHCP Enabled | Yes |
| MAC Address | 08-00-27-75-45-79 |

**Observation:**

- The client successfully obtained an IP address within the 172.16.0.x range.

- The DNS server was correctly pointing to the Domain Controller (172.16.0.1).

- The default gateway was correctly set to the Domain Controller.

**Result:**\
The ipconfig /all command successfully displayed complete network configuration details.

**2.2 ping 172.16.0.1**

**Command:**

cmd

ping 172.16.0.1

**Purpose:**\
Tests basic network connectivity to the Domain Controller. Verifies that the client can reach the server.

**Expected Output:**

text

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

**Observation:**

- All four ICMP echo requests received replies.

- The response time was less than 1 millisecond (indicating a direct connection).

- TTL value was 128 (typical for Windows Server).

**Result:**\
The client successfully communicated with the Domain Controller. Network connectivity was confirmed.

**Screenshot 2:** ping 172.16.0.1 Output

**2.3 ping mydomain.com**

**Command:**

cmd

ping mydomain.com

**Purpose:**\
Tests connectivity AND DNS resolution simultaneously. This confirms that DNS is working correctly and the network path is clear.

**Expected Output:**

text

Pinging mydomain.com \[172.16.0.1\] with 32 bytes of data:

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

Reply from 172.16.0.1: bytes=32 time\<1ms TTL=128

**Observation:**

- The domain name mydomain.com successfully resolved to IP 172.16.0.1.

- Replies were received from the Domain Controller.

**Result:**\
DNS resolution was confirmed to be working correctly. The client successfully resolved the domain name and reached the target.

**Screenshot 3:** ping mydomain.com Output

**2.4 tracert 172.16.0.1**

**Command:**

cmd

tracert 172.16.0.1

**Purpose:**\
Traces the route taken by packets to reach the destination. This command helps identify network hops and potential bottlenecks.

**Expected Output:**

text

Tracing route to 172.16.0.1 over a maximum of 30 hops

1 \<1 ms \<1 ms \<1 ms 172.16.0.1

Trace complete.

**Observation:**

- Only 1 hop was required to reach the Domain Controller (direct connection).

- This indicates that the client and server are on the same local network segment.

**Result:**\
The tracert command confirmed that the client can reach the Domain Controller directly without intermediate routers.

**Screenshot 4:** tracert 172.16.0.1 Output

**2.5 nslookup mydomain.com**

**Command:**

cmd

nslookup mydomain.com

**Purpose:**\
Queries DNS for the IP address of mydomain.com. This command confirms that DNS records are correctly configured.

**Expected Output:**

text

Server: DC01.mydomain.com

Address: 172.16.0.1

Name: mydomain.com

Address: 172.16.0.1

**Observation:**

- The DNS server (172.16.0.1) successfully responded.

- The domain mydomain.com resolved to 172.16.0.1.

**Result:**\
DNS resolution was confirmed. The DNS server is correctly configured and authoritative for the mydomain.com zone.

**Screenshot 5:** nslookup mydomain.com Output

**2.6 netstat -an**

**Command:**

cmd

netstat -an

**Purpose:**\
Shows all active network connections and listening ports on the machine. This helps identify what services are running and what ports are open.

**Output Analysis:**

**TCP Listening Ports:**

| Proto | Local Address | Foreign Address | State |
|-------|-----------------|-----------------|-----------|
| TCP | 0.0.0.0:135 | 0.0.0.0:0 | LISTENING |
| TCP | 0.0.0.0:445 | 0.0.0.0:0 | LISTENING |
| TCP | 0.0.0.0:5040 | 0.0.0.0:0 | LISTENING |
| TCP | 172.16.0.50:139 | 0.0.0.0:0 | LISTENING |

**Interpretation:**

| Port | Service | Purpose |
|----------|-----------------|--------------------------------|
| **135** | RPC | Windows remote procedure calls |
| **139** | NetBIOS | File and printer sharing |
| **445** | SMB | Windows file sharing (Active) |
| **5040** | Windows Service | Internal Windows service |

**UDP Ports:**

| Proto | Local Address | Foreign Address |
|-------|-----------------|-----------------|
| UDP | 0.0.0.0:123 | *:* |
| UDP | 172.16.0.50:137 | *:* |
| UDP | 172.16.0.50:138 | *:* |
| UDP | 0.0.0.0:5353 | *:* |

**Interpretation:**

| Port | Service | Purpose |
|--------------|---------|-----------------------|
| **123** | NTP | Network Time Protocol |
| **137, 138** | NetBIOS | File sharing |
| **5353** | mDNS | Local name resolution |

**Observation:**

- Port 445 (SMB) was actively listening — the client could share files.

- Many dynamic ports (49664-49707) were in use — normal Windows behavior.

- No suspicious ports were open — the system appeared clean.

**Result:**\
netstat -an successfully displayed all active connections and listening ports. The output was clean with no suspicious open ports.

**Screenshot 6:** netstat -an Output on Win11-Client

## 📸 Screenshots

![Screenshot 1](IAM_Lab_09_1.png)

![Screenshot 2](IAM_Lab_09_2.png)

![Screenshot 3](IAM_Lab_09_3.png)

![Screenshot 4](IAM_Lab_09_4.png)

![Screenshot 5](IAM_Lab_09_5.png)

![Screenshot 6](IAM_Lab_09_6.png)

![Screenshot 7](IAM_Lab_09_7.png)

