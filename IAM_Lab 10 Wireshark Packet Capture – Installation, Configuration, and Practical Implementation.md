## **Active Directory Lab 11** 

## **Wireshark Packet Capture – Installation, Configuration, and Practical Implementation** 

## **Objective** 

The objective of this lab was to capture and analyze network traffic using Wireshark in a Windows Server Active Directory environment. The lab involved installing Wireshark on the Domain Controller, capturing DNS queries, Kerberos authentication traffic, and LDAP queries. The goal was to understand how network protocols work at the packet level and to develop packet analysis skills essential for SOC and IAM roles. 

## **Lab Environment** 

Component Details Operating System (DC) Windows Server 2019 (Domain Controller) Operating System (Client) Windows 11 Pro Virtualization Oracle VirtualBox Domain <u>mydomain.com</u> DC IP Address 172.16.0.1 Client IP Address 172.16.0.50 Tool Used Wireshark 4.6.7 with Npcap Capture Interface Internal Network (172.16.0.1) 

## **Part 1: Installation Challenges and Solutions** 

## **Challenge 1: Wireshark Installation on DC-Server** 

## **Issue:** 

Wireshark needed to be installed on the DC-Server to capture traffic on the Internal Network. However, the DC-Server was initially configured with only an Internal Network adapter (Adapter 2) and did not have internet access to download the installer. 

## **Initial Attempt:** 

- Tried to download Wireshark directly on DC-Server using Microsoft Edge. 

- The browser displayed a "No Internet" error message. 

## **Root Cause:** 

The DC-Server had only one active network interface (Internal Network, 172.16.0.1) and no NAT adapter for internet connectivity. The Internal Network is isolated and does not provide internet access. 

## **Challenge 2: Shared Folder Setup for File Transfer** 

## **Issue:** 

While the NAT adapter provided internet access, the initial approach was to transfer the Wireshark installer from the host laptop to the DC-Server using a shared folder. However, accessing the shared folder failed with the error: 

text 

Windows cannot access \\VBOXSVR\Shared_VM 

## **Root Cause:** 

VirtualBox Guest Additions were not installed on the DC-Server. Without Guest Additions, shared folders, mouse integration, and screen resizing do not work. 

## **Solution:** 

VirtualBox Guest Additions were installed on the DC-Server. 

## **Procedure:** 

1. In the DC-Server VM window, clicked **Devices** → **Insert Guest Additions CD image** . 

2. Opened File Explorer → Opened the **CD Drive** (VirtualBox Guest Additions). 

3. Double-clicked VBoxWindowsAdditions.exe to run the installer. 

4. Followed the installation wizard → Clicked **Next** → **Next** → **Install** . 

5. After installation, clicked **Finish** and **Restarted** the VM. 

## **Post-Installation:** 

1. After restart, opened File Explorer. 

2. Typed \\VBOXSVR\Shared_VM in the address bar. 

3. The shared folder opened successfully, showing the Wireshark installer. 

## **Result:** 

Shared folder access was successfully established. The Wireshark installer was available on the DC-Server. 

## **Challenge 3: Npcap Installation Prompt** 

## **Issue:** 

During Wireshark installation, a component selection screen appeared but did not immediately show the Npcap installation option. 

## **Observation:** 

The Wireshark installer asks for component selection first. The Npcap prompt appears on the **next screen** after clicking "Next". 

## **Solution:** 

Proceeded with the installation steps: 

1. **Components Selection:** Kept default options (TShark, External capture tools) → Clicked **Next** . 

2. **Npcap Installation:** The installer displayed a checkbox for **"Install Npcap"** . Ensured this was **checked** . 

3. **Npcap Installation Options:** When the Npcap installer appeared, selected: 

   - ✅ **Install Npcap in WinPcap API-compatible Mode** 

   - ✅ **Restrict Npcap driver's access to Administrators only** (left unchecked) 

   - ✅ **Support raw 802.11 traffic** (left unchecked) 

4. Clicked **Install** → Completed the installation. 

5. **Restarted** the DC-Server. 

## **Result:** 

Wireshark with Npcap was successfully installed on the DC-Server. 

## **Challenge 4: Selecting the Correct Network Interface** 

## **Issue:** 

After opening Wireshark on the DC-Server, the list of interfaces included several options (Ethernet, Internal, Local Area Connection*, etc.). It was unclear which interface would capture traffic between the DC and the Windows 11 client. 

## **Root Cause:** 

The DC-Server had two network interfaces: 

- **Adapter 1 (NAT):** IP 10.0.2.15 (internet traffic — not useful for capturing client traffic). 

- **Adapter 2 (Internal):** IP 172.16.0.1 (traffic to/from Win11-Client — the correct interface). 

## **Solution:** 

The interface with the 172.16.0.1 IP address was identified and selected. 

## **Procedure:** 

1. In Wireshark, reviewed the list of available interfaces. 

2. Identified the interface labeled **"Internal"** (or "Ethernet 2") with IP 172.16.0.1. 

3. Double-clicked the interface to start capturing. 

**Screenshot 5:** Wireshark Interface Selection Showing Internal Network 

## **Result:** 

The correct interface was selected, and live packet capture began successfully. 

fi |dns +|+ No. Time Source Destination Protocol Lengt! Info . 793 235.062297000 172.16.0.1 172.16.0.50 DNS 81 Standard query response @xde67 Server failure HTTPS config.edge.skype.com 794 235.063377200 172.16.0.1 172.16.0.50 DNS 81 Standard query response @x9@bd Server failure HTTPS config.edge.skype.com 795 235.06371030@ 172.16.0.1 172.16.0.50 DNS 81 Standard query response @xf8c9 Server failure A config.edge.skype.com 796 235.064059500 172.16.0.1 172.16.0.50 DNS 81 Standard query response @x3914 Server failure A config.edge.skype.com 797 236.7476398@0 172.16.0.50 172.16.0.1 DNS 81 Standard query @xd@63 A config.edge.skype.com 798 236.882479700 172.16.0.1 172.16.0.50 DNS 86 Standard query response @xbe6 Server failure A officeclient.microsoft.com 799 237.789570500 172.16.0.1 172.16.0.50 DNS 72 Standard query response @x9e73 Server failure HTTPS www.bing.com 80@ 237.790284600 172.16.0.1 172.16.0.50 DNS 72 Standard query response @x1la5 Server failure HTTPS ww.bing.com 801 237.790436300 172.16.0.1 172.16.0.50 DNS 72 Standard query response @xac9@ Server failure A www.bing.com 802 237.790547100 172.16.0.1 172.16.0.50 DNS 72 Standard query response @x6c48 Server failure A www.bing.com 803 237.790631800 172.16.0.1 172.16.0.50 DNS 72 Standard query response @x6c48 Server failure A www.bing.com 804 237.791163100 172.16.0.1 172.16.0.50 DNS 72 Standard query response @xa2d2 Server failure A www.bing.com 805 237.823438900 172.16.0.50 172.16.0.1 DNS 72 Standard query @x554b HTTPS www. bing. com 806 237.827336800 172.16.0.50 172.16.0.1 DNS 72 Standard query @x656c A ww.bing.com 807 238.404034900 172.16.0.50 172.16.0.1 DNS 83 Standard query @x523b A odc.officeapps. live.com 808 238.7014897@0 172.16.0.1 172.16.0.50 DNS 81 Standard query response @xd@63 Server failure A config.edge.skype.com 809 238.734140700 172.16.0.50 172.16.0.1 DNS 7@ Standard query @x2666 A g.live.com 810 239.432972200 172.16.0.50 172.16.0.1 DNS 83 Standard query @x523b A odc.officeapps. live.com 811 239.769686600 172.16.0.50 172.16.0.1 DNS 7@ Standard query @x2666 A g.live.com 812 240.452130900 172.16.0.50 172.16.0.1 DNS 83 Standard query @x523b A odc.officeapps. live.com 813 240.773535600 172.16.0.50 172.16.0.1 DNS 7@ Standard query @x2666 A g.live.com v 

# | Command Prompt x + »¥ 

Microsoft Windows [Version 10.0.26200.8037] (c) Microsoft Corporation. ALL rights reserved. 

C:\Users\john.doe>nsLookup mydomain.com 

DNS request timed out. timeout was 2 seconds. Server: UnkKnown Address: 172.16.0.1 

Name: mydomain.com Addresses: d17:625c:£037:2:520e:e648:e656:bc7b 172.16.0.1 10.0.2.15 



<!-- Start of picture text -->
Mi “internal - x<br>+<br>(Wsseqynome=crmydonainzsnf<br>Me sg 215 156472760 192. 16.0.58 oeteet i<br><-739 219161078400 172.16.0.1 172.16.0.50 DNs 100 Standard query response @x0005 AAAA mydomain.com AAAA £d17:625c:£037:2:520e:e648:e656:bc7b<br><!-- End of picture text -->

## **Captured Packets:** 

Packe Source → Destination Info t 736 172.16.0.50 → 172.16.0.1 Standard query 0x0004 A <u>mydomain.com</u> Standard query response 0x0004 A 172.16.0.1, A 737 172.16.0.1 → 172.16.0.50 10.0.2.15 738 172.16.0.50 → 172.16.0.1 Standard query 0x0005 AAAA <u>mydomain.com</u> Standard query response 0x0005 AAAA 739 172.16.0.1 → 172.16.0.50 fd17:625c:f037:2:520e:e648:e656:bc7b 

## **Observation:** 

- The client sent a DNS query asking for mydomain.com. 

- The DC responded with the IPv4 address 172.16.0.1 (and also returned 10.0.2.15, the NAT IP). 

- The client also asked for IPv6 (AAAA), and the DC responded with a dynamically assigned IPv6 address. 

## **Result:** 

DNS traffic was successfully captured and analyzed. The query and response packets were clearly visible. 

## **Step 2: Analyzing a DNS Packet** 

## **Procedure:** 

1. In Wireshark, double-clicked the **DNS Response** packet (Packet 737). 

2. Expanded the **"Domain Name System (response)"** section. 

3. Reviewed the following fields: 

   - **Transaction ID:** 0x0004 (matches the query) 

   - **Flags:** QR = 1 (Response), AA = 1 (Authoritative Answer) 

   - **Questions:** mydomain.com (Type A) 

   - **Answers:** mydomain.com → 172.16.0.1, mydomain.com → 10.0.2.15 



<!-- Start of picture text -->
ut veviees neip<br>i “Internal - a x<br>File Edit View Go Capture Analyze Statistics Telephony Wireless Tools Help<br>45C@O UOFREB Cee Stseeaaank<br>(WR [eros & =<br>7 @.23957220@ 172.16.0.1 172.16.0.50 KRBS 238 KRB Error: KRBSKDC_ERR_PREAUTH REQUIRED<br>14 @.265624700 172.16.0.50 172.16.0.1 KRBS 351 AS-REQ<br>15 @.276188500 172.16.0.1 172.16.0.50 KRBS 1705 AS-REP<br>24 @.298267700 172.16.0.50 172.16.0.1 KRBS 151 TGS-REQ<br>26 @.302923200 172.16.0.1 172.16.0.50 KRBS 1639 TGS-REP<br>44 1.36779080@ —172.16.0.50 172.16.0.1 KRBS 273 AS-REQ<br>45 1.37086110@ 172.16.0.1 172.16.0.50 KRBS 246 KRB Error: KRBSKDC_ERR_PREAUTH REQUIRED<br>52 1.376087600 172.16.0.5@ 172.16.0.1 KRBS 353 AS-REQ<br>53 1.379410300 172.16.0.1 172.16.0.50 KRBS 17@5 AS-REP<br>62 1.386225700 172.16.0.50 172.16.0.1 KRBS 335 TGS-REQ<br>64 1.389099200 172.16.0.1 172.16.0.50 KRBS 1763 TGS-REP<br>7@ 1.393232200 172.16.0.50 172.16.0.1 wap 547 bindRequest(13) "<ROOT>" sasl<br>72 1.39516410@ 172.16.0.1 172.16.0.50 LDAP 264 bindResponse(13) success<br>82 1.426578800 172.16.0.50 172.16.0.1 LoaP 547 bindRequest(18) "<ROOT>" sasl<br>84 1.429983300 172.16.0.1 172.16.0.50 LDAP 264 bindResponse(18) success<br>104106 29.65109770029.656883200 172.16.0.50172.16.0.1 172.16.0.1172.16.0.50 pappap 546264 bindRequest(3)bindResponse(3) "<ROOT>"success sasl ||<br>116 29.717377900 172.16.0.50 172.16.0.1 LoaP 547 bindRequest(8) "<ROOT>" sasl<br>118 29.72057760@ 172.16.0.1 172.16.0.50 pap 264 bindResponse(8) success<br>139 36.186382300 172.16.0.50 172.16.0.1 KRBS 335 TGS-REQ v<br><><br>>Frame 4: Packet, 271 bytes on wire (2168 bits), 271 bytes captured (2168 bits) on inter{| 0000 @8 00 27 23 @3 98 @8 @@ 27 75 45 79 @8 0@ 45 @@ --'#---- ‘uEy--E-<br>> Ethernet II, Src: PCSSystemtec_75:45:79 (8:00:27:75:45:79), Dst: PCSSystemtec_23:03:98|| 9710 @1 @1 2c 89 40 @@ 88 @6 75 1a ac 10 @@ 32 ac 10 - +,@ us -2--<br>> Internet Protocol Version 4, Src: 172.16.0.50, Dst: 172.16.0.1 oS bes o $ 3 bedee 3s be ai 2 & at 2 % a 2% ae 25. 6.<br>> esremssoe Control Protocol, Src Port: 51236, Dst Port: 88, Seq: 1, Ack: 1, Len: 217 || 9 2) 43 95 o1 95 a2 03 @2 01 O23 1530133011... 88<br>0050 al @4 02 @2 00 80 a2 09 04 07 30.05 a8 G3 G1 G1 -------- Os<br>0060 ff a4 81 ab 30 81 a8 a@ 07 03 05 00 40 810010 ----@--- ----@-<br>0070 al 15 3@ 13 a@ @3 @2 @1 @1 al Oc 30 @a 1b OB Ga Be Oj<br>0080 6f 68 Ge 2e 64 6f 65 a2 @a 1b 08 4d 59 44 4f 4d ohn.doe- -- -MYDOM<br>0090002@0b® 41491b 49@64e 4e6ba5 a37211 1d6218 OF7430 1b6732 a@7431 31b30 @2O830 4d@130 25939 44al31 4f1433 4d30.1230  4132 AIN:-@--IN:--krbtgt---21 0091302«+++- -MYDOMA-@<br>00c® 34 38 3@ 35 5a a6 11 18 Of 32 31 30 30 30 3931 4805Z--- -2100091<br>00dO00 33a8 Ge30 323@ 34Oc O238 C130 3512 G2Sa O1a7 0611 02O2 04C1176a 021f C188 03°33 3024805Z-O----- ----j--3eee<br>0070 a9 1d 3@ 1b 30 19 a@ @3 O2 @1 14 al 12 04 10 57 eeBeBese cocccosly<br>0100 49 4e 31 31 2d 43 4c 49 45 4e 54 20 20 20 20 IN11-CLI ENT<br><!-- End of picture text -->

A kerberos| No. Time Source Destination Protocol Lengtl Info .' 4 @.2238140007 8.239572200 172.16.6.1172.16.0.56 172.16.0.54172.16.@.1 KRB5SKRB5 236271 AS-REQKRB Error: KRBSKDC_ER 14 @.265624700 172.16.0.58 172.16.4.1 KREBS 351 AS-REQ 15 @.276188500 172.16.0.1 172.16.4.58 KRB5 1705 AS-REP 24 6.298267700 172.16.6.58 172.16.6.1 KRB5S 151 TGS-REQ 26 @.302923200 172.16.@.1 172.16.4.58 KREBS 1639 TGS-REP 



<!-- Start of picture text -->
Input Devices Help<br>Mi “internal - x<br>File Edit View Go Capture Analyze Statistics Telephony Wireless Tools Help<br>48C4@O DOBREV ePSTFISSAQQRH<br>(WetecES=} + ;<br>15 15.809428300 172.16.0.1 172.16.0.50 LDAP «2761 searchResEntry(1) "<ROOT>" | searchResDone(1) success [1 result]<br>3@ 15.855198900 172.16.0.50 172.16.0.1 LDAP 547 bindRequest(3) "<ROOT>" sas]<br>32 15.858562300 172.16.0.1 172.16.0.5@ LDAP 264 bindResponse(3) success<br>33 15.869485300 172.16.0.50 172.16.0.1 LDAP 246 SASL GSS-API Privacy: payload (128 bytes)<br>34 15.870162000 172.16.0.1 172.16.0.58 LDAP 263 SASL GSS-API Privacy: payload (145 bytes)<br>35 15.873553500 172.16.0.50 172.16.0.1 LDAP 129 SASL GSS-API Privacy: payload (11 bytes)<br>41 15.92677070@ 172.16.0.50 172.16.0.1 LDAP 547 bindRequest(8) "<ROOT>" sas]<br>43 15.933942200 172.16.0.1 172.16.0.5@ LDAP 264 bindResponse(8) success<br>44 15.937289500 172.16.0.50 172.16.0.1 LDAP 246 SASL GSS-API Privacy: payload (128 bytes)<br>45 15.938306800 172.16.0.1 172.16.0.50 LDAP 263 SASL GSS-API Privacy: payload (145 bytes)<br>46 15.941306700 172.16.0.50 172.16.0.1 LDAP 129 SASL GSS-API Privacy: payload (11 bytes)<br>84 17811552100 172.16.0.50 172.16.0.1 LDAP 404 searchRequest(1) "<ROOT>" baseObject<br>86 17.813723200 172.16.0.1 172.16.0.5@ LDAP «2761 searchResEntry(1) "<ROOT>” | searchResDone(1) success [1 result]<br>89 17.820848100 172.16.0.50 172.16.0.1 LDAP 59@ bindRequest(3) "<ROOT>" sasl<br>91 17.828996300 172.16.0.1 172.16.0.50 LDAP 264 bindResponse(3) success<br>92 17.8355@8800 172.16.0.50 172.16.0.1 LDAP 228 SASL GSS-API Privacy: payload (110 bytes)<br>93 17.836274100 172.16.0.1 172.16.0.50 LDAP 252 SASL GSS-API Privacy: payload (134 bytes)<br>94 17.837842500 172.16.0.50 172.16.0.1 LDAP 233 SASL GSS-API Privacy: payload (115 bytes)<br>95 17.838569200 172.16.0.1 172.16.0.50 LDAP 21 SASL GSS-API Privacy: payload (92 bytes)<br>< 96 17.840413500 172.16.0.50 172.16.0.1 LDAP 227 SASL GSS-API Privacy: payload (109 bytes) > v<br>> Frame 14: Packet, 404 bytes on wire (3232 bits), 404 bytes captured (3232 bits) on intel| 0000 08 0@ 27 23 03 98 @8 @@ 2775 45 79 08 0@ 4500 '# "uEy: “E><br>> Ethernet II, Src: PCSSystemtec_75:45:79 (@8:00:27:75:45:79), Dst: PCSSystemtec_23:03:98|| 9719 @1 86 2e al 40 0@ 82 @6 72 7d ac 10 00 32 ac 10 el rear<br>> Internet Protocol Version 4, Src: 172.16.0.50, Dst: 172.16.0.1 oS ° a 8 2 ies 3 ea 2 aa a “ 2 a a a 3 4S 3 ~ a<br>>: Transmissionran aT» areSrc  fe Port:‘tz 51267,b Dst Port:Port: 389, 389, Seq:Seq: 1,1, Ack:Ack: 1,1, Len: Len: 35) 9...2050o @234 99@1 0078 @1O1 4f@1 0400 0087 aOb 01GF 0062 Oa6a G165 CO63 G274 2163 006C _«x: O--- objectcl_ === :<br>2060 61 73 73 30 84 00 00 1 2b 04 11 73 75 62 73 63 ass@---- +-subsc<br>2070 68 65 6d 61 53 75 62 65 Ge 74 72 79 4 Gd 64.73 hemaSube ntry:-ds<br>0080 53 65 72 76 69 63 65 4e 61 6d 65 @4 Ge Ge 61 Gd ServiceN ame: -nam<br>2090 69 Ge 67 43 Gf Ge 74.65 78 74 73 G4 14 64 65 66 ingConte xts- def<br>0020 61 75 6c 74 4e 61 6d 69 Ge 67 43 GF Ge 74.65 78 aultNami ngContex<br><!-- End of picture text -->

## **Observation:** 

- Each time an OU or user was clicked in ADUC, an LDAP query was sent. 

- The DC responded with the requested directory information. 

- The searchRequest included the filter criteria (e.g., (&(objectClass=user) (objectCategory=person))). 

## **Result:** 

LDAP traffic was successfully captured and analyzed. 

## **Step 5: Saving the PCAP File** 

## **Procedure:** 

1. In Wireshark, clicked **File** → **Save As** . 

2. Named the file: Day11_DNS_Kerberos_LDAP.pcap. 

3. Saved to: C:\Users\Administrator\Desktop\. 

4. Clicked **Save** . 

## **Result:** 

The PCAP file was successfully saved. This file serves as proof of work and can be used for further analysis. 

## **Troubleshooting Summary** 

|Challenge|Root Cause|Solution|
|---|---|---|
|Shared folder<br>access denied|Guest Additions<br>not installed|Installed VirtualBox Guest Additions|
|Correct interface<br>not visible|Multiple interfaces<br>listed|Selected the interface with<br>IP 172.16.0.1 (Internal)|
|Too many packets<br>captured|No flter applied|Used dns, kerberos, ldap, and dns.qry.name ==<br>"mydomain.com" flters|
|DNS query not<br>appearing|Filter didn't match|Used specifc flter for mydomain.com|
|**Key Takeaways**|||
|Protocol<br>What I|Captured|Why It Matters|
|**DNS**<br>Query<br>for my|and response<br>domain.com|Demonstrates name resolution in AD|
|**Kerberos**<br>AS-RE|Q, AS-REP, TGS-REQ, TGS|-REP<br>Shows how authentication works in<br>AD|
|**LDAP**<br>Search|requests for OUs and u|sers<br>Shows how AD queries work|



## **Conclusion** 

This lab provided practical experience with **Wireshark packet capture and analysis** in a Windows Server Active Directory environment. Wireshark was successfully installed on the Domain Controller after adding a NAT adapter and installing Guest Additions for shared folder access. The installation process included installing Npcap for packet capture capabilities. 

Packet captures were performed for **DNS** , **Kerberos** , and **LDAP** traffic. The DNS capture demonstrated how clients resolve domain names to IP addresses. The Kerberos capture illustrated the authentication flow (AS-REQ, AS-REP, TGS-REQ, TGS-REP). The LDAP capture showed how directory queries are performed when browsing Active Directory Users and Computers. 

The challenges faced during installation (internet connectivity, shared folder access, and Npcap installation) provided valuable troubleshooting experience. The ability to capture and analyze network traffic is an essential skill for **IAM Analysts, SOC Analysts, and System Administrators** responsible for maintaining secure and reliable enterprise environments. 

