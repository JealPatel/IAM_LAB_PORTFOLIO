# **Networking Lab 13** 

# **Subnetting Hands-On – Network Range and Subnet Mask Analysis** 

# **Objective** 

The objective of this lab was to understand the fundamentals of IPv4 subnetting by calculating network ranges, network addresses, broadcast addresses, usable IP addresses, subnet masks, and the total number of addresses for different CIDR prefixes. 

**DC-Server** and **Win11-** The lab also involved verifying the subnet configuration of the **Client** using ipconfig /all and practicing subnetting calculations using /24 and /8 networks. 

# **Lab Environment** 

**Component Details** Domain Controller DC-Server Client Machine Win11-Client Domain mydomain.com DC IPv4 Address 172.16.0.1 Client IPv4 Address 172.16.0.50 or an address within the range Subnet Mask 255.255.255.0 /24 CIDR Prefix Command Used ipconfig /all 

# **Part 1: Calculate Network Range for 172.16.0.0/24** 

# **Step 1: Determine the Network Information** 

The network used for the lab is: 

172.16.0.0/24 

The /24 CIDR prefix means that the first 24 bits are used for the network portion, leaving 8 bits for hosts. 

# **Subnetting Calculation** 

CIDR:        /24 

Subnet Mask: 255.255.255.0 

Host Bits:   8 

Total IPs:   2⁸ = 256 

Usable IPs:  256 - 2 = 254 

Two addresses are reserved: 

- Network address 

- Broadcast address 

# **Network Details** 

**Parameter Value** IP Range 172.16.0.0 – 172.16.0.255 Network Address 172.16.0.0 Broadcast Address 172.16.0.255 Usable IPs 172.16.0.1 – 172.16.0.254 Subnet Mask 255.255.255.0 Total IPs 256 Usable IPs 254 

# **Observation** 

The /24 network provides **256 total addresses** , of which **254 can be assigned to hosts** . 

# **Part 2: Comparing /24 with /16** 

# **Step 2: What If We Used 172.16.0.0/16?** 

The same private IP range can be represented using a /16 prefix: 

172.16.0.0/16 

The subnet mask becomes: 255.255.0.0 There are now 16 host bits. 

# **Calculation** 

Host Bits = 32 - 16 

= 16 

Total IPs = 2¹⁶ 

= 65,536 

Usable IPs = 65,536 - 2 

= 65,534 

# **Network Details** 

**Parameter Value** IP Range 172.16.0.0 – 172.16.255.255 Network Address 172.16.0.0 Broadcast Address 172.16.255.255 Usable IPs 172.16.0.1 – 172.16.255.254 Subnet Mask 255.255.0.0 Total IPs 65,536 Usable IPs 65,534 

**Observation** 

Changing from /24 to /16 significantly increases the number of available host addresses. 

# **Part 3: Verify Subnet Mask on DC-Server** 

# **Step 3: Check Network Configuration** 

# **Procedure** 

# On **DC-Server** : 

1. Open **Command Prompt** . 

2. Execute: 

ipconfig /all 

3. Locate the network adapter information. 

4. Verify the IPv4 address and subnet mask. 

# **Expected Configuration** 

IPv4 Address:  172.16.0.1 

Subnet Mask:   255.255.255.0 

# **Observation** 

The subnet mask 255.255.255.0 corresponds to: 

/24 

# **Result** 

The Domain Controller is configured on the 172.16.0.0/24 network. 

**Part 4: Verify Subnet Mask on Win11-Client** 

# **Step 4: Check Client Network Configuration** 

# **Procedure** 

# On **Win11-Client** : 

1. Open **Command Prompt** . 

2. Execute: 

ipconfig /all 

3. Locate the Ethernet adapter. 

4. Check the IPv4 address and subnet mask. 

# **Expected Configuration** 

IPv4 Address:  172.16.0.50 

Subnet Mask:   255.255.255.0 

The client's IP may also be another address within the same /24 range. 

# **Observation** 

The subnet mask is: 255.255.255.0 

which corresponds to: 

/24 

# **Result** 

The Win11-Client is configured within the same 172.16.0.0/24 network as the Domain Controller. 

# **Part 5: Practice Subnetting Calculations** 

# **Step 5: 192.168.1.0/24** 

# **Network Address** 

192.168.1.0/24 

**Answer:** 

192.168.1.0 

# **Broadcast Address** 

**Answer:** 

192.168.1.255 

# **Usable IP Range** 

**Answer:** 

192.168.1.1 – 192.168.1.254 

# **Step 6: 10.0.0.0/8** 

**Network Address** 

10.0.0.0/8 

# **Answer:** 

10.0.0.0 

**Broadcast Address** 

**Answer:** 

10.255.255.255 

# **Usable IP Range** 

# **Answer:** 

10.0.0.1 – 10.255.255.254 

# **Subnetting Practice Summary** 

# **Exercise** 

# **Answer** 

192.168.1.0/24 Network Address 192.168.1.0 

192.168.1.0/24 Broadcast Address 192.168.1.255 192.168.1.0/24 Usable IPs 192.168.1.1 – 192.168.1.254 10.0.0.0/8 Network Address 10.0.0.0 10.0.0.0/8 Broadcast Address 10.255.255.255 10.0.0.0/8 Usable IPs 10.0.0.1 – 10.255.255.254 

# **Subnet Mask Reference** 

# **CIDR Subnet Mask Total IPs Usable IPs** 

/8 255.0.0.0 16,777,216 16,777,214 /16 255.255.0.0 65,536 65,534 /24 255.255.255.0 256 254 

# **Key Takeaways** 

# **1. CIDR Prefix** 

The CIDR prefix indicates how many bits belong to the network portion. 

For example: 

172.16.0.0/24 

means: 

Network bits = 24 

Host bits    = 8 

# **2. Subnet Mask** 

For /24: 

255.255.255.0 

For /16: 

255.255.0.0 

For /8: 255.0.0.0 

# **3. Total IP Calculation** 

The basic formula used is: Total IPs = 2^(Host Bits) For /24: Host Bits = 32 - 24 

Total = 2⁸ = 256 

# **4. Usable IP Calculation** 

For a traditional IPv4 subnet: Usable IPs = Total IPs - 2 

The two reserved addresses are: 

Network Address 

Broadcast Address 

Therefore: 

256 - 2 = 254 usable IPs 

# **Skills Demonstrated** 

- IPv4 Addressing 

- CIDR Notation 

- Subnetting 

- Network Address Calculation 

- Broadcast Address Calculation 

- Usable IP Range Calculation 

- Subnet Mask Identification 

- Network Configuration Analysis 

- ipconfig /all 

- Basic Network Troubleshooting 

- Network Address Planning 

# **Conclusion** 

This lab provided hands-on practice with **IPv4 subnetting and network addressing** . The network ranges for /24 and /16 were calculated, including their network addresses, broadcast addresses, subnet masks, and usable IP ranges. 

**DC-Server** and **Win11-Client** The subnet configuration of both the was then verified using ipconfig /all. Finally, subnetting calculations were practiced using 192.168.1.0/24 and 10.0.0.0/8. 

The lab strengthened the understanding of **CIDR notation, subnet masks, host bits, network addressing, and IP range calculations** , which are fundamental networking concepts for cybersecurity and SOC-related work. 

