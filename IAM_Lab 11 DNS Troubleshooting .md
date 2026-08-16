## **Active Directory Lab 12** 

## **DNS Troubleshooting – Break, Diagnose, and Fix** 

## **Objective** 

The objective of this lab was to troubleshoot DNS resolution in a Windows Server Active Directory environment. The lab involved first verifying that DNS was functioning correctly, intentionally changing the Windows 11 client's DNS server to an incorrect public DNS server, observing the resulting DNS failure, identifying the root cause using nslookup, ping, and ipconfig /all, and finally restoring the correct DNS configuration. 

The goal was to understand the importance of DNS in an Active Directory environment and develop practical **network troubleshooting and root-cause analysis skills** relevant to SOC, IAM, and System Administration roles. 

## **Lab Environment** 

|**Component**|**Details**|
|---|---|
|Operating System (DC)|Windows Server 2019 (Domain Controller)|
|Operating System (Client)|Windows 11 Pro|
|Virtualization|Oracle VirtualBox|
|Domain|mydomain.com|
|DC IP Address|172.16.0.1|
|Client IP Address|172.16.0.50|
|Correct DNS Server|172.16.0.1|
|Incorrect DNS Server|8.8.8.8|
|Tools Used|nslookup, ping, ipconfg /all|
|Network|Internal Network|



**Part 1: DNS Verification and Break-Fix Scenario** 

## **Step 1: Starting the Virtual Machines** 

## **Procedure:** 

1. Started the **DC-Server** VM. 

2. Logged in using: 

Username: mydomain\Administrator 

Password: P@ssw0rd123 

3. Started the **Win11-Client** VM. 

4. Logged in using: 

Username: mydomain\Administrator 

Password: P@ssw0rd123 

5. Verified that both VMs were connected to the same Internal Network. 

## **Result:** 

Both the Domain Controller and Windows 11 client were successfully started and connected to the lab environment. 

## **Step 2: Verifying DNS Before Breaking It** 

Before making any changes, DNS functionality was tested to establish a working baseline. 

## **Procedure:** 

1. Opened **Command Prompt** on Win11-Client. 

2. Executed: 

nslookup mydomain.com 

## **Expected Output:** 

Server:  DC01.mydomain.com 

Address: 172.16.0.1 

Name:    mydomain.com 

Address: 172.16.0.1 

## **Observation:** 

# | Command Prompt x + » 

Microsoft Windows [Version 10.0.26200.8037] se) biesesein: Corporation. ALL rights reserved. 

C:\Users\john.doe>nsLookup mydomain.com DNS request timed out. timeout was 2 seconds. Server: Unknown Address: 172.16.0.1 

Name: mydomain.com Addresses: fd17:625c:f037:2:520e:e648:e656:bc7b 172.16.0.1 10.0.2.15 



<!-- Start of picture text -->
< - — oO xX<br>Ethernet Properties x<br>NetworkingGace _ Advanced network settings.<br>Internet Protocol Version 4 (TCP/IPv4) Properties x & Enapiea<br>|| Gener : : LS 194,462<br>You fed: 175,453<br>this can get IP settings assigned automatically if your network supports<br>8 for thecapability.appropriate Otherwise,IP settings. you need to ask your network administrator 1000 (Mbps)<br>00:06:35<br>© Obtain an IP address automatically<br>© Use the following IP address:<br>\ Pediene [az.AB 16.0.at 50]ESpiT 5 adapter Rename<br>Subnet mask: [ 255 .255.255. 0 |<br>‘ Default gateway: [a72.1.0.1 phal properties 2<br>Obtain |<br>DNS server address automatically er options Edit<br>© Use the following DNS server addresses:<br>Preferred DNS server: [ 172. 16.0.1<br>(Validate settings upon exit ieee Settings ><br>ery and sharing settings<br>x (oe) con<br>oo = Pamtienns ><br>an=mQnupeB@Ggae=| © ~ 8 CWM® gen0262:20 PM<br><!-- End of picture text -->

C:\Users\john.doe>nsLookup mydomain.com DNS request timed out. * timeout was 2 seconds. Server: UnKnown Address: 8.8.8.8 

DNS request timed out. timeout was 2 seconds. DNS request timed out. timeout was 2 seconds. DNS request timed out. timeout was 2 seconds. DNS request timed out. timeout was 2 seconds. kkk Request to Unknown timed-out 

## **Step 5: Testing Domain Name Connectivity** 

The domain name was tested using the ping command. 

## **Procedure:** 

Executed: 

ping mydomain.com 

## **Expected Result:** 

Ping request could not find host mydomain.com. 

Please check the name and try again. 

## **Observation:** 

The hostname could not be resolved to an IP address. 

## **Result:** 

## **Hostname resolution failed.** 

## **Step 6: Testing Direct IP Connectivity** 

To determine whether the problem was related to general network connectivity or DNS specifically, the Domain Controller's IP address was pinged directly. 

## **Procedure:** 

Executed: 

ping 172.16.0.1 

## **Expected Result:** 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

## **Observation:** 

The client successfully communicated with the Domain Controller using its IP address. 

## **Result:** 

## **Network connectivity was confirmed to be working.** 

## **Part 3: Troubleshooting and Root Cause Analysis** 

## **Step 7: Checking Network Configuration** 

The client's network configuration was inspected to identify the DNS server being used. 

## **Procedure:** 

Executed: 

ipconfig /all 

## **Observation:** 

The DNS Server entry showed: 

DNS Servers . . . . . . . . . : 8.8.8.8 

## **Result:** 

The incorrect DNS configuration was identified. 

## **Root Cause** 

The Windows 11 client was configured to use: 

8.8.8.8 

as its DNS server. 

However, the Active Directory domain: 

mydomain.com 

is an internal/private domain whose DNS records are hosted by the Domain Controller at: 

172.16.0.1 

The client was therefore querying the wrong DNS server. 

## **Root Cause Identified:** 

The client's DNS server was incorrectly configured as 8.8.8.8 instead of the internal Domain Controller DNS server 172.16.0.1. 



<!-- Start of picture text -->
< - = oO x<br>Ethernet Properties x<br>—<br>Glens, Advanced network settings<br>Internet Protocol Version 4 (TCP/IPv4) Properties xX & Enapiea<br>iy General 216,642<br>|<br>a ow<br>Th = You can get IP settings assigned automatically if your network supports ted: 176,764<br>8 thisfor thecapability. appropriate Otherwise,IP settings.you need to ask your network administrator 1000 (Mbps)<br>8 00:09:42<br>& © Obtain an IP address automatically<br>O Use the following IP address:<br>| IP address: [a72.16.0 . 50 | seater came<br>Subnet mask: | 255. 255.255. 0 ,<br>Default gateway: Ear me properties<br>Obtain DNS server address automatically r options Edit<br>O Use the following DNS server addresses:<br>Preferred DNS server: [ 172.16. 0. J |<br>Alternate DNS server: | cos «= il<br>C\Validate settings upon exit Advanced... ttings ><br>very and sharing settings<br>x a<br><< erates ><br>an=~Qp~_~Bm e @Ceaoas> _ | & ~~ & CWM® géEnroae2:23 PM<br><!-- End of picture text -->

## **Part 5: Final Verification** 

## **Step 9: Testing DNS After the Fix** 

## **Test 1 – nslookup** 

Executed: nslookup mydomain.com 

## **Expected Output:** 

Server:  DC01.mydomain.com Address: 172.16.0.1 

Name:    mydomain.com Address: 172.16.0.1 

## **Observation:** 

The domain name was successfully resolved by the internal DNS server. 

## **Result:** 

## **DNS resolution restored successfully.** 

## **Test 2 – Ping Domain** 

Executed: 

ping mydomain.com 

## **Expected Output:** 

Pinging mydomain.com [172.16.0.1] with 32 bytes of data: 

Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 Reply from 172.16.0.1: bytes=32 time<1ms TTL=128 

## **Observation:** 

The hostname was successfully resolved to 172.16.0.1, and the Domain Controller responded to the ping. 

## **Result:** 

## **DNS and network connectivity were successfully restored.** 

## **Troubleshooting Summary** 

|**Challenge**|**Root Cause**|**Solution**|
|---|---|---|
|nslookup mydomain.com<br>failed|Client was using 8.8.8.8|Changed DNS to 172.16.0.1|
|ping mydomain.com failed|<sup>Domain name could not be</sup><br>resolved|Restored internal DNS|
|ping 172.16.0.1 worked|Network connectivity was<br>functioning|Confrmed issue was DNS,<br>not network|
|ipconfg /all showed wrong|<br>Incorrect IPv4 DNS<br>|Changed DNS server back to|
|DNS|confguration|172.16.0.1|



**Key Takeaways** 

## **Test What It Demonstrated** 

nslookup mydomain.com DNS name resolution ping mydomain.com DNS + network connectivity ping 172.16.0.1 Direct IP connectivity ipconfig /all DNS and network configuration 8.8.8.8 Incorrect DNS server for internal domain 172.16.0.1 Internal Active Directory DNS server 

## **Important Troubleshooting Logic** 

The most important part of this lab was comparing the results: 

ping 172.16.0.1 

↓ 

✅ 

Network connectivity works 

ping mydomain.com 

↓ 

✅ 

Hostname resolution fails 

nslookup mydomain.com 

↓ 

✅ 

DNS resolution fails 

Therefore: 

## **The network was working, but DNS resolution was broken.** 

This is a useful troubleshooting methodology because it prevents incorrectly blaming the network when the actual issue is DNS configuration. 

## **Skills Demonstrated** 

- DNS Troubleshooting 

- Active Directory DNS 

- Windows Server Administration 

- Windows 11 Administration 

- Network Troubleshooting 

- DNS Configuration 

- nslookup 

- ping 

- ipconfig /all 

- Root Cause Analysis 

- Break-and-Fix Troubleshooting 

- Domain Name Resolution 

- Network Diagnostics 

## **Conclusion** 

This lab provided practical experience with **DNS troubleshooting in a Windows Server Active Directory environment** . 

The DNS configuration was first verified to establish a working baseline. The Windows 11 client's DNS server was then intentionally changed from the internal Domain Controller (172.16.0.1) to the public DNS server (8.8.8.8), resulting in failed resolution of the internal mydomain.com domain. 

Through the use of **nslookup, ping, and ipconfig /all** , the issue was isolated to DNS rather than general network connectivity. The root cause was identified as an incorrect DNS server configuration on the Windows 11 client. 

The DNS configuration was restored to 172.16.0.1, after which domain name resolution and connectivity were successfully verified. 

The lab strengthened practical skills in **DNS troubleshooting, network diagnostics, root-cause analysis, and Active Directory administration** , which are valuable for **SOC Analysts, IAM Analysts, and System Administrators** . 

