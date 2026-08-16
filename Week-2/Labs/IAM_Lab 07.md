**Active Directory Lab 07**

**Configuring and Testing DNS in Windows Server**

**Objective**

The objective of this lab was to understand the role of the **Domain Name System (DNS)** in an Active Directory environment. The lab involved creating a new **Host (A) record**, verifying forward and reverse DNS name resolution, and managing the DNS cache using command-line tools. This exercise demonstrated how DNS enables reliable communication between clients and servers within a Windows domain.

**Lab Environment**

| **Component** | **Details** |
|------------------|------------------------------------|
| Operating System | Windows Server (Domain Controller) |
| Client Machine | Windows 11 |
| Virtualization | VMware Workstation / VirtualBox |
| Domain | mydomain.com |
| Tool Used | DNS Manager, Command Prompt |

**Step 1: Opening DNS Manager**

The **DNS Manager** console was opened from **Server Manager** on the Domain Controller. The DNS server hosting the **mydomain.com** zone was accessed to manage DNS records used by the Active Directory environment.

**Result**

The DNS Manager console opened successfully, displaying the configured DNS server and its available DNS zones.

**Screenshot 1:** *DNS Manager Console*

**Step 2: Exploring the Forward Lookup Zone**

The **Forward Lookup Zones** section was expanded, and the **mydomain.com** zone was selected. Existing DNS records were reviewed, including the **A record** for the Domain Controller and the **Name Server (NS)** records responsible for handling DNS queries within the domain.

This step provided an overview of the existing DNS infrastructure supporting the Active Directory environment.

**Result**

The Forward Lookup Zone was successfully explored, and the existing DNS records were verified.

**Screenshot 2:** *Forward Lookup Zone Records*

**Step 3: Creating a New Host (A) Record**

A new **Host (A)** record named **test** was created within the **mydomain.com** forward lookup zone. The hostname was mapped to the IP address **172.16.0.1**, which corresponds to the Domain Controller. During creation, the option to automatically generate the corresponding **Pointer (PTR)** record was enabled.

This configuration allows the hostname **test.mydomain.com** to resolve to the specified IP address while also supporting reverse DNS lookups.

**Result**

The new **A record** and its associated **PTR record** were successfully created.

**Screenshot 3:** *New Host (A) Record Created*

**Step 4: Verifying Forward DNS Resolution**

The Windows 11 client machine was used to verify DNS functionality using the **nslookup** command. DNS queries were performed for both **test.mydomain.com** and **mydomain.com**.

The hostname successfully resolved to the IP address **172.16.0.1**, confirming that the newly created DNS record was functioning correctly.

**Result**

Forward DNS name resolution was successfully verified from the client machine.

**Screenshot 4:** *Forward DNS Resolution Using nslookup*

**Step 5: Managing the DNS Cache**

The local DNS cache on the client machine was examined using the **ipconfig /displaydns** command. The DNS cache was then cleared using **ipconfig /flushdns**, and the cache contents were viewed again to confirm that cached DNS entries had been removed.

This exercise demonstrated how cached DNS records can be viewed and refreshed to ensure that clients retrieve the latest DNS information.

**Result**

The DNS cache was successfully displayed, cleared, and verified after the cache flush operation.

**Screenshot 5:** *DNS Cache Management Commands* 

**Step 6: Verifying Reverse DNS Resolution**

A reverse DNS lookup was performed using the **nslookup** command with the IP address **172.16.0.1**. The query successfully returned the hostname **test.mydomain.com**, confirming that the automatically generated **PTR record** was functioning correctly.

This verified that reverse name resolution was properly configured within the DNS server.

**Result**

Reverse DNS resolution was successfully verified using the configured PTR record.

**Screenshot 6:** *Reverse DNS Lookup Result*

**Conclusion**

This lab provided practical experience in configuring and managing the **Domain Name System (DNS)** within an Active Directory environment. The Forward Lookup Zone was explored, and a new **Host (A) record** was successfully created along with its corresponding **PTR record**. DNS functionality was validated through forward and reverse name resolution using the **nslookup** utility. Additionally, DNS cache management was performed using **ipconfig** commands to demonstrate how cached records can be viewed and refreshed. Overall, this lab reinforced the critical role of DNS in supporting Active Directory services and ensuring reliable name resolution across the network.

## 📸 Screenshots

![Screenshot 1](IAM_Lab_07_1.png)

![Screenshot 2](IAM_Lab_07_2.png)

![Screenshot 3](IAM_Lab_07_3.png)

![Screenshot 4](IAM_Lab_07_4.png)

![Screenshot 5](IAM_Lab_07_5.png)

![Screenshot 6](IAM_Lab_07_6.png)

![Screenshot 7](IAM_Lab_07_7.png)

![Screenshot 8](IAM_Lab_07_8.png)

![Screenshot 9](IAM_Lab_07_9.png)

![Screenshot 10](IAM_Lab_07_10.png)

![Screenshot 11](IAM_Lab_07_11.png)

![Screenshot 12](IAM_Lab_07_12.png)

![Screenshot 13](IAM_Lab_07_13.png)

