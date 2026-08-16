🛡️ IAM Lab Portfolio – Active Directory & Networking (Updated: Week 3 Complete)
Author: Jeal Patel
Start Date: July 2026
Current Progress: Weeks 1, 2 & 3 Complete
Goal: Build hands-on skills for IAM, SOC, and System Administration roles.

📋 Table of Contents
Lab Architecture

Week 1: Active Directory Foundation

Week 2: Networking for IAM

Week 3: Linux Fundamentals

Week 4: Group Policy & Security Hardening (Coming Soon)

Certifications

Portfolio Structure

🖥️ Lab Architecture
Component	Details
Host Machine	Laptop with 8 GB RAM, Windows 11
Virtualization	Oracle VirtualBox 7.x
Domain Controller	Windows Server 2019 – 172.16.0.1
Windows Client	Windows 11 Pro – 172.16.0.50
Ubuntu Server	Ubuntu 26.04 LTS – 172.16.0.100/24
Domain	mydomain.com
Subnet	172.16.0.0/24 (255.255.255.0)
DHCP Range	172.16.0.100 – 172.16.0.200
📅 Week 1: Active Directory Foundation
What I Built
Domain Controller (DC-Server) running Windows Server 2019

Active Directory Domain (mydomain.com)

Organizational Units (OUs): _ADMINS, _EMPLOYEES (IT, HR, Sales), _GROUPS

Users: Created 15+ users (manual + PowerShell)

Security Groups: IT_Team, HR_Team, Sales_Team

RBAC: Implemented Role-Based Access Control

Delegation: Delegated password reset permissions to IT_Team

Shared Folders: NTFS & Share permissions for department folders

Group Policy: Password policy enforced

PowerShell Automation: Scripts to create 10+ users and export reports

Key Skills Learned
Skill	Description
Active Directory	Built a Domain Controller from scratch
OU Management	Structured AD for security and delegation
RBAC	Users → Groups → Permissions
Delegation	Least Privilege principle applied
PowerShell	Automated user creation and reporting
Week 1 Deliverables
IAM_Lab_1.docx – Day 1: OU Structure & Users

IAM_Lab_2.docx – Day 2: Groups & RBAC

IAM_Lab_3.docx – Day 3: Delegation

IAM_Lab_4.docx – Day 4: Shared Folders

IAM_Lab_5.docx – Day 5: PowerShell Automation

IAM_Lab_6.docx – Day 6: Account Lockouts

Week1Summary.docx – Weekly Review

🌐 Week 2: Networking for IAM
What I Learned
Day	Topic	Key Takeaway
Day 8	DNS Fundamentals	DNS translates names to IPs. A Records = Name → IP. PTR = IP → Name.
Day 9	DHCP & IP Addressing	DHCP auto-assigns IPs. DORA = Discover, Offer, Request, Acknowledge. APIPA = 169.254.x.x (when DHCP fails).
Day 10	Network Commands	ping, tracert, nslookup, netstat – the core troubleshooting toolkit.
Day 11	Wireshark	Captured DNS, Kerberos (AS-REQ/AS-REP), and LDAP traffic.
Day 12	DNS Break & Fix	"If you can ping the IP but not the name, it's DNS."
Day 13	Subnetting	Calculated /24, /16, /8 networks and understood CIDR notation.
Day 14	Review	Documented everything and updated portfolio.
Key Ports for IAM
Port	Protocol	Purpose
53	TCP/UDP	DNS – Name resolution
88	TCP/UDP	Kerberos – Authentication
389	TCP/UDP	LDAP – Directory queries
445	TCP	SMB – File sharing
636	TCP	LDAPS – Secure LDAP
3389	TCP	RDP – Remote Desktop
Week 2 Deliverables
Day8_DNS.png – DNS Manager & nslookup

Day9_DHCP.png – DHCP leases

Day10_Commands.txt – Top 10 Network Commands

Day11_DNS_Capture.png – Wireshark DNS capture

Day11_Kerberos_Capture.png – Wireshark Kerberos capture

Day11_LDAP_Capture.png – Wireshark LDAP capture

Day11_PCAP_Saved.png – PCAP file saved

Day12_DNS_Broken.png – DNS failure

Day12_DNS_Fixed.png – DNS restored

Day12_DNS_Troubleshooting.txt – Troubleshooting document

Day13_Subnetting.txt – Subnetting cheat sheet

Day14_Network_Diagram.png – Network diagram

Week2_Summary.docx – Weekly review

🐧 Week 3: Linux Fundamentals
What I Learned
Day	Topic	Key Takeaway
Day 15	Installing Ubuntu Server	Installed Ubuntu 26.04 LTS with static IP (172.16.0.100/24) and fixed DNS using Netplan.
Day 16	Linux File System & Navigation	Learned pwd, ls -la, cd, mkdir, touch, cp, mv, rm; understood absolute vs relative paths and file permissions (chmod, chown).
Day 17	Linux Logs & Security Monitoring	Monitored /var/log/auth.log; used tail -f, grep "Failed password", and awk to detect failed SSH logins.
Day 18	Linux Services & Process Management	Managed services with systemctl; monitored processes with ps aux, top; checked listening ports with sudo ss -tulpn.
Day 19	Linux Networking Commands	Used ip addr, ip route, ping, dig, nslookup, curl, and ss -tulpn for network troubleshooting.
Day 20	Bash Scripting for Automation	Created 4 scripts: check_failed_logins.sh, count_failed_by_ip.sh, system_health.sh, and alert_failed_logins.sh.
Day 21	Review	Documented all Linux commands and updated portfolio.
Key Linux Commands Learned
Navigation & File Management
Command	Purpose
pwd	Print Working Directory
ls -la	List all files (including hidden) with details
cd /	Go to root directory
cd ~	Go to home directory
mkdir	Create a directory
touch	Create an empty file
cp	Copy a file
mv	Move or rename a file
rm	Remove a file
Log Analysis
Command	Purpose
sudo tail -f /var/log/auth.log	View auth logs in real-time
sudo grep "Failed password" /var/log/auth.log	Find failed logins
sudo grep "Accepted password" /var/log/auth.log	Find successful logins
sudo journalctl -xe	View systemd logs with errors
Service & Process Management
Command	Purpose
sudo systemctl status sshd	Check SSH service status
sudo systemctl start/stop/restart sshd	Start/Stop/Restart SSH
sudo systemctl enable/disable sshd	Enable/Disable at boot
ps aux	List all running processes
top	Real-time process viewer
kill -9 PID	Force stop a process
Networking
Command	Purpose
ip addr	Show IP addresses
ip route	Show routing table
ping -c 4 172.16.0.1	Test connectivity to DC
dig mydomain.com	Detailed DNS query
nslookup mydomain.com	Simple DNS query
curl -v http://172.16.0.1	HTTP request to DC
sudo ss -tulpn	List listening ports
Bash Scripts Created
check_failed_logins.sh – Shows the last 10 failed login attempts

count_failed_by_ip.sh – Counts failed logins by IP address

system_health.sh – Quick system health check (uptime, memory, disk)

alert_failed_logins.sh – Alerts if more than 10 failed logins detected

Week 3 Deliverables
Day15_Ubuntu_Installed.png – Ubuntu installation screenshot

Day15_Ubuntu_DNS_Fixed.png – DNS resolution working

Day16_pwd.png – pwd output in home directory

Day16_ls_la.png – ls -la showing hidden files

Day16_chmod.png – chmod 755 and ls -l output

Day17_Failed_Login.png – grep "Failed password" output

Day17_SSH_Connection.png – SSH connection from Win11-Client

Day18_systemctl_status.png – systemctl status sshd output

Day18_ss.png – sudo ss -tulpn output

Day19_ip_addr.png – ip addr output

Day19_ping_DC.png – ping 172.16.0.1 -c 4 output

Day19_dig.png – dig mydomain.com output

Day20_Script1.png – ./check_failed_logins.sh output

Day20_Script2.png – ./count_failed_by_ip.sh output

Day20_Script3.png – ./system_health.sh output

check_failed_logins.sh – Bash script

count_failed_by_ip.sh – Bash script

system_health.sh – Bash script

alert_failed_logins.sh – Bash script

00-installer-config.yaml – Netplan configuration

Week3_Summary.docx – Weekly review

📜 Certifications (In Progress)
Certification	Status
Microsoft SC-300 (IAM)	🟡 Planned (After Month 2)
CompTIA Security+	🟡 Planned
📂 Portfolio Structure
text
IAM_Lab_Portfolio/
├── Week 1/
│   ├── Screenshots/
│   ├── Documents/
│   └── Scripts/
├── Week 2/
│   ├── Screenshots/
│   ├── Documents/
│   └── PCAPs/
├── Week 3/
│   ├── Screenshots/
│   ├── Scripts/
│   ├── Configs/
│   └── Documents/
├── README.md
└── LICENSE
🔗 Connect With Me
LinkedIn: https://www.linkedin.com/in/jeal-patel-91aa78318/

GitHub: https://github.com/JealPatel/

📝 License
This repository is for educational and portfolio purposes. Feel free to use it as a reference for your own learning journey.
