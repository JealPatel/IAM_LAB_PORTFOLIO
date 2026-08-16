# **IAM Lab 16 — Linux Service, Process & Network Management** 

# **Objective** 

The objective of this lab was to practice basic Linux **service management, process management, and network socket/port inspection** . 

The lab focused on using systemctl to manage services, ps and top to monitor processes, kill to terminate a test process, and ss to identify listening network ports. 

These are important Linux administration and cybersecurity skills because a security analyst may need to determine **which services are running, which processes are active, and which network ports are exposed** . 

# **Lab Environment** 

|**Component**|**Details**|
|---|---|
|Virtual Machine|Ubuntu-Lab|
|Operating System|Ubuntu Linux|
|User|labuser|
|SSH Service|OpenSSH|
|Service Manager|systemd|
|Process Tools|ps, top, kill|
|Network Tool|ss|



**Step 0: Start the VM** 

labuser@ubuntu-lab:"$ sudo systemctl status sshd (sudo: authenticate] Password: hk ssh.service - OpenBSO Secure Shell server Loaded: loaded (/usr/lib/systemd/system’ssh.service; disabled; preset: enabled) Active: inactive (dead) TriggeredBy: «© ssh.socket Docs: manzsshd(ay man:sshd_cantig(s) labuser@ubuntu-lab: "$ 

abuser@ubuntu-lab:"$ sudo systemctl start sshd abuser@ubuntu-lab:"$ sudo systemcetl status sshd ssh.service - OpenBSD Secure Shell server Loaded: loaded (/usr/lib/systemd/systemssh.service; disabled; preset: enabled) Active: active (running) since Wed 2626-68-12 11:41:54 UTC; Ss aga Invocation: addelatedshedasegzeeteceacadt riggeredBy: © ssh.socket abe Docs: man:sshd(a) Iman: sshd_config(5) Process: 1715 ExecStartPre=/usr/shin/sshd -t (code=exited, status=8/SUCCESS) Main PID: 1718 (sshd) Tasks: 1 (limit: 1688) Memory: 1.8M (peak: 2.5M) CPU: 69ms Caroup: “system. slice/ssh.service Cajig "sshd: /usr/sbin/sshd -0 [listener] 6 of 16-1084 startups" AUG 12 11:41:54 ubuntu-lab systemd[1]: Starting ssh.service - OpenBSD Secure Shell server... Aug 12 11:41:54 ubuntu-lab sshd[1718]: Server listening on 6.4.8.8 port 22. Aug 12 11:41:54 ubuntu-lab systemd[1i]: Started ssh.service - OpenBSo Secure Shell server. Aug 12 11:41:54 ubuntu-lab sshd[1718]: Server listening on :: port 22. abusergubuntu-lab:"s 

labuser@gubuntu-lab:"$ sudo systemct] status sshd [sudo: authenticate] Password: hm ssh.service - OpenBSD Secure Shell server Loaded: loaded (/usr/lib/systemd/systemssh.service; disabled; preset: enabled) Active: inactive (dead) TrigferedBy: « ssh.socket Docs: tman:sshd(a) man:sshd_contig(S) labuser@gubuntu-lap: “$ 



<!-- Start of picture text -->
abuser@ubuntu-lab:"$ sudo systemctl start sshd<br>abuser@ubuntu-lab:"$ sudo systemcetl status sshd<br>ssh.service - OpenBSD Secure Shell server<br>Loaded: loaded (/usr/lib/systemd/systemssh.service; disabled; preset: enabled)<br>Active: active (running) since Wed 2626-98-12 11:41:54 UTC; Ss ago<br>Invocation: addelatedshedasegzeeteceacadt<br>riggeredBy: © ssh.socket abe<br>Docs: man:sshd(a)<br>man:sshd_contig(5)<br>Process: 1715 ExecStartPres/usr/sbin/sshd -t (codesexited, status=a/SUCCESS)<br>Main PID: 1718 (sshd)<br>Tasks: 1 (limit: 1688)<br>Memory: 1.8M (peak: 2.5M)<br>CPU: 69ms<br>Caroup: “system. slice/ssh.service<br>Cajig "sshd: /usr/sbin/sshd -0 [listener] 6 of 16-1084 startups"<br>AUG 12 11:41:54 ubuntu-lab systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...<br>Aug 12 11:41:54 ubuntu-lab sshd[1718]: Server listening on 6.4.8.8 port 22.<br>Aug 12 11:41:54 ubuntu-lab systemd[1i]: Started ssh.service - OpenBSo Secure Shell server.<br>Aug 12 11:41:54 ubuntu-lab sshd[1718]: Server listening on :: port 22.<br>abusergubuntu-lab:"s<br><!-- End of picture text -->



<!-- Start of picture text -->
abuser@ubuntu-lab:"$ sudo systemctl restart sshd<br>abuser@ubuntu-lab:"$ sudo systemctl status sshd<br>ssh.service - OpenBSD Secure Shell server<br>Loaded: loaded (/usr/lib/systemd/system’ssn.service; disabled; preset: }<br>Active: since Hed 2826-68-12 11:44:58 UTC; 2s ago<br>Invocation: bet ?4a5S5esalddbbbeetalizobeet329.<br>riggeredBy: «© ssh.socket<br>Docs: man:sshd(8)<br>fan:sshd_contig(o)<br>Process: 1761 ExecStartPres/usr/sbin/sshd -t (codesexited, status=@/SUCCESS)<br>Main PID: 1764 (sshd)<br>Tasks: 1 (limit: 1989)<br>Memory: 1.6M (peak: 1.9M)<br>CPU: 45ms<br>CGroun: “system.slice/ssh. service<br>Lived "sshd: /usr/shinvsshd -D [listener] @ of 14-160 startups"<br>Bug 12 11:44:58 ubuntu-lab systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...<br>Rug le di:44:5@ ubuntu-lab sshd[1764]: Server listening on 4.4.6.6 port 22.<br>Rug 12 11:44:56 ubuntu-lab sshd[1764]: Server listening on :: port 22.<br>Bug 12 14:44:58 ubuntu-lab systemd([1]: Started ssh.service - OpenBSD Secure Shell server.<br>abuser@ubuntu- lab:<br><!-- End of picture text -->



<!-- Start of picture text -->
alabuser@ubuntu-lab:~$ ee ac<br><!-- End of picture text -->

labuser@upuntu-lab:"$ sudo systemctl disable sshd Removed ‘/fetc/systemd/systemmulti-user.target.wants/ssh.service'. Removed ‘/fetc/systemd/system’sshd.service’. Disabling ‘sshd.service', but its triggering units are still active: ssh.sacket labuser@upuntu-lab: Ss 



<!-- Start of picture text -->
root 81 8.0 8.0 8 a? I 11:36 © 6:60 [kworker/u12:6]<br>root 82 8.0 8.6 (7) 6? I 11:36 6:00 [kworker/u13:6]<br>root 93 8.6 6.0 a a? I 11:36 6:00 [kworker/R-charger_manager]<br>root 184 6.1 0.6 c) a? I 11:36 6:06 [kworker/1:1H-kblockd]<br>root 397 6.0 0.6 ) 6? iS} 11:36 6:00 [scsi_eh_2]<br>root 398 6.0 6.6 a a? I 11:36 6:06 [kworker/R-scsi_tmf_2]<br>root 473 6.0 6.6 Q 0? I 11:36 6:60 [kworker/R-kdmf lush/252:8]<br>root 513 6.0 6.6 i) 6? s 11:36 6:00 [jbd2/dm-9-8]<br>root 514 0.0 0.0 Q a? I 11:36 6:06 [kworker/R-ext4-rsyv-conversion]<br>root 800 6.1 1.1 50652 19588 7 S<s 11:37 6:01 /usr/lib/systemd/systemd- journald<br>root B14 0.0 0.0 @ a? I 11:37 6:00 [kworker/R-kmpathd]<br>root 815 08.6 6.8 a a? I 11:37 6:00 [kworker/R-kmpath_handlerd]<br>root 833 6.6 6.5 279492 9644 ? SLsl 11:37 6:60 /usr/sbin/multipathd -d -s<br>systemd+ 856 6.1 6.8 22876 14900 ? 8s 11:37 6:06 /usr/lib/systemd/systemd-resolved<br>root 860 6.2 6.8 39372 13592 7? Ss 11:37 6:02 /usr/lib/systemd/systemd-udevd<br>root 861 6.0 6.6 a 6? s 11:37 6:08 [psimon]<br>root 976 6.0 8.8 (3) 6? 3 11:37 6:00 [jbd2/sda2-8]<br>root 371 6.6 6.8 C) a? I 11:37 6:66 [kworker/R-ext4-rsv-conversion]<br>root 973 «6.0 6.6 a 6? $ 11:37 6:00 [irg/18-vmwgtx]<br>root 975 6.0 6.6 a a? I 11:37 6:00 [kworker/R-ttm]<br>systemd+ 1088 9.6 @.7 21428 12276 7 8s 11:37 6:00 /usr/lib/systemd/systemd-networkd<br>root 1158 0.0 0.0 Q a? I 11:37 6:00 [kworker/R-cfg80211]<br>root 1242 0.0 @.1 2888 1948 ? Ss 11:37 6:00 /bin/sh /usr/lib/systemd/scripts/chronyd-starter.sh -n -F 1<br>root 1243 6.8 0.2 7060 3412 7 8s 11:37 6:00 /usr/shin/cron -f -P<br>Messaget+ 1244 0.6 @.3 39008 5586 ? Ss 11:37 6:06 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-o<br>root 1252 6.1 1.7 46724 30100 ? Ss 11:37 6:01 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers<br>polkitd 1253 6.0 0.5 306444 8496 ? Ssl 11:37 6:00 /usr/lib/polkit-1/polkitd --no-debug --log-level=notice<br>root 1266 6.0 6.5 18552 9572 ? 8s 11:37 6:00 /usr/lib/systemd/systemd- logind<br>root 1263 6.6 6.8 543364 15012 ? Ssl 11:37 6:00 /usr/libexec/udisks2/udisksd<br>root 1325 6.0 6.3 8766 5548 ? Ss 11:37 6:06 login -- labuser<br>isys log 1327 6.0 6.3 220548 6128 ? Ssl 11:37 6:00 /usr/sbin/rsyslogd -n -iNONE<br>root 1336 6.1 1.9 1268096 32860 ? Ssl 11:37 6:01 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal]<br>root 1375 6.1 8.8 391604 14116 ? Ssl 11:37 6:06 /usr/sbin/ModemManager<br>_chrony 1378 6.0 8.3 20420 6276 ? 8 11:37 6:06 /usr/sbin/chronyd -n -F 1<br>_chrony 1392 0.0 6.1 12092 2432 ? $ 11:37 6:06 /usr/sbin/chronyd -n -F 1<br>root 1497 6.6 0.8 ) 6? I 11:37 6:00 [kworker/1:2H]<br>root 1498 0.6 0.6 fr) 0? I 11:37 6:00 [kworker/@:2H-kblockd]<br>labuser 1626 6.0 8.7 22016 12708 ? Ss 11:39 6:06 /usr/lib/systemd/systemd --user<br>labuser 1632 06.0 0.2 23004 4084 ? 8 11:39 6:00 (sd-pam)<br>labuser 1652 6.0 0.3 8856 5808 tty1 Ss 11:39 6:08 -bash<br>root 1747 6.0 0.6 a a? I 11:44 6:06 [kworker/u9:3-events_power_ef ficient]<br>root 1762 6.0 0.6 a a? I 11:44 6:00 [kworker/1:8-cgroup_free]<br>root 1764 6.0 6.4 10740 7780 ? Ss 11:44 6:00 sshd: /usr/sbin/sshd -D [listener] 8 of 10-100 startups<br>root 1767 8.0 9.6 (7) 6? I 11:44 6:00 [kworker/@:2-events]<br>root 1795 6.6 6.6 6 a? I 11:45 6:66 [kworker/u16:3-events_unbound]<br>root 1908 9.6 9.6 2) 6°? i} 11:45 6:66 [psimon]<br>root 1913 0.0 0.0 8 a? I 14:46 6:00 [kworker/u9:4-ext4-rsv-conversion]<br>root 1928 8.0 0.0 Q a? I 11:47 6:00 [kworker/1:0H]<br>labuser 1953 100 6.2 9764 «64684 ttyl R+ 11:49 6:06 ps aux<br>labuser@ubuntu-lab:"$<br><!-- End of picture text -->

# **Column Meaning** 

# **Example** 

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND 

root         1  0.0  0.1 101456  8456 ?        Ss   10:00   0:01 /sbin/init 

labuser    456  0.0  0.2  10524  9672 pts/0    Ss   10:01   0:00 -bash 

# **Security Relevance** 

A security analyst can use process listings to identify: 

- Unexpected processes 

- Suspicious programs 

- High CPU-consuming processes 

- Processes running under unexpected users 

# **Result** 

Running Linux processes were successfully listed. 

# **2.2 Monitor Processes in Real Time** 

# **Command** 

top 

# **Purpose** 

top provides a real-time view of running processes and system resource usage. 

# **Information to Observe** 

- CPU utilization 

- Memory utilization 

- Running processes 

- Process IDs 

- Process users 

- Process resource consumption 

For example: 



<!-- Start of picture text -->
Hop - 11:53:32 up 16 min, 1 user, load average: 0.02, 0.08, 0.16<br>Tasks: 117 total, 1 running, 116 sleeping, @ stopped, 9 zombie<br>SCpu(s): @.@ us, @.@ sy, @.@ ni, 99.5 id, @.0 wa, @.@hi, @.5 si, 0.0 st<br>MiB Mem : 1642.6 total, 1118.2 free, 345.2 used, 324.0 buff /cache<br>MiB Swap: 1847.6 total, 1847.0 free, 6.6 used. 1297.4 avail Mem<br>PID USER PR_ NI VIRT RES SHRS CPU MEM TIME+ COMMAND<br>3 root 26 «8 8 8 6I 6.7 6.6 6:12.65 kworker/0:6-ata_sff<br>1978 labuser 26 8 10828 «66364 «4216 R 8.7) «68.4 =—-280.08 top<br>1 root 20 8 25324 16680 117045 6.0 1.6 9:15.49 systemd<br>2 root 20 8 8 e ®@S 6.0 8.0 6:00.05 kthreadd<br>3 root 26 () fs) () as 0.0 0.0 6:00.00 pool_workqueue_re lease<br>4 root @ -20 a a oI 8.8 0.0 6:00.00 kworker/R-rcu_gp<br>5 root @ -20 t) a 6I 6.0 6.6 6:00.00 kworker/R-sync_wq<br>6 root @ -20 8 ) @I 8.0 8.0 6:00.00 kworker/R-kyfree_rcu_reclaim<br>7 root @ -20 (3) 8 oI 8.8 0.0 6:00.00 kworker/R-slub_f lushwq<br>8 root @ -20 fs) () at 0.0 0.0 9:00.00 kworker/R-netns<br>12 root 20 8 8 ) @I 8.6 8.6 6:00.00 kworker/u8:0-ipv6é_addrcont<br>13 root @ -20 fs) () at 0.0 0.0 6:00.06 kworker/R-mm_percpu_wq<br>14 root 20 8 8 e 8S 8.0 6.6 6:00.55 ksoftirgd/e<br>15 root 20 () (7) () eI 0.0 6.0 6:01.08 rcu_preempt<br>16 root 26 () a () as 6.8 6.8 6:00.00 rcu_exp_par_gp_kthread_worker/@<br>17 root 20 () (7) () @s 0.8 0.0 6:00.09 rcu_exp_gp_kthread_worker<br>18 root rt C t) a 6S 6.0 8.0 6:00.03 migration’<br>19 root 26 () ta) ts) as 8.8 8.8 6:00.00 kprobe-optimizer<br>20 root -51 rc) i) rc) os 0.0 0.0 6:00.00 idle_inject/o<br>21 root 20 rc) i) 8 as 0.0 0.0 8:00.00 cpuhp/o<br>22 root 20 Q fa) Q as 0.0 0.0 6:00.00 cpuhp/1<br>23 root -51 () fs) (7) as 0.0 0.0 6:00.00 idle_inject/1<br>24 root an) 8 ) 9S 8.6 8.6 6:00.13 migration/1<br>25 root 20 C) Q C) as 0.0 0.0 0:00.49 ksoftirgd/1<br>28 root 26 C8 tc) a 6I 6.6 6.6 6:06.77 kworker/u9:6-events_power_efficient<br>29 root 20 8 ta) ts) oI 8.8 8.8 9:00.33 kworker/u10:0-events_unbound<br>38 root 20 «8 8 e @S 6.0 8.0 6:00.01 kdevtmpfs<br>31 root @ -20 8 ) @1I 8.6 8.6 6:60.00 kworker/R-inet_frag_wq<br>32 root 20 Q i) i) oI 0.0 0.0 6:00.06 rcu_tasks_kthread<br>33 root 20 «8 8 a 81 8.0 8.0 6:00.00 rcu_tasks_rude_kthread<br>34 root 20 Q i) Q os 0.0 0.0 0:00.01 kauditd<br>35 root 20 () a () as 0.0 0.0 6:00.01 khungtaskd<br>36 root 20 (7) 8 7) 6s 6.8 8.8 8:00.00 oom_reaper<br>37 root 20 «8 t) C) 9I 6.6 6.0 6:66.29 kworker/u9:1-flush-252:6<br>38 root 26 8 t) a 6I 6.6 6.6 6:06.27 kworker/u3:2-events_power_efficient<br>39 root @ -20 () () oI 8.8 8.0 6:00.00 kworker/R-writeback<br>40 root 20 «8 8 ) 8S 8.0 6.0 6:00.20 kcompactde<br>41 root 25 5 fs) Q as 0.0 0.0 0:00.00 ksmd<br>42 root 39 19 (7) () as 6.8 0.0 0:00.00 khugepaged<br>43 root @ -20 8 Q 6I 6.0 6.0 6:00.00 kworker/R-kblockd<br>44 root @ -20 8 Q @I 8.0 8.6 6:00.00 kworker/R-blkcg_punt_bio<br>4546 rootroot -51@ -200 88 ea @I05 6.68.0 8.66.0 6:60.006:00.00 kworker/R-kintegritydirg/9-acpi oe<br><!-- End of picture text -->

labuser@ubuntu-lab:~$ ps aux | grep sshd root 1764 8.8 6.4 10740 7780 ? Ss 11:44 8:00 : fusr/sbiné -D [listener] @ of 10-100 startups labuser 1989 6.6 @.1 6716 2600 ttyl St+ 11:54 6:00 grep --color=auto labuser@ubuntu-lab:~$ 



<!-- Start of picture text -->
labuser@ubuntu-lab:"€ sleep 1688&<br>[1] 1999<br>labuser@ubuntu-lab:“$ ps aux | grep 10a<br>labuserlabuser@ubuntu-lab:"$foie 6.8 8.1 6fl6 2646 ttyl St 11:55 6:68 grep- --color=auto<br><!-- End of picture text -->



<!-- Start of picture text -->
labuser@ubuntu-lab:"$ kill -9 1999<br>[1]+ Killed sleep 1908<br>labuser@ubuntu- lab:<br><!-- End of picture text -->



<!-- Start of picture text -->
labuser@ubuntu-lab:~$ sudo ss -tulpn<br>Net id State Recv-@ Send-Q Local Address:Port Peer Address:Port Process<br>udp UNCONN (7) () 127.0.0.54:53 0.0.0.0: users: (("'systemd-resolve",pid=856, fd=18 )<br>udp UNCONN a i) 127.6.6.53%10:53 8.0.0.0:% users: (('systemd-resolve",pid=856, fd=16 )<br>udp UNCONN @ t) 127.0.0.1:923 0.0.0.0:% users: (("'chronyd", pid=1378, fd=4 )<br>udp UNCONN (7) t) (::1] :323 (8B) ) Bk: users: (('"'chronyd", pid=1378, fd=5))<br>tcp LISTEN a 4096 127.6.0.54:53 0.0.0.0:% users: (('systemd-resolve",pid=856, fd=19 )<br>tcp LISTEN Q 4096 127.0.0.59%10:53 0.0.0.0: users: (("'systemd-resolve",pid=856, fd=17 )<br>tcptcp LISTENLISTEN (a)8 40964096 8.8.0.0:22[::] :22 8.0.0.0:(IG) BE users:users:(("sshd"(("'sshd'"',,pid=1764,pid=1764, fd=4)fd=3) ,, ("'systemd",("systemd" ,pid=1,pid=1, fd=92)fd=93)))<br>labuser@ubuntu-lab:“s<br><!-- End of picture text -->



<!-- Start of picture text -->
ubuntu-State:lab<br>Units: 436 loaded (incl. loaded aliases)<br>Jobs: @ queued<br>Failed: 6 units<br>Since: Wed 2026-08-12 11:37:62 UTC; 21min ago<br>systemd: 259.5-6ubuntu3<br>Tainted: unmerged-bin<br>CGroup:<br>init.scope<br>“1 susr/lib/systemd/systemd --switched-root --system --deserialize=48<br>system.slice<br>ModemManager. service<br>41375 /usr/sbin/ModemManager<br>chrony.service<br>1242 “bin/sh /usr/lib/systemd/scripts/chronyd-starter.sh -n -F 1<br>1378 /usr/sbin/chronyd -n -F 1<br>1392 /usr/sbin/chronyd -n -F 1<br>cron.service<br>“1243 /usr/sbin/cron -f -P<br>dbus. service<br>“1244 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only<br>mult ipathd.service<br>“833 /usr/sbin/multipathd -d -s<br>networkd-dispatcher.service<br>“4252 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers<br>polkit.service<br>“4253 /usr/lib/polkit-1/polkitd --no-debug --log-level=notice<br>rsyslog.service<br>1327 /usr/sbin/rsyslogd -n -iNONE<br>ssh.service<br>“1764 "sshd: /usr/sbin/sshd -D [listener] @ of 10-100 startups"<br>systemd-journald.service<br>“see /usr/lib/systemd/systemd-journald<br>systemd-logind.service<br>“1260 /usr/lib/systemd/systemd-logind<br>systemd-networkd.service<br>“1988 /usr/lib/systemd/systemd-networkd<br>systemd-resolved.service<br>Ces6 susr/lib/systemd/systemd-resolved<br>systemd-udevd. service<br>“udev<br>“s60 /usr/lib/systemd/systemd-udevd<br>udisks2.service<br>“1263 /usr/libexec/udisks2/udisksd<br>unattended-upgrades.service<br>“1336 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal<br>user.slice<br>Cuser-1000.slice<br>lines 1-49<br><!-- End of picture text -->

top 

an analyst can inspect currently running processes and resource consumption. 

This can help identify potentially suspicious processes. 

# **3. Network Exposure** 

Using: 

sudo ss -tulpn 

an analyst can determine which ports are listening and which processes are associated with those ports. 

For example: 

Port 22 → SSH → sshd 

This provides a basic connection between: 

Service → Process → Port 

which is very useful when investigating a Linux system. 

# **Command Summary** 

# **Command Purpose** 

systemctl status sshd Check SSH service status systemctl stop sshd Stop SSH service systemctl start sshd Start SSH service systemctl restart sshd Restart SSH service systemctl enable sshd Enable service at boot systemctl disable sshd Disable service at boot ps aux List running processes top Monitor processes in real time ps aux | grep sshd Find SSH-related processes sleep 1000 & Create a harmless background test process kill -9 PID Forcefully terminate a process ss -tulpn Display listening network sockets 

# **Command** 

# **Purpose** 

# **Key Takeaways** 

# **Service Management** 

systemctl 

is used to manage services controlled by systemd. 

# **Process Management** 

ps 

top 

kill 

can be used to view, monitor, and terminate processes. 

# **Network Monitoring** 

ss 

can be used to identify listening ports and associated processes. 

# **Important Relationship** 

A useful way to remember this lab is: 

SERVICE 

↓ 

# PROCESS 

↓ 

PORT 

For example: 

SSH Service 

↓ 

sshd Process 

↓ 

TCP Port 22 

# **Skills Demonstrated** 

- Linux Service Management 

- systemctl 

- systemd 

- Linux Process Management 

- Process Monitoring 

- ps 

- top 

- kill 

- Network Socket Analysis 

- TCP/UDP Port Identification 

- Listening Port Enumeration 

- SSH Service Management 

- Basic Linux Security Monitoring 

- Basic SOC Investigation 

# **Conclusion** 

This lab provided hands-on experience with Linux service, process, and network management. The SSH service was started, stopped, restarted, enabled, and disabled to understand service lifecycle management. 

Running processes were then examined using ps and top, while a harmless sleep process was created and terminated to practice process management safely. Finally, the ss command was used to identify listening network ports and associate them with running services. 

These skills are particularly useful in **Linux administration, SOC operations, incident response, and security monitoring** , where analysts may need to determine whether an unexpected service, process, or listening port is present on a system. 

