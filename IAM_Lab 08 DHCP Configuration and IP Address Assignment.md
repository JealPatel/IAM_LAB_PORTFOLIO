# **Active Directory Lab 08** 

# **DHCP Configuration and IP Address Assignment – Practical Implementation & Troubleshooting** 

# **Objective** 

The objective of this lab was to understand the operation of the Dynamic Host Configuration Protocol (DHCP) in a Windows Server environment. The lab involved installing the DHCP Server role, configuring a scope, reviewing DHCP address allocation, verifying client leases, releasing and renewing IP addresses, and observing APIPA behavior when the DHCP service was unavailable. Since the Windows 11 client was already configured with a static IP address, the lab also covered switching from a static configuration to DHCP-based addressing. 

# **Lab Environment** 

|Component|Details|
|---|---|
|Operating System|Windows Server 2019 (Domain Controller)|
|Client Machine|Windows 11 Pro|
|Virtualization|Oracle VirtualBox|
|Domain|mydomain.com|
|DHCP Server|Windows Server (Role Installed)|
|DHCP Address Range|172.16.0.100 – 172.16.0.200|
|Client Initial State|Static IP Address (172.16.0.50)|
|Tools Used|DHCP Manager, Server Manager, Command Prompt, Services Console|



# **Step 1: Installing the DHCP Server Role** 

The DHCP Server role was not installed by default on the Domain Controller. To begin the lab, the role had to be added through Server Manager. 

# **Procedure:** 

1. Server Manager → **Add roles and features** . 

2. Selected **Role-based or feature-based installation** . 

3. Selected the server (DC-Server) from the server pool. 

4. From the Server Roles list, checked **DHCP Server** . 

5. A pop-up appeared asking to add required features — clicked **Add Features** . 

6. Clicked **Next** through the remaining screens. 

7. **Install** . On the Confirmation page, clicked 

8. Installation completed successfully. 

# **Post-Installation Configuration:** 

1. After installation, a yellow notification flag appeared in Server Manager. 

2. Clicked . **Complete DHCP configuration** 

3. Clicked **Next** → **Commit** → **Close** . 

# **Authorization:** 

1. Opened DHCP Manager (Server Manager → Tools → DHCP). 

2. Right-clicked the server → **Authorize** . 

3. Right-clicked again → **Refresh** . 

4. The server showed a green checkmark, indicating it was authorized. 

# **Result:** 

The DHCP Server role was successfully installed and authorized on the Domain Controller. The server was now ready to lease IP addresses to clients. 



<!-- Start of picture text -->
2<br>File Action View Help<br>@=| wiz a|B ml a<br>‘@ DHCP Actions<br>vjv deOt.mydomepi rid Add a Scope IP a<br>i]3 ServerPolicie)| Acopescopebeforeis a rangedynamtofPtNew Scope Wizard eg More Actions »<br>Hi Filters<br>& IPv6 Toaddanewscope,, Scope Name<br>‘You have to provide an identifying scope name. You also have the option of providing<br>For more informatio! a description<br>Type a name and description for this scope. This information helps you quickly identify<br>how the scope is to be used on your network.<br>Name Intemal Network<br>Description: __ [IP Range For Lab Clients 7<br><Back Cancel<br>Ry 5<br>== 0Om:aiA @€@ zB J DAs syn2:17PM WH<br><!-- End of picture text -->



<!-- Start of picture text -->
File Action View Help<br>e>\anmi\5 Sib mia<br>‘@ DHCP Actions<br>v vEE dcOl.mydomepina ri) Add a Scope pv ras<br>4 Server Acscopeis a range offto= dose soe senna 4 ke cea aete n dae tneeae Mee ceca cee adietre More Actions ,<br>| Policie|) scope before dynami New Scope Wizard<br>Bb ®veFilters To add anew scope,| IP Address Range<br>‘You define the scope address range by identifying a set of consecutive IP addresses<br>For more informatio<br>Configuration settings for DHCP Server<br>Enter the range of addresses that the scope distibutes<br>StatIP address: [172. 16. 0 . 100<br>EndIP address: [172. 16. 0 . 200<br>Configuration settings that propagate to DHCP Client<br>Lenath as<br>Subnet mask: [255. 255. 255. 0<br><Back Cancel<br>«< ><br>=i? ©ye+* @ B z a © te gam2:18PM WY<br><!-- End of picture text -->



<!-- Start of picture text -->
File Action View Help<br>| Am 3 |B m| a<br>@ DHCP _ Actions<br>Y vHf de0l.mydomegia]"|a Server|| Ci)a scopeisAdda rangea Scopeof rea IPvaMore Actions a»<br>@ FiltersPolicie|| scope before dynamt New Scope Wizard<br>& Ive To add anew scope,| Router‘You (Defaultcan specityGateway)the routers, or default gateways, to be distibuted by this scope.<br>For more informatio<br>To add an IP address for a router used by clients, enter the address below.<br>IP address:<br>(|<br>1721604<br><Back Next > Cancel<br>< ><br>== 20SyBifl e@ wp & @ Me ay4/20262:20PM u<br><!-- End of picture text -->



<!-- Start of picture text -->
2<br>File Action View Help<br>e9\/2Rn/68|Eb alfa<br>@ pHcp Actions<br>Yjv deOt.mydomepia i)U Add a Scope ro .<br>a3s ServerPolMollcié|! Ascopescapebeforeis a rangedynamiofp}New Scope Wizard i a nt ere g More Actions »<br>HH Filters<br>% IPv6 To add anew scope,, Domain Name and DNS Servers<br>The Domain Name System (DNS) maps and translates domain names used by clients<br>For mare informatio on your network,<br>‘You can specify the parent domain you want the client computers on your network to use for<br>DNS name resolution.<br>Parent domain: |mydomain.com<br>To configure scope clients to use DNS servers on your network, enter the IP addresses for those<br>servers.<br>Server name IP address:<br>cot<br>Resolve 172.16.0.1<br><Back Cancel<br>« ><br>eaoreC@nmpkOo ®@ m Fal te yas2:21PM<br><!-- End of picture text -->

- 10.Clicked **Next** (skipped WINS Servers). 

# 11. **Activate Scope:** Selected **Yes, I want to activate this scope now** . 

12.Clicked **Next** → **Finish** . 

# **Result:** 

The DHCP scope was successfully created and activated with an IP address range of 172.16.0.100 to 172.16.0.200. 

# **Step 3: Reviewing DHCP Configuration and Address Pool** 

The DHCP Manager console was opened on the Domain Controller through Server Manager → Tools → DHCP. The configured IPv4 scope was expanded to review the available address pool. 

The DHCP scope was configured with the following address range: 

Setting Value Start IP 172.16.0.100 End IP 172.16.0.200 Subnet Mask 255.255.255.0 Lease Duration 1 Day 

This address pool provides IP addresses that can be dynamically assigned to client machines on the network. 

# **Result:** 

The DHCP scope and configured IP address range were successfully reviewed. 



<!-- Start of picture text -->
‘@ pHeP - x<br>File Action View Help<br>€9| 4m & & |B tl *<br>@vials, StartIP Address End IP Address Description Actions<br>v al £0172.16.0.100 172,16.0.200 Address range for distribution Address Pool a<br>v (1) Scope More Actions »<br>Bad<br>1% Adi<br>> (By Res<br>G Scc}<br>(j Pol<br>(3 Server<br>(5) Policie<br>> ® Filters<br>» ib iPv6<br><!-- End of picture text -->



<!-- Start of picture text -->
© © Administrator: Corymand Pro X + ov - o x<br>(c) Microsoft Corporation. All rights reserved.<br>C:\Users\Administrator>ipconfig /all<br>Windows IP Configuration<br>Host Name... ....... =. . : Winll-Client<br>Primary Dns Suffix ..... . . : mydomain.com<br>Node Type. ......... . . : Hybrid<br>IP Routing Enabled. ....... : No<br>WINS Proxy Enabled. ....... : No<br>DNS Suffix Search List. . . . . . : mydomain.com<br>Ethernet adapter Ethernet:<br>Connection-specific DNS Suffix .<br>Description. ...... .. .. : Intel(R) PRO/1000 MT Desktop Adapter<br>Physical Address. . ..... . . : 08-00-27-75-45-79<br>DHCP Enabled. ..........: No<br>Autoconfiguration Enabled... . : Yes<br>Link-local IPv6 Address .... . : fe80::4alce:51cd:e3bf:1521%10(Preferred)<br>IPv4 Address. ......... . : 172.16.0.50(Preferred)<br>Subnet Mask... ....... . : 255.255.255.0<br>Default Gateway ........ . : 172.16.0.1<br>DHCPv6 IAID.......... . : 84410407<br>DHCPv6 Client DUID. . ... . . . : 00-01-01-00-31-F8-44-BD-08-00-27-75-45-79<br>DNS Servers .......... . : 172.16.0.1<br>HE Q Search~ bue@a- ~ & CVM®© gs3:00 202AM<br><!-- End of picture text -->

3. Ran: ipconfig /release to release the DHCP lease. 

   - The IP address was removed (0.0.0.0 appeared). 

4. Ran: ipconfig /renew to request a new IP address. 

   - The client sent a DHCP Discover request. 

   - The DHCP server responded with a DHCP Offer. 

   - The client requested the offered IP. 

   - The server acknowledged the request. 

5. Ran: ipconfig /all again to verify the new IP address. 

# **Result:** 

The Windows 11 client successfully obtained an IP address within the configured 172.16.0.100 – 172.16.0.200 DHCP range. The ipconfig /release and /renew commands worked successfully. 

# **Step 7: Verifying the Updated DHCP Lease** 

After renewing the IP address on the client, the Address Leases section in DHCP Manager was refreshed on the Domain Controller. 

# **Procedure:** 

1. In DHCP Manager, right-clicked **Address Leases** → **Refresh** . 

2. The Windows 11 client appeared with its current DHCP lease information. 

3. The lease expiration information was reviewed. 

# **Result:** 

The renewed DHCP lease was successfully displayed in DHCP Manager. 

**Screenshot 4:** Updated DHCP Lease Information 

# **Step 8: Simulating DHCP Server Failure** 

To understand how a client behaves when a DHCP server becomes unavailable, the DHCP Server service was temporarily stopped on the Domain Controller. 

# **Procedure:** 

1. On DC-Server, opened **Services** (Start Menu → services.msc). 

2. Found **DHCP Server** in the list. 

3. Right-clicked → **Stop** . 

4. On Win11-Client, ran: 

   - ipconfig /release (removed the current IP) 

   - ipconfig /renew (attempted to get a new IP) 

5. Since the DHCP server was unavailable, the client could not obtain an address from the configured DHCP pool. 

6. The client automatically assigned itself an address from the 169.254.x.x range. This behavior is known as **APIPA (Automatic Private IP Addressing)** . 

# **Result:** 

The Windows 11 client received a 169.254.x.x address after the DHCP server became unavailable, successfully demonstrating APIPA behavior. 

# **Step 9: Restoring DHCP Service** 

The DHCP Server service was started again on the Domain Controller to restore DHCP functionality. 

# **Procedure:** 

1. On DC-Server, opened **Services** . 

2. Found **DHCP Server** → Right-clicked → **Start** . 

3. On Win11-Client, ran: ipconfig /renew. 

4. The client successfully received an IP address from the configured DHCP scope. 

# **Result:** 

The client recovered from the APIPA address and successfully obtained a valid 172.16.0.x address from the DHCP server. 

**Screenshot 6:** Client IP Address After DHCP Service Restoration 

# **Troubleshooting and Challenges Faced** 

Challenge Solution Added the DHCP Server role through Server Manager → DHCP Server role not installed Add roles and features. Authorization required after Right-clicked server in DHCP Manager → Authorize → installation Refresh. Client not receiving DHCP Switched client from static IP to "Obtain an IP address address automatically". Checked Services → DHCP Server service was stopped → DHCP server not responding Restarted it. Address Leases not showing Refreshed the Address Leases view in DHCP Manager. updated IP 

# **Key Takeaways** 

Concept What I Learned The DHCP Server role must be manually installed—it does not come DHCP Installation pre-installed. Scope Creation A scope must be defined before clients can receive IP addresses. DHCP servers must be authorized in Active Directory before they can Authorization issue leases. Clients can be switched from static to DHCP configuration through Static to DHCP network settings. ipconfig ipconfig /release and /renew are essential for DHCP troubleshooting. Commands 

Concept What I Learned 

APIPA When DHCP is unavailable, clients self-assign a 169.254.x.x address. Service Recovery Restarting the DHCP Server service restores DHCP functionality. 

# **Conclusion** 

This lab provided practical experience with **DHCP installation, configuration, dynamic IP address assignment, lease management, and troubleshooting** in a Windows Server environment. The DHCP server role was installed and authorized, and a scope was created with an address range of 172.16.0.100 to 172.16.0.200. The Windows 11 client was switched from a static IP to DHCP and successfully obtained an IP address dynamically. The release and renewal process demonstrated how clients request and receive new DHCP leases. The lab also simulated DHCP server failure, resulting in an APIPA 169.254.x.x address, and demonstrated successful network recovery after the DHCP service was restored. This exercise reinforced the importance of DHCP in automating network configuration and maintaining reliable IP address management in enterprise networks. 

