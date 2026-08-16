**Active Directory Lab 11**

**Wireshark Packet Capture – Installation, Configuration, and Practical Implementation**

**Objective**

The objective of this lab was to capture and analyze network traffic using Wireshark in a Windows Server Active Directory environment. The lab involved installing Wireshark on the Domain Controller, capturing DNS queries, Kerberos authentication traffic, and LDAP queries. The goal was to understand how network protocols work at the packet level and to develop packet analysis skills essential for SOC and IAM roles.

**Lab Environment**

| Component | Details |
|---------------------------|-----------------------------------------|
| Operating System (DC) | Windows Server 2019 (Domain Controller) |
| Operating System (Client) | Windows 11 Pro |
| Virtualization | Oracle VirtualBox |
| Domain | [mydomain.com](https://mydomain.com/) |
| DC IP Address | 172.16.0.1 |
| Client IP Address | 172.16.0.50 |
| Tool Used | Wireshark 4.6.7 with Npcap |
| Capture Interface | Internal Network (172.16.0.1) |

**Part 1: Installation Challenges and Solutions**

**Challenge 1: Wireshark Installation on DC-Server**

**Issue:**\
Wireshark needed to be installed on the DC-Server to capture traffic on the Internal Network. However, the DC-Server was initially configured with only an Internal Network adapter (Adapter 2) and did not have internet access to download the installer.

**Initial Attempt:**

- Tried to download Wireshark directly on DC-Server using Microsoft Edge.

- The browser displayed a "No Internet" error message.

**Root Cause:**\
The DC-Server had only one active network interface (Internal Network, 172.16.0.1) and no NAT adapter for internet connectivity. The Internal Network is isolated and does not provide internet access.

**Challenge 2: Shared Folder Setup for File Transfer**

**Issue:**\
While the NAT adapter provided internet access, the initial approach was to transfer the Wireshark installer from the host laptop to the DC-Server using a shared folder. However, accessing the shared folder failed with the error:

text

Windows cannot access \\VBOXSVR\Shared_VM

**Root Cause:**\
VirtualBox Guest Additions were not installed on the DC-Server. Without Guest Additions, shared folders, mouse integration, and screen resizing do not work.

**Solution:**\
VirtualBox Guest Additions were installed on the DC-Server.

**Procedure:**

1. In the DC-Server VM window, clicked **Devices** → **Insert Guest Additions CD image**.

2. Opened File Explorer → Opened the **CD Drive** (VirtualBox Guest Additions).

3. Double-clicked VBoxWindowsAdditions.exe to run the installer.

4. Followed the installation wizard → Clicked **Next** → **Next** → **Install**.

5. After installation, clicked **Finish** and **Restarted** the VM.

**Post-Installation:**

1. After restart, opened File Explorer.

2. Typed \\VBOXSVR\Shared_VM in the address bar.

3. The shared folder opened successfully, showing the Wireshark installer.

**Result:**\
Shared folder access was successfully established. The Wireshark installer was available on the DC-Server.

**Challenge 3: Npcap Installation Prompt**

**Issue:**\
During Wireshark installation, a component selection screen appeared but did not immediately show the Npcap installation option.

**Observation:**\
The Wireshark installer asks for component selection first. The Npcap prompt appears on the **next screen** after clicking "Next".

**Solution:**\
Proceeded with the installation steps:

1. **Components Selection:** Kept default options (TShark, External capture tools) → Clicked **Next**.

2. **Npcap Installation:** The installer displayed a checkbox for **"Install Npcap"**. Ensured this was **checked**.

3. **Npcap Installation Options:** When the Npcap installer appeared, selected:

 - ✅ **Install Npcap in WinPcap API-compatible Mode**

 - ❌ **Restrict Npcap driver's access to Administrators only** (left unchecked)

 - ❌ **Support raw 802.11 traffic** (left unchecked)

4. Clicked **Install** → Completed the installation.

5. **Restarted** the DC-Server.

**Result:**\
Wireshark with Npcap was successfully installed on the DC-Server.

**Challenge 4: Selecting the Correct Network Interface**

**Issue:**\
After opening Wireshark on the DC-Server, the list of interfaces included several options (Ethernet, Internal, Local Area Connection\*, etc.). It was unclear which interface would capture traffic between the DC and the Windows 11 client.

**Root Cause:**\
The DC-Server had two network interfaces:

- **Adapter 1 (NAT):** IP 10.0.2.15 (internet traffic — not useful for capturing client traffic).

- **Adapter 2 (Internal):** IP 172.16.0.1 (traffic to/from Win11-Client — the correct interface).

**Solution:**\
The interface with the 172.16.0.1 IP address was identified and selected.

**Procedure:**

1. In Wireshark, reviewed the list of available interfaces.

2. Identified the interface labeled **"Internal"** (or "Ethernet 2") with IP 172.16.0.1.

3. Double-clicked the interface to start capturing.

**Screenshot 5:** Wireshark Interface Selection Showing Internal Network

**Result:**\
The correct interface was selected, and live packet capture began successfully.

**Challenge 5: Capturing Only DNS Traffic**

**Issue:**\
During the initial capture, a large volume of packets (ARP, broadcast, multicast) was being captured, making it difficult to find specific DNS queries.

**Solution:**\
Applied Wireshark display filters to isolate specific traffic types.

**Procedure:**

1. To view DNS traffic only:

 - Typed dns in the filter bar → Pressed **Enter**.

2. To view the specific mydomain.com query:

 - Typed dns.qry.name == "mydomain.com" → Pressed **Enter**.

**Screenshot 6:** Wireshark Filtered for DNS Traffic

**Result:**\
DNS queries and responses were successfully isolated and analyzed.

**Part 2: Practical Implementation and Captures**

**Step 1: Capturing DNS Traffic**

**Procedure:**

1. Opened Wireshark on DC-Server.

2. Double-clicked the **Internal** interface (172.16.0.1) to start capture.

3. On Win11-Client, opened Command Prompt → Ran:

cmd

nslookup mydomain.com

4. Stopped the capture on DC-Server.

5. Applied filter: dns.qry.name == "mydomain.com".

**Captured Packets:**

| Packet | Source → Destination | Info |
|----|----|----|
| 736 | 172.16.0.50 → 172.16.0.1 | Standard query 0x0004 A [mydomain.com](https://mydomain.com/) |
| 737 | 172.16.0.1 → 172.16.0.50 | Standard query response 0x0004 A 172.16.0.1, A 10.0.2.15 |
| 738 | 172.16.0.50 → 172.16.0.1 | Standard query 0x0005 AAAA [mydomain.com](https://mydomain.com/) |
| 739 | 172.16.0.1 → 172.16.0.50 | Standard query response 0x0005 AAAA fd17:625c:f037:2:520e:e648:e656:bc7b |

**Observation:**

- The client sent a DNS query asking for mydomain.com.

- The DC responded with the IPv4 address 172.16.0.1 (and also returned 10.0.2.15, the NAT IP).

- The client also asked for IPv6 (AAAA), and the DC responded with a dynamically assigned IPv6 address.

**Result:**\
DNS traffic was successfully captured and analyzed. The query and response packets were clearly visible.

**Step 2: Analyzing a DNS Packet**

**Procedure:**

1. In Wireshark, double-clicked the **DNS Response** packet (Packet 737).

2. Expanded the **"Domain Name System (response)"** section.

3. Reviewed the following fields:

 - **Transaction ID:** 0x0004 (matches the query)

 - **Flags:** QR = 1 (Response), AA = 1 (Authoritative Answer)

 - **Questions:** mydomain.com (Type A)

 - **Answers:** mydomain.com → 172.16.0.1, mydomain.com → 10.0.2.15

**Observation:**

- The Transaction ID in the response matched the query, confirming this was the correct response.

- The AA (Authoritative Answer) flag was set, meaning the DC was authoritative for the zone.

- Multiple A records were returned for the domain.

**Result:**\
DNS packet analysis was successfully completed. The structure of a DNS response was understood.

**Step 3: Capturing Kerberos (Login) Traffic**

**Procedure:**

1. Started a new capture on the **Internal** interface.

2. On Win11-Client, logged out (Start Menu → User Icon → Sign out).

3. Logged back in as mydomain\john.doe (password: P@ssw0rd123).

4. Stopped the capture on DC-Server.

5. Applied filter: kerberos. 

**Captured Kerberos Packets:**

| Packet Type | Description |
|-------------|-------------------------------------------------|
| **AS-REQ** | Client requests authentication ticket from DC |
| **AS-REP** | DC responds with a Ticket Granting Ticket (TGT) |
| **TGS-REQ** | Client requests service access ticket |
| **TGS-REP** | DC grants service access ticket |

**Observation:**

- The entire Kerberos authentication exchange was visible.

- The AS-REQ/AS-REP exchange handles initial authentication and TGT issuance.

- The TGS-REQ/TGS-REP exchange handles service-specific authorization.

**Result:**\
Kerberos authentication traffic was successfully captured and analyzed.

**Screenshot 9:** Kerberos Traffic (AS-REQ, AS-REP, TGS-REQ, TGS-REP) 

**Step 4: Capturing LDAP Traffic**

**Procedure:**

1. Started a new capture on the **Internal** interface.

2. On Win11-Client, opened **Active Directory Users and Computers**.

3. Browsed through the OU structure (\_EMPLOYEES, IT, HR, Sales).

4. Stopped the capture on DC-Server.

5. Applied filter: ldap. 

**Captured LDAP Packets:**

| Packet Type | Description |
|-----------------------|-----------------------------------------|
| **bindRequest** | Client authenticates to the LDAP server |
| **bindResponse** | Server confirms authentication |
| **searchRequest** | Client asks for directory information |
| **searchResultEntry** | Server returns the requested entries |
| **searchResultDone** | Server signals search completion |

**Observation:**

- Each time an OU or user was clicked in ADUC, an LDAP query was sent.

- The DC responded with the requested directory information.

- The searchRequest included the filter criteria (e.g., (&(objectClass=user)(objectCategory=person))).

**Result:**\
LDAP traffic was successfully captured and analyzed.

**Step 5: Saving the PCAP File**

**Procedure:**

1. In Wireshark, clicked **File** → **Save As**.

2. Named the file: Day11_DNS_Kerberos_LDAP.pcap.

3. Saved to: C:\Users\Administrator\Desktop\\

4. Clicked **Save**.

**Result:**\
The PCAP file was successfully saved. This file serves as proof of work and can be used for further analysis.

**Troubleshooting Summary**

| Challenge | Root Cause | Solution |
|----|----|----|
| Shared folder access denied | Guest Additions not installed | Installed VirtualBox Guest Additions |
| Correct interface not visible | Multiple interfaces listed | Selected the interface with IP 172.16.0.1 (Internal) |
| Too many packets captured | No filter applied | Used dns, kerberos, ldap, and dns.qry.name == "mydomain.com" filters |
| DNS query not appearing | Filter didn't match | Used specific filter for mydomain.com |

**Key Takeaways**

| Protocol | What I Captured | Why It Matters |
|----|----|----|
| **DNS** | Query and response for mydomain.com | Demonstrates name resolution in AD |
| **Kerberos** | AS-REQ, AS-REP, TGS-REQ, TGS-REP | Shows how authentication works in AD |
| **LDAP** | Search requests for OUs and users | Shows how AD queries work |

**Conclusion**

This lab provided practical experience with **Wireshark packet capture and analysis** in a Windows Server Active Directory environment. Wireshark was successfully installed on the Domain Controller after adding a NAT adapter and installing Guest Additions for shared folder access. The installation process included installing Npcap for packet capture capabilities.

Packet captures were performed for **DNS**, **Kerberos**, and **LDAP** traffic. The DNS capture demonstrated how clients resolve domain names to IP addresses. The Kerberos capture illustrated the authentication flow (AS-REQ, AS-REP, TGS-REQ, TGS-REP). The LDAP capture showed how directory queries are performed when browsing Active Directory Users and Computers.

The challenges faced during installation (internet connectivity, shared folder access, and Npcap installation) provided valuable troubleshooting experience. The ability to capture and analyze network traffic is an essential skill for **IAM Analysts, SOC Analysts, and System Administrators** responsible for maintaining secure and reliable enterprise environments.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_10_1.png)

![Screenshot 2](IAM_Lab_10_2.png)

![Screenshot 3](IAM_Lab_10_3.png)

![Screenshot 4](IAM_Lab_10_4.png)

![Screenshot 5](IAM_Lab_10_5.png)

![Screenshot 6](IAM_Lab_10_6.png)

