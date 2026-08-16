### **Active Directory Lab 9** 

### **Network Troubleshooting Commands – Practical Implementation** 

### **Objective** 

The objective of this lab was to gain hands-on experience with essential network troubleshooting commands in a Windows environment. The lab involved running various network diagnostic commands on both the Domain Controller and the Windows 11 client to understand network configuration, connectivity, DNS resolution, and active connections. The goal was to develop foundational troubleshooting skills necessary for IAM and SOC roles. 

### **Lab Environment** 

|Component|Details|
|---|---|
|Operating System (DC)|Windows Server 2019 (Domain Controller)|
|Operating System (Client)|Windows 11 Pro|
|Virtualization|Oracle VirtualBox|
|Domain|mydomain.com|
|DC IP Address|172.16.0.1|
|Client IP Address|172.16.0.50|
|Tools Used|Command Prompt, ipconfg, ping, tracert, nslookup, netstat|



### **Step 1: Opening Command Prompt on Win11-Client** 

### **Procedure:** 

1. On **Win11-Client** , clicked the Start Menu. 

2. Typed cmd in the search box. 

3. Right-clicked **Command Prompt** → selected **Run as administrator** . 

4. The Command Prompt window opened with administrative privileges. 

### **Result:** 

Command Prompt was successfully opened as Administrator on the Windows 11 client. 

### **Step 2: Running Network Commands on Win11-Client** 

The following network commands were executed one by one to understand their output and diagnostic purpose. 

### **2.1 ipconfig /all** 

### **Command:** 

cmd 



<!-- Start of picture text -->
OF Administrator: Command Pro X + v = ia) x<br>Microsoft Windows [Version 10.0.26200.8037]<br>(c) Microsoft Corporation. All rights reserved.<br>C:\Users\Administrator>ipconfig /all<br>Windows IP Configuration<br>Host Name .......... .. . : Winl1-Client<br>Primary Dns Suffix ..... . . : mydomain.com<br>Node Type .......... .. . : Hybrid<br>IP Routing Enabled. ....... : No<br>WINS Proxy Enabled. ...... . : No<br>DNS Suffix Search List. . .. . . : mydomain.com<br>Ethernet adapter Ethernet:<br>Connection-specific DNS Suffix . :<br>Description. ......... . . : Intel(R) PRO/1000 MT Desktop Adapter<br>Physical Address. ...... . . : 08-00-27-'75-45-79<br>DHCP Enabled. ......... . : No<br>Autoconfiguration Enabled ... . =: Yes<br>Link-local IPv6 Address .... . : fe80::4adle:51cd:e3bf:1521%10(Preferred)<br>IPv4 Address. ........ . . : 172.16.0.50(Preferred)<br>Subnet Mask .......... . : 255.255.255.0<br>Default Gateway ........ . : 172.16.0.1<br>DHCPv6 IAID......... . . : 84410407<br>DHCPv6 Client DUID. . ... . . . : 00-01-01-00-31-F8-44-BD-08-00-27-75-45-79<br>ma Q Search buc Casa ~A & CM gxjr0263:21 AM<br>DNS Servers . ........ . . 1: 172.16.0.1<br>NetBIOS over Tcpip. ..... . . : Enabled<br><!-- End of picture text -->



<!-- Start of picture text -->
DNS Servers . ........ . . 1: 172.16.0.1<br>NetBIOS over Tcpip. ..... . . : Enabled<br><!-- End of picture text -->

Parameter 

Value 

DHCP Enabled 

Yes 

MAC Address 08-00-27-75-45-79 

### **Observation:** 

- The client successfully obtained an IP address within the 172.16.0.x range. 

- The DNS server was correctly pointing to the Domain Controller (172.16.0.1). 

- The default gateway was correctly set to the Domain Controller. 

### **Result:** 

The ipconfig /all command successfully displayed complete network configuration details. 

### **2.2 ping 172.16.0.1** 

### **Command:** 

cmd 

ping 172.16.0.1 

### **Purpose:** 

Tests basic network connectivity to the Domain Controller. Verifies that the client can reach the server. 

### **Expected Output:** 

text 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

### **Observation:** 

- All four ICMP echo requests received replies. 

- The response time was less than 1 millisecond (indicating a direct connection). 

# C:\Users\Administrator>ping 172.16.0.1 

Pinging 172.16.0.1 with 32 bytes of data: Reply from 172.16.0.1: bytes=32 time=lms TTL=128 Reply from 172.16.0.1: bytes=32 time=2ms TTL=128 Reply from 172.16.0.1: bytes=32 time<lms TTL=128 Reply from 172.16.0.1: bytes=32 time<lms TTL=128 

Ping statistics for 172.16.0.1: Packets: Sent = 4, Received = 4, Lost = 0 (0% loss), Approximate round trip times in milli-seconds: Minimum = Oms, Maximum = 2ms, Average = Oms 

## C:\Users\Administrator>ping mydomain.com 

Pinging mydomain.com [172.16.0.1] with 32 bytes of data: Reply from 172.16.0.1: bytes=32 time<lms TTL=128 Reply from 172.16.0.1: bytes=32 time=lms TTL=128 Reply from 172.16.0.1: bytes=32 time=8ms TTL=128 Reply from 172.16.0.1: bytes=32 time=1lms TTL=128 

Ping statistics for 172.16.0.1: Packets: Sent = 4, Received = 4, Lost = 0 (0% loss), Approximate round trip times in milli-seconds: Minimum = Oms, Maximum = 8ms, Average = 2ms 

cy \Users\Administrator>tracert 172.16.0.1 

Tracing route to DCQ1 [172.16.0.1] over a maximum of 30 hops: 1 1 ms 1 ms 1 ms DCO1 [172.16.0.1] 

Trace complete. 

C:\Users\Administrator>nsLookup mydomain.com DNS request timed out. thmeout was 2 seconds. Server: Unknown Address: 172.16.0.1 

Name: mydomain.com Addresses: £d17:625c:f037:2:520e:e648:e656:bc7b 172.16.0.1 

10.0.2.15 

### **Interpretation:** 

|Port<br>Service|Purpose|
|---|---|
|**135**<br>RPC|Windows remote procedure calls|
|**139**<br>NetBIOS|File and printer sharing|
|**445**<br>SMB|Windows fle sharing (Active)|
|**5040**<br>Windows Service|Internal Windows service|
|**UDP Ports:**||
|Proto<br>Local Address|Foreign Address|
|UDP<br>0.0.0.0:123|_:_|
|UDP<br>172.16.0.50:137|_:_|
|UDP<br>172.16.0.50:138|_:_|
|UDP<br>0.0.0.0:5353|_:_|
|**Interpretation:**||
|Port<br>Service|Purpose|
|**123**<br>NTP|Network Time Protocol|
|**137, 138**<br>NetBIOS|File sharing|
|**5353**<br>mDNS|Local name resolution|
|**Observation:**||



- Port 445 (SMB) was actively listening — the client could share files. 

() F| Administrator: Command Pro + C:\Users\Administrator=netstat —an Active Connections Proto Local Address Foreign Address State TCP 8.6.6.6:135 6.6.6.6:6 LISTENING TCP 6.6.6.6 :495 6.6.6.6:6 LISTENING TCP 8.6.0.0: 56408 6.6.0.6:6 LISTENING TCP 6.6.0.6: 49664 8.6.6.6:6 LISTENING TCP 6.6.0.6: 49665 8.6.6.6:6 LISTENING TCP 6.6.0.6: 49666 8.6.6.6:6 LISTENING TCP 6.6.0.6: 49668 8.6.6.6:6 LISTENING TCP 6.6.6.6: 49676 6.6.6.6:6 LISTENING TCP 6.6.6.6: 49671 6.6.6.6:6 LISTENING TCP 6.6.6.6: 49707 6.6.6.6:6 LISTENING TCP 172.16.6.56:139 6.6.0.6:6 LISTENING TCP [::]:135 [::]:8 LISTENING TCP [::]:4455 [::]:8 LISTENING TCP [::]:49664 [::]:8 LISTENING TCP [::]:49665 [::]:8 LISTENING TCP [::]:49666 [::]:8 LISTENING TCP [::]:49668 [::]:68 LISTENING TCP [::]:49679 [::]:8 LISTENING TCP [::] 49671 [::]:8 LISTENING TCP [::] 49707 [::]:8 LISTENING Ts 6.6.6.6:123 an LP 6.6.0.6: 5656 oe LP 6.6.0.6:5353 oe LP 6.6.0.6:53955 oe LP 127.8.6.1:1960 oe LCP 1237.6.6.1:49963 137 .6.6.1:49963 LCP 127.8.6.1:52916 ace LCP 127.8.6.1: 56326 127 .6.6.1: 56326 UO 127.8.6.1: 56322 127 .8.6.1: 56322 LP 127.8.6.1:66959 127.8.6.1: 60959 UDP 127.6.6.1:640521 127.6.6.1:64521 LP 172.16.6.56:137 oe LP 172.16.6.56:138 oe LP 172.16.6.56:1996 oe LCP 172.16.6.56:52989 aoe UDP [::]:123 o:8 UDP [::]:5953 o18 UDP [::]:5355 o1# UDF [::1]:1986 are UDP [::1]:52988 a8 LUD [Feie: :4a4e:51ced:e3bF:1521%168)]:1990 «:8 UDP [Febe: :4ate :S5led:e3bF:1521%18)]:52907 #:* 



<!-- Start of picture text -->
+ »<br><!-- End of picture text -->

