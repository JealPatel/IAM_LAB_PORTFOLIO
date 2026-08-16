# **IAM Lab 17 — Linux Network Configuration, DNS & Connectivity Analysis** 

# **Objective** 

The objective of this lab is to practice basic Linux network troubleshooting and analysis using: 

- ip addr 

- ip route 

- ping 

- dig 

- nslookup 

- curl 

- ss 

The lab helps understand the relationship between **IP addressing, routing, DNS resolution, HTTP connectivity, and listening network ports** . 

# **Lab Environment** 

**Component Details** DC-Server Windows Server / Domain Controller Ubuntu-Lab Ubuntu Linux Ubuntu User labuser DC IP 172.16.0.1 Ubuntu IP 172.16.0.100 Network 172.16.0.0/24 Domain mydomain.com 

**Step 0: Start the VMs** 

# **Procedure** 

1. Started **DC-Server** . 

2. Logged in using: 

mydomain\Administrator 

3. Started **Ubuntu-Lab** . 

4. Logged in using: 

Username: labuser 

Password: P@ssw0rd123 

# **Result** 

Both virtual machines were successfully started. 

# **Step 1: IP Configuration** 

# **1.1 Check IP Addresses** 

# **Command** 

ip addr 

# **Purpose** 

The ip addr command displays the network interfaces and IP addresses configured on the Ubuntu system. 

You may see something similar to: 

lo: 

inet 127.0.0.1/8 

enp0s3: 

inet 172.16.0.100/24 

Your interface name may be different, such as: 

ens33 

enp0s3 

eth0 

**Important Interfaces** 



<!-- Start of picture text -->
labuser@ubuntu-lab:"# ip addr<br>1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65596 qdisc noqueue state UNKNOWN group default qlen 1948<br>link/ loopback 84:68: 00:00:00:66 Ord 66:68:66: 48:80708<br>inet 127.0.0.1/8 scope host lo<br>Valid_lft forever preferred_lft forever<br>ineté 128 scope host noprefixroute<br>Valid_lft forever preferred_lft forever<br>2: enpa@sa: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 15@@ qdisc ptifo_fast state UP group default glen 1ieae<br>linkfether G6:86:27:9d:efiad bred ftiftittsft tts ft<br>altname enxesaee?odeta3<br>inet 172.16.9.198/24 brd 172.16.9.255 scope global enpas3<br>Valid_lft forever preferred_lft forever<br>ineté f64 scope link proto kernel_ll<br>Valid_lftt forever preferred_lft forever<br>labuser@ubuntu-lab:"s _<br><!-- End of picture text -->

labuser@ubuntu-lab:"$ ip route detault via dey enpas3 prota static dev enpass proto kernel scope link src labuser@ubuntu- lab: 



<!-- Start of picture text -->
labuser@ubuntu-lab:"S ping 172.16.8.1 -c 4<br>ING 172.16.8.1 (€172.16.8.1) 56(84) bytes of data.<br>4 bytes from 172.16.8.1: icmp_segri ttl=128 times2.24 ms<br>4 bytes from 172.16.8.1: icmp_seg=2? ttl=128 time=1.41 ms<br>4 bytes from 172.16.8.1: icmposeg=3 ttl=128 timesi.64 ms<br>4 bytes trom i72.16.8.1: icmp_seg=4 ttl=126 time=i.32 ms<br>-- 172.16,.8.1 ping statistics ---<br>packets transmitted, 4 received, @% packet loss, time daiems<br>tt minfvave/max/mdey = 1.811/1.4601/2.299/6.498 mes<br>labuUser@uountu-lab:lab: s<br><!-- End of picture text -->

labuser@ubuntu-lab:"S ping 172.16.8.1 -c 4 ING 172.16.8.1 (€172.16.8.1) 56(84) bytes of data. 4 bytes from 172.16.8.1: icmp_segri ttl=128 times2.24 ms 4 bytes from 172.16.8.1: icmp_seg=2? ttl=128 time=1.41 ms 4 bytes from 172.16.8.1: icmposeg=3 ttl=128 timesi.64 ms 4 bytes trom i72.16.8.1: icmp_seg=4 ttl=126 time=i.32 ms -- 172.16,.8.1 ping statistics --packets transmitted, 4 received, @% packet loss, time daiems tt minfvave/max/mdey = 1.811/1.4601/2.299/6.498 mes labuUser@uountu-lab:lab: s 



<!-- Start of picture text -->
labuser@ubuntu-lab:"$ ping mydomain.com -c 4<br>ING mydomain.com (172.16.8.1) S684) bytes of data.<br>4 bytes from 172.16.8.1: icmp_seg=1 ttl=128 time=8.963 ms<br>4 opytes trom 172.16.6.4: icmp_seqce ttl-128 time-@.766 ms<br>4 bytes from i?f2.16.8.1: icmp_seq=3 ttl=128 time=6.925 ms<br>4 bytes from 172.16.8.1: icmp_seqs4 ttl=128 times@.528 ms<br>-- mydomain.com ping statistics ---<br>packets transmitted, 4 received, 8% packet loss, time 5@11ms<br>‘tt minvave/max/mdey = @.528/6.793/6.965/8.174 ms<br>labuser@ubuntu- lab:<br><!-- End of picture text -->

labuser@ubuntu-lab:"$ ping mydomain.com -c 4 ING mydomain.com (172.16.8.1) S684) bytes of data. 4 bytes from 172.16.8.1: icmp_seg=1 ttl=128 time=8.963 ms 4 opytes trom 172.16.6.4: icmp_seqce ttl-128 time-@.766 ms 4 bytes from i?f2.16.8.1: icmp_seq=3 ttl=128 time=6.925 ms 4 bytes from 172.16.8.1: icmp_seqs4 ttl=128 times@.528 ms -- mydomain.com ping statistics --packets transmitted, 4 received, 8% packet loss, time 5@11ms ‘tt minvave/max/mdey = @.528/6.793/6.965/8.174 ms labuser@ubuntu- lab: 



<!-- Start of picture text -->
labuser@ubuntu-lab:"$ dig mycdomain.com<br><!-- End of picture text -->

>; <<>> Dib 9.28.18-lubuntu2-Ubuntu <<>> mydomain.com 3: @lobal options: +cmd 33 GOt answer: 33 ->>HEADER¢<opcode: QUERY, status: NOERROR, id: 22383 33 flags: gr ed ra; QUERY: 1, ANSWER: 2, AUTHORITY: &, ADDITIONAL: 1 ;3 OPT PSEUDOSECTION: >; EDNS: version: @, flags:; udp: 65494 35 QUESTION SECTION: ;mycdomain.com. IN A >; ANSHER SECTION: mydamain. com. 556 IN A 16.48.2.15 mycdomain. con. 556 IN A 172.16.@.1 33 Query time: 3 msec 3; SERVER: 127.6.8.959#53(127.4.8.53) (UDP) 33 HHEN: Thu Aug 19 11:29:13 UTC 2826 33 H8G SIZE revd: 73 labuser@ubuntu-lab: "s 



<!-- Start of picture text -->
abuser@ubuntu-lab:"s nslookup mydomain.com<br>EPVER: 127.8.8.53<br>Wdress: 127.8.8.59#59<br>fon-authoritative answer:<br>fame : mydamain.comcom<br>Wddress: 16.@.2.15<br>Jame: muidanain.camcam<br>Address: L72.16.8.1<br>farnie : mydonain.comcom<br>Wddress: tdt?:625c:f897:2:52%8e:e2648:e656:bc7b<br>abuser@ubuntu-lab: “slab: “s “s<br><!-- End of picture text -->

abuser@ubuntu-lab:"s nslookup mydomain.com EPVER: 127.8.8.53 Wdress: 127.8.8.59#59 fon-authoritative answer: fame : mydamain.comcom Wddress: 16.@.2.15 Jame: muidanain.camcam Address: L72.16.8.1 farnie : mydonain.comcom Wddress: tdt?:625c:f897:2:52%8e:e2648:e656:bc7b abuser@ubuntu-lab: “slab: “s “s 



<!-- Start of picture text -->
labuser@ubuntu-lab:"$ curl -y htto://172.16.8.1<br>e Trying 172.16.8.1:88...<br>ee connect to 172.16.8.1 port 8@ from 172.16.4.168 port 54864 failed: Connection timed out<br>* Failed to connect to 172.16.9.1 port 8@ after 145718 ms: Could not connect to server<br>* Closing connection #a<br>curl: (28) Failed to connect to 172.16.9.1 port 66 after 145718 ms: Could not connect to server<br>labuser@ubuntu-lab:"s<br><!-- End of picture text -->



<!-- Start of picture text -->
apuser@ubuntu-lab:$ curl -v http: /¢mydomain.com<br>le Host mudoamain.com:4@ was resolved.<br>bh IPvG: fdi?:625c:f@g7:2:526e:eb46:e6S6:bcrb<br>ko Trying [fdl?s625ce:fe3?s2:S2ee:e648:eb5e:bc7b)88...<br>ft Immediate connect fail for fdi?:625c:f637:2:526e:e648:e656:bc%b: Network is unreachable<br>fm’ Trying 172.16.8.1:80...<br>h* =oTrying 18.@.2.15:808...<br>hm connect to 172.16.9.1 port 88 from 172.16.9.19@ port 49882 failed: Connection timed out<br>hk Connect to 18.8.2.15 port 88 from 172.16.8.108 port 41968 failed: Connection timed out<br>fh Failed to connect to mydomain.com port 8@ after 146373 ms: Could not connect to server<br>f& Closing connection #6<br>curl: (26) Failed to connect to mydomain.com port 88 after 146373 ms: Could not connect to server<br>labuser@ubuntu-lab:"s<br><!-- End of picture text -->

# **Step 5: Check Listening Ports** 

# **5.1 Use ss** 

# **Command** 

sudo ss -tulpn 

# **Purpose** 

This command displays network sockets and listening services. 

# **Options** 

# **Option Meaning** 

- -t TCP 

- -u UDP 

- -l Listening 

- -p Show process 

- -n Show numerical addresses/ports 

You might see: 

Netid   State    Local Address:Port 

tcp     LISTEN   0.0.0.0:22 

# **Port 22** 

Port: 

22 

is normally associated with: 

SSH 

So if SSH is running: 

sshd → TCP → Port 22 → LISTEN 

# **Important** 

Your output **doesn't have to exactly match the worksheet** . 

For example, if SSH isn't running, port 22 won't appear. 

You can check SSH with: 

sudo systemctl status ssh 

Then check again: 



<!-- Start of picture text -->
abuser@ubuntu-lab:“$ sudo ss -tulpn<br>(sudo: authenticate] Password:<br>Net id State Recy-@ Send-@ Local Address:Port Peer Address:Port Process<br>idp UNCONN fa) fa) 127.0.0.1:323 0.0.0.0: users:(("'chronyd", pid=1364, fd=4))<br>udp UNCONN t) (7) 127.0.0.54:53 8.0.0.0: users: (("'systemd-resolve",pid=855, fd=18 )<br>udp UNCONN a a 127.6.0.53%10:53 6.0.0.0: users: (("'systemd-resolve",pid=855,fd=16) )<br>udp UNCONN C) (2) [3:4] :323 (6B) BE users: (("chronyd", pid=1364, fd=5))<br>cp LISTEN a 4096 127.0.6.53%10:53 6.0.8.0: users: ((''systemd-resolve",pid=855,fd=17) )<br>cp LISTEN a 4096 6.0.0.0:22 0.0.8.0:% users: (("systemd",pid=1, fd=100))<br>cp LISTEN (a) 4096 127.0.0.54:53 0.0.0.0:% users: (("'systemd-resolve",pid=855,fd=19))<br>cp LISTEN () 4096 [::]:22 (881) Be users: (("systempid=1, f d =161))",<br>Labuser@ubuntu-lab:~s<br><!-- End of picture text -->

↓ 

curl -v http://mydomain.com 

# 6. Check local listening services 

↓ 

sudo ss -tulpn 

# **Easy Memory Trick** 

Think: 

# **IP → Route → Ping → DNS → Application → Ports** 

or: 

# **"Can I identify myself → find the path → reach the machine → resolve its name → reach the service → see what's listening?"** 

That's a really solid troubleshooting mindset. 

# **Expected Results Summary** 

**Test Expected Result What It Proves** ip addr 172.16.0.100/24 IP configuration ip route Route via 172.16.0.1 Routing ping 172.16.0.1 Replies Network connectivity ping mydomain.com Resolves to 172.16.0.1 DNS + connectivity dig mydomain.com A record returned Detailed DNS nslookup mydomain.com IP returned DNS resolution curl -v http://172.16.0.1 Depends on HTTP service Application connectivity curl -v http://mydomain.com Depends on HTTP service DNS + HTTP sudo ss -tulpn Listening sockets Network exposure 

# **Cybersecurity Relevance** 

This lab is directly useful for basic **SOC and network troubleshooting** . 

An analyst can use these commands to investigate questions such as: 

- What IP address does this machine have? 

- Which network does it belong to? 

- Where is its traffic being routed? 

- Can it communicate with the Domain Controller? 

- Is DNS resolving correctly? 

- Can the machine reach a particular service? 

- Which ports are currently exposed? 

- Which processes are associated with those ports? 

For example: 

Ubuntu 

172.16.0.100 

│ 

│ ping 

↓ 

DC-Server 

172.16.0.1 

│ 

├── DNS : 53 

├── SSH : 22 (if enabled) 

└── Other services 

