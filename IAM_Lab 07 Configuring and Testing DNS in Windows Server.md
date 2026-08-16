### **Active Directory Lab 07** 

### **Configuring and Testing DNS in Windows Server** 

### **Objective** 

The objective of this lab was to understand the role of the **Domain Name System (DNS)** in an Active Directory environment. The lab involved creating a new **Host (A) record** , verifying forward and reverse DNS name resolution, and managing the DNS cache using command-line tools. This exercise demonstrated how DNS enables reliable communication between clients and servers within a Windows domain. 

### **Lab Environment** 

### **Component Details** 

Operating System Windows Server (Domain Controller) Client Machine Windows 11 Virtualization VMware Workstation / VirtualBox Domain mydomain.com Tool Used DNS Manager, Command Prompt 



<!-- Start of picture text -->
fe<br>we<br>&, DNS Manager - og x cu<br>File Action View Help<br>P<>| © XSeasalbmli Gs<br>=aii A 48 Roce Name= DCO<br>igi Al<br>& |<br>iG Fi<br>Hide<br>Events Events<br>Services Services<br>ls BPAPerformanceresults BPAPerformanceresults<br>ms ©=r& e@ B & a* @ Fl Ie 5/3/20264:56 PM a<br><!-- End of picture text -->



<!-- Start of picture text -->
&,* ONS Manager - Oo 4 4<br>File Action Wew Help<br>§@¢o9\/4m/| S| ml i OG<br>qd4 &w~= DNSa@ )peo. Fanward Lookup Zones EdName_nsdes.mydomain.com. . TypeActive.. Directory-Integrated.. Pr. StatusRunning.. DNSSECNot Signed.. Status<br>cy (5): Reverse Lookup Zones Ed mydomain.com Active Directory-Integrated Pr. Running Mot Signed<br>(A Trust Points<br>2 (4) Conditional Forwarders<br>i<br><!-- End of picture text -->



<!-- Start of picture text -->
Tia Server Manager<br>_— fed<br>&, DNS Manager _ oO x ie<br>File Action View Help<br>Peo 2nlOeasibm|i aa<br>i lq & DNS Name Type Data Timestam<br>aiigi AlAl v v@ ocoForwardEl —Msdesmydorain.c: Lookup Zones ie|wed_msdesDtep | sites<br>e = mydomain.com =] ud<br>ce D “| Reverse Lookup Zones Be P .<br>it Fi =| Trust Points - DomainDnsZones<br>“) Conditional Forwarders F]forestonsZones<br>EAGame as parent folder) Start of Authority (SOA) [36], dcOl.mydomain.com... static<br>Ficame as parent folder) Name Server (NS) dcOl.mydomain.com. static<br>Eicame as parent folder) Host (4) 10.0.2.15 7/26/2026)<br>Eicame as parent folder) Host (4) 172.16.0.1 7/26/2026<br>Eicame as parent folder) IPv6 Host (AAAA) fd17:625c:f037:0002:520e:e... 7/26/2026<br>FAacon Host (4) 172.16.0.1 static<br>Fdeor Host (4) 10.0.2.15 static<br>FAaeon IPv6 Host (AAA4) fd17:625c:f037:0002;520e:e.., static<br>FAwin11-client Host (4) 172.16.0.50 7/26/2026)<br>< rI|< ><br><!-- End of picture text -->



<!-- Start of picture text -->
few Server M<br>© hs DNS Manage — oO . . vo<br>File Action View Help<br>eo9\|fm| Xo as\bm| i AG<br>i L = 5 cat New Host h x ft Timestam<br>Ha A v © Forward Lookup Zones Name (uses parent domain name if blank):<br>= 3 adomuncor<br>a =. mydomain.com<br>= D “| Reverse Lookup Zones Fully qualified domain name (FQDN):<br>~ Conditional Forwarders IP address: 6], dcOl.mydomain.com... static<br>0.2.15 7/26/2026<br>Create associated pointer (PTR) record 2.16.01 7/26/2026<br>(allow any authenticated user to update DNS records with the 17:625c:F037:0002:520e:e... 7/26/2026<br>same owner name 2.16.0,1 static<br>0.2.15 static<br>17:625c:F037:0002:520e:e.., static<br>2,16.0.50 7/26/2026<br>< > < ><br>Events | Events<br><!-- End of picture text -->



<!-- Start of picture text -->
& DNS Manager - O * (225<br>File Action View Help<br>S@o(F FIXES SIBm| di aS<br>Ld & DNS Marne Type Data Tirmestam<br>A v g poo a mades<br>w (5) Forward Lookup Zones sites<br>A (Ed. umsdes.mydomainic Jt c<br>D = (ie) mydornain.com Dy=_udpP<br>Fi Lo[S) TrustReversePoints Lookup Zones |- DornainDnsZones;<br>(4) Conditional Fanwarders CP] ForestDnsZones<br>[Altame as parent folder) Start of Suthority (C4) [36], dcOmydorain.com., static<br>[Altame as parent folder) Name Server (NS) dcOLmydomain.carm, static<br>]tsame as parent folder) Hast (43 10.0.2.15 7262026<br>lame as parent folder) Hast (43 172.16.0.1 P26 2026<br>lame as parent folder) PYG Host (Acca) FAM E25 FOS FOO AOere., P26 f2026<br>fAyaent Hast (4) 172.16,0,1 static<br>FAlaent Hast (Ai 10,0.2,15 static<br>fAlaent [Pye Host (Ae AA4 TAT 625cF0S 7000252 Oe... static<br>[Alwint1-Client Host (4) 172.168.0050 F2Gf2026<br>Attest Hast (a4 172.16.0.1<br>< >| < ><br><!-- End of picture text -->



<!-- Start of picture text -->
vals<br><!-- End of picture text -->



<!-- Start of picture text -->
™) Command Prompt<br><!-- End of picture text -->



<!-- Start of picture text -->
x + »<br><!-- End of picture text -->

Microsoft Windows [Version 10.0.26200.8037] (c) Microsoft Corporation. All rights reserved. 

C:\Users\john.doe>nslookup test.mydomain.com DNS request timed out. timeout was 2 seconds. Server: Unknown Address: 172.16.0.1 

Name: test.mydomain.com Address: 172.16.0.1 

C:\Users\john.doe> 

dap._tcp.Default-First-Site-Name._sites.dc._msdcs.mydomain.com 

|Record<br>Name<br>.<br>...<br>.<br>HOomain. com<br><br>|:<br>_ldap._tcp.Default-First-Site-Name._sites.dc._msdcs.my<br><br>|
|---|---|
|Record Type...<br>..<br><br><br><br>|:<br>33<br><br>|
|Time<br>To<br>Live<br>....:<br><br>|TH7<br><br>|
|Data Length...<br>..:<br><br><br><br>|16<br><br>|
|Section...<br>..<br>.<br>.<br><br><br><br>|:<br>Answer<br><br>|
|SRV Record<br>...<br>.<br>.|:<br>dc@1.mydomain.com<br>0|
||100<br>389|
|dc01.%ydomain.<br>com||
|Record Name<br>.<br>...<br>|.<br>:<br>dc@1.mydomain.com<br><br>|
|Record Type ....<br><br><br><br>|.:<br>1<br><br>|
|Time<br>To<br>Live<br>...<br>|.:<br>TU7<br>|
|Data Length. ..<br><br><br>|.:4<br><br><br>|
|Section...<br>..<br>..<br><br><br><br>|..<br>:<br>Additional<br><br><br>|
|A (Host)<br>Record<br>.<br>.|.<br>:<br>172.16.0.1|
|Record Name...<br>.<br><br>|.<br>:<br>dc@1.mydomain.com<br><br><br>|
|Record Type...<br><br><br><br><br>|..<br>:<br>28<br><br>|
|Time<br>To<br>Live<br>...<br>|.:<br>TUT<br><br>|
|Data Length ....<br><br><br>|.:<br>16<br><br><br>|
|Section...<br>..<br>..<br><br>|..<br>:<br>Additional<br><br><br>|
|AAAARecord...<br>.|.<br>:<br>£d17:625c:f037:2:520e:e6U8:e656:bc7b|





<!-- Start of picture text -->
dc01.%ydomain.com<br>Record Name . ... . : dc@1.mydomain.com<br>Record Type .....: 1<br>Time To Live ....: TU7<br>Data Length. ....:4<br>Section... .. .. .. : Additional<br>A (Host) Record . . . : 172.16.0.1<br>Record Name... . . : dc@1.mydomain.com<br>Record Type... .. : 28<br>Time To Live ....: TUT<br>Data Length .....: 16<br>Section... .. .. .. : Additional<br>AAAA Record... . . : £d17:625c:f037:2:520e:e6U8:e656:bc7b<br><!-- End of picture text -->

#### g. live.com 

No records of type A 

_ldap._tcp.Default-—First-Site-Name._sites.DC01.mydomain.com. 

Record Name . ... . : _ldap._tcp.Default-First-Site-Name._sites.DC01.mydomai n.com. Record Type... . . : 255 Time To Live ... . : 400 Data Length .....: 0 Section... .. . . : Answer DCO1.mydomain.com Record Name . .. . . : DCO1.mydomain.com Record Type .....: 1 Time To Live ... . : 3685 Data Length. ....:4 Section... .. . . : Answer A (Host) Record . . . : 172.16.0.1 

www.msftnesi.com 

No records of type A 

watson.events.data.microsoft.com 

No records of type A 

_ldap._tcp.DC0O1.mydomain.com. 

Record Name... . . : _ldap._tcp.DCO1.mydomain.com. Record Type... .. : 255 Time To Live ... . : 400 Data Length. ....: 0 Section... ... . : Answer v10.events.data.microsoft.com 

No records of type A 

## C:\Users\john.doe>ipconfig /flushdns 

## Windows IP Configuration 

Successfully flushed the DNS Resolver Cache. 

# C:\Users\john.doe>ipconfig /dispLlaydns 

Windows IP Configuration 

C:\Users\john.doe> 

C:\Users\john.doe>nsLookup 172.16.0.1 DNS request timed out. timeout was 2 seconds. Server: Unknown Address: 172.16.0.1 DNS request timed out. timeout was 2 seconds. *kx Request to Unknown timed-out 

### **Conclusion** 

**Domain Name** This lab provided practical experience in configuring and managing the **System (DNS)** within an Active Directory environment. The Forward Lookup Zone was explored, and a new **Host (A) record** was successfully created along with its corresponding **PTR record** . DNS functionality was validated through forward and reverse name resolution using the **nslookup** utility. Additionally, DNS cache management was performed using **ipconfig** commands to demonstrate how cached records can be viewed and refreshed. Overall, this lab reinforced the critical role of DNS in supporting Active Directory services and ensuring reliable name resolution across the network. 

