**Active Directory Lab 08**

**DHCP Configuration and IP Address Assignment – Practical Implementation & Troubleshooting**

**Objective**

The objective of this lab was to understand the operation of the Dynamic Host Configuration Protocol (DHCP) in a Windows Server environment. The lab involved installing the DHCP Server role, configuring a scope, reviewing DHCP address allocation, verifying client leases, releasing and renewing IP addresses, and observing APIPA behavior when the DHCP service was unavailable. Since the Windows 11 client was already configured with a static IP address, the lab also covered switching from a static configuration to DHCP-based addressing.

**Lab Environment**

| Component | Details |
|----|----|
| Operating System | Windows Server 2019 (Domain Controller) |
| Client Machine | Windows 11 Pro |
| Virtualization | Oracle VirtualBox |
| Domain | [mydomain.com](https://mydomain.com/) |
| DHCP Server | Windows Server (Role Installed) |
| DHCP Address Range | 172.16.0.100 – 172.16.0.200 |
| Client Initial State | Static IP Address (172.16.0.50) |
| Tools Used | DHCP Manager, Server Manager, Command Prompt, Services Console |

**Step 1: Installing the DHCP Server Role**

The DHCP Server role was not installed by default on the Domain Controller. To begin the lab, the role had to be added through Server Manager.

**Procedure:**

1. Server Manager → **Add roles and features**.

2. Selected **Role-based or feature-based installation**.

3. Selected the server (DC-Server) from the server pool.

4. From the Server Roles list, checked **DHCP Server**.

5. A pop-up appeared asking to add required features — clicked **Add Features**.

6. Clicked **Next** through the remaining screens.

7. On the Confirmation page, clicked **Install**.

8. Installation completed successfully.

**Post-Installation Configuration:**

1. After installation, a yellow notification flag appeared in Server Manager.

2. Clicked **Complete DHCP configuration**.

3. Clicked **Next** → **Commit** → **Close**.

**Authorization:**

1. Opened DHCP Manager (Server Manager → Tools → DHCP).

2. Right-clicked the server → **Authorize**.

3. Right-clicked again → **Refresh**.

4. The server showed a green checkmark, indicating it was authorized.

**Result:**\
The DHCP Server role was successfully installed and authorized on the Domain Controller. The server was now ready to lease IP addresses to clients.

**Step 2: Creating the DHCP Scope**

A scope defines the range of IP addresses that the DHCP server can assign to clients. Since a scope did not exist, one had to be created.

**Procedure:**

1. In DHCP Manager, expanded the server → right-clicked **IPv4** → **New Scope**.

2. Clicked **Next** on the welcome screen.

3. **Scope Name:** Internal Network. 

4. **IP Address Range:**

 - Start IP: 172.16.0.100

 - End IP: 172.16.0.200

 - Length: 24 (Subnet mask: 255.255.255.0) 

5. Clicked **Next** (no exclusions were added).

6. **Lease Duration:** Set to **1 day** (default is 8 days).

7. **Configure DHCP Options:** Selected **Yes, I want to configure these options now**.

8. **Router (Default Gateway):** Entered 172.16.0.1 → Clicked **Add** → **Next**. 

9. **Domain Name and DNS Servers:**

 - Parent domain: mydomain.com

 - Server name: DC01

 - IP address: 172.16.0.1 (ensured it was added to the list) 

10. Clicked **Next** (skipped WINS Servers).

11. **Activate Scope:** Selected **Yes, I want to activate this scope now**.

12. Clicked **Next** → **Finish**.

**Result:**\
The DHCP scope was successfully created and activated with an IP address range of 172.16.0.100 to 172.16.0.200.

**Step 3: Reviewing DHCP Configuration and Address Pool**

The DHCP Manager console was opened on the Domain Controller through Server Manager → Tools → DHCP. The configured IPv4 scope was expanded to review the available address pool.

The DHCP scope was configured with the following address range:

| Setting | Value |
|----------------|---------------|
| Start IP | 172.16.0.100 |
| End IP | 172.16.0.200 |
| Subnet Mask | 255.255.255.0 |
| Lease Duration | 1 Day |

This address pool provides IP addresses that can be dynamically assigned to client machines on the network.

**Result:**\
The DHCP scope and configured IP address range were successfully reviewed.

**Screenshot 1:** DHCP IPv4 Scope and Address Pool

**Step 4: Switching Client from Static IP to DHCP**

The Windows 11 client was initially configured with a static IP address (172.16.0.50) to ensure network connectivity during the initial lab setup. To test DHCP functionality, the client had to be switched to DHCP mode.

**Procedure:**

1. On Win11-Client, opened **Network Settings**.

2. Navigated to **Advanced network settings** → **More network adapter options**.

3. Right-clicked the Ethernet adapter → **Properties**.

4. Selected **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.

5. Changed from **Use the following IP address** to **Obtain an IP address automatically**.

6. Changed from **Use the following DNS server addresses** to **Obtain DNS server address automatically**.

7. Clicked **OK** → **Close**.

**Result:**\
The client was now configured to obtain its IP address automatically from the DHCP server.

**Step 5: Verifying Current DHCP Leases**

The Address Leases section within DHCP Manager was examined to identify the IP addresses currently assigned to client machines.

**Procedure:**

1. In DHCP Manager, expanded **IPv4** → expanded **Scope** → clicked **Address Leases**.

2. The Windows 11 client appeared in the lease list with an IP address belonging to the configured DHCP range.

**Result:**\
The Windows 11 client was successfully identified in the DHCP Address Leases section with an address from the configured pool. The client was now receiving its network configuration dynamically.

**Screenshot 2:** DHCP Address Lease for Windows 11 Client

**Step 6: Testing DHCP Address Assignment from the Client**

The DHCP functionality was tested from the Windows 11 client using the Command Prompt. The current network configuration was first reviewed using ipconfig /all.

**Procedure:**

1. Opened Command Prompt as Administrator on Win11-Client.

2. Ran: ipconfig /all to view the current IP configuration.

 - The client showed an IP in the 172.16.0.100 – 172.16.0.200 range. 

3. Ran: ipconfig /release to release the DHCP lease.

 - The IP address was removed (0.0.0.0 appeared).

4. Ran: ipconfig /renew to request a new IP address.

 - The client sent a DHCP Discover request.

 - The DHCP server responded with a DHCP Offer.

 - The client requested the offered IP.

 - The server acknowledged the request.

5. Ran: ipconfig /all again to verify the new IP address.

**Result:**\
The Windows 11 client successfully obtained an IP address within the configured 172.16.0.100 – 172.16.0.200 DHCP range. The ipconfig /release and /renew commands worked successfully.

**Step 7: Verifying the Updated DHCP Lease**

After renewing the IP address on the client, the Address Leases section in DHCP Manager was refreshed on the Domain Controller.

**Procedure:**

1. In DHCP Manager, right-clicked **Address Leases** → **Refresh**.

2. The Windows 11 client appeared with its current DHCP lease information.

3. The lease expiration information was reviewed.

**Result:**\
The renewed DHCP lease was successfully displayed in DHCP Manager.

**Screenshot 4:** Updated DHCP Lease Information

**Step 8: Simulating DHCP Server Failure**

To understand how a client behaves when a DHCP server becomes unavailable, the DHCP Server service was temporarily stopped on the Domain Controller.

**Procedure:**

1. On DC-Server, opened **Services** (Start Menu → services.msc).

2. Found **DHCP Server** in the list.

3. Right-clicked → **Stop**.

4. On Win11-Client, ran:

 - ipconfig /release (removed the current IP)

 - ipconfig /renew (attempted to get a new IP)

5. Since the DHCP server was unavailable, the client could not obtain an address from the configured DHCP pool.

6. The client automatically assigned itself an address from the 169.254.x.x range. This behavior is known as **APIPA (Automatic Private IP Addressing)**.

**Result:**\
The Windows 11 client received a 169.254.x.x address after the DHCP server became unavailable, successfully demonstrating APIPA behavior.

**Step 9: Restoring DHCP Service**

The DHCP Server service was started again on the Domain Controller to restore DHCP functionality.

**Procedure:**

1. On DC-Server, opened **Services**.

2. Found **DHCP Server** → Right-clicked → **Start**.

3. On Win11-Client, ran: ipconfig /renew.

4. The client successfully received an IP address from the configured DHCP scope.

**Result:**\
The client recovered from the APIPA address and successfully obtained a valid 172.16.0.x address from the DHCP server.

**Screenshot 6:** Client IP Address After DHCP Service Restoration

**Troubleshooting and Challenges Faced**

| Challenge | Solution |
|----|----|
| DHCP Server role not installed | Added the DHCP Server role through Server Manager → Add roles and features. |
| Authorization required after installation | Right-clicked server in DHCP Manager → Authorize → Refresh. |
| Client not receiving DHCP address | Switched client from static IP to "Obtain an IP address automatically". |
| DHCP server not responding | Checked Services → DHCP Server service was stopped → Restarted it. |
| Address Leases not showing updated IP | Refreshed the Address Leases view in DHCP Manager. |

**Key Takeaways**

| Concept | What I Learned |
|----|----|
| DHCP Installation | The DHCP Server role must be manually installed—it does not come pre-installed. |
| Scope Creation | A scope must be defined before clients can receive IP addresses. |
| Authorization | DHCP servers must be authorized in Active Directory before they can issue leases. |
| Static to DHCP | Clients can be switched from static to DHCP configuration through network settings. |
| ipconfig Commands | ipconfig /release and /renew are essential for DHCP troubleshooting. |
| APIPA | When DHCP is unavailable, clients self-assign a 169.254.x.x address. |
| Service Recovery | Restarting the DHCP Server service restores DHCP functionality. |

**Conclusion**

This lab provided practical experience with **DHCP installation, configuration, dynamic IP address assignment, lease management, and troubleshooting** in a Windows Server environment. The DHCP server role was installed and authorized, and a scope was created with an address range of 172.16.0.100 to 172.16.0.200. The Windows 11 client was switched from a static IP to DHCP and successfully obtained an IP address dynamically. The release and renewal process demonstrated how clients request and receive new DHCP leases. The lab also simulated DHCP server failure, resulting in an APIPA 169.254.x.x address, and demonstrated successful network recovery after the DHCP service was restored. This exercise reinforced the importance of DHCP in automating network configuration and maintaining reliable IP address management in enterprise networks.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_08_1.png)

![Screenshot 2](IAM_Lab_08_2.png)

![Screenshot 3](IAM_Lab_08_3.png)

![Screenshot 4](IAM_Lab_08_4.png)

![Screenshot 5](IAM_Lab_08_5.png)

![Screenshot 6](IAM_Lab_08_6.png)

