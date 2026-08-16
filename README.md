# 🛡️ IAM Lab Portfolio – Active Directory & Networking (Updated: Week 3 Complete)

**Author:** Jeal Patel  
**Start Date:** July 2026  
**Current Progress:** Weeks 1, 2 & 3 Complete  
**Goal:** Build hands-on skills for IAM, SOC, and System Administration roles.

---

## 📋 Table of Contents
- [Lab Architecture](#-lab-architecture)
- [Week 1: Active Directory Foundation](#-week-1-active-directory-foundation)
- [Week 2: Networking for IAM](#-week-2-networking-for-iam)
- [Week 3: Linux Fundamentals](#-week-3-linux-fundamentals)
- [Week 4: Group Policy & Security Hardening (Coming Soon)](#-week-4-group-policy--security-hardening-coming-soon)
- [Certifications](#-certifications)
- [Portfolio Structure](#-portfolio-structure)

---

## 🖥️ Lab Architecture

| Component | Details |
| :--- | :--- |
| **Host Machine** | Laptop with 8 GB RAM, Windows 11 |
| **Virtualization** | Oracle VirtualBox 7.x |
| **Domain Controller** | Windows Server 2019 – `172.16.0.1` |
| **Windows Client** | Windows 11 Pro – `172.16.0.50` |
| **Ubuntu Server** | Ubuntu 26.04 LTS – `172.16.0.100/24` |
| **Domain** | `mydomain.com` |
| **Subnet** | `172.16.0.0/24` (`255.255.255.0`) |
| **DHCP Range** | `172.16.0.100` – `172.16.0.200` |

---

## 📅 Week 1: Active Directory Foundation

### What I Built
- **Domain Controller** (`DC-Server`) running Windows Server 2019
- **Active Directory Domain** (`mydomain.com`)
- **Organizational Units (OUs):** `_ADMINS`, `_EMPLOYEES` (IT, HR, Sales), `_GROUPS`
- **Users:** Created 15+ users (manual + PowerShell)
- **Security Groups:** `IT_Team`, `HR_Team`, `Sales_Team`
- **RBAC:** Implemented Role-Based Access Control
- **Delegation:** Delegated password reset permissions to `IT_Team`
- **Shared Folders:** NTFS & Share permissions for department folders
- **Group Policy:** Password policy enforced
- **PowerShell Automation:** Scripts to create 10+ users and export reports

### Key Skills Learned
| Skill | Description |
| :--- | :--- |
| Active Directory | Built a Domain Controller from scratch |
| OU Management | Structured AD for security and delegation |
| RBAC | Users → Groups → Permissions |
| Delegation | Least Privilege principle applied |
| PowerShell | Automated user creation and reporting |

### Week 1 Deliverables
| Lab | Topic | Markdown | Images |
| :--- | :--- | :--- | :--- |
| **Lab 01** | OU Structure & Users | [View](Week-1/Labs/IAM_Lab_01.md) | [Images](Week-1/Images/) |
| **Lab 02** | Groups & RBAC | [View](Week-1/Labs/IAM_Lab_02.md) | [Images](Week-1/Images/) |
| **Lab 03** | Delegation | [View](Week-1/Labs/IAM_Lab_03.md) | [Images](Week-1/Images/) |
| **Lab 04** | Shared Folders | [View](Week-1/Labs/IAM_Lab_04.md) | [Images](Week-1/Images/) |
| **Lab 05** | PowerShell Automation | [View](Week-1/Labs/IAM_Lab_05.md) | [Images](Week-1/Images/) |
| **Lab 06** | Account Lockouts | [View](Week-1/Labs/IAM_Lab_06.md) | [Images](Week-1/Images/) |

---

## 🌐 Week 2: Networking for IAM

### What I Learned
| Day | Topic | Key Takeaway |
| :--- | :--- | :--- |
| **Day 8** | DNS Fundamentals | DNS translates names to IPs. A Records = Name → IP. PTR = IP → Name. |
| **Day 9** | DHCP & IP Addressing | DHCP auto-assigns IPs. DORA = Discover, Offer, Request, Acknowledge. APIPA = `169.254.x.x` (when DHCP fails). |
| **Day 10** | Network Commands | `ping`, `tracert`, `nslookup`, `netstat` – the core troubleshooting toolkit. |
| **Day 11** | Wireshark | Captured DNS, Kerberos (AS-REQ/AS-REP), and LDAP traffic. |
| **Day 12** | DNS Break & Fix | *"If you can ping the IP but not the name, it's DNS."* |
| **Day 13** | Subnetting | Calculated `/24`, `/16`, `/8` networks and understood CIDR notation. |
| **Day 14** | Review | Documented everything and updated portfolio. |

### Key Ports for IAM
| Port | Protocol | Purpose |
| :--- | :--- | :--- |
| **53** | TCP/UDP | DNS – Name resolution |
| **88** | TCP/UDP | Kerberos – Authentication |
| **389** | TCP/UDP | LDAP – Directory queries |
| **445** | TCP | SMB – File sharing |
| **636** | TCP | LDAPS – Secure LDAP |
| **3389** | TCP | RDP – Remote Desktop |

### Week 2 Deliverables
| Lab | Topic | Markdown | Images |
| :--- | :--- | :--- | :--- |
| **Lab 07** | DNS Fundamentals | [View](Week-2/Labs/IAM_Lab_07.md) | [Images](Week-2/Images/) |
| **Lab 08** | DHCP & IP Addressing | [View](Week-2/Labs/IAM_Lab_08.md) | [Images](Week-2/Images/) |
| **Lab 09** | Network Troubleshooting | [View](Week-2/Labs/IAM_Lab_09.md) | [Images](Week-2/Images/) |
| **Lab 10** | Wireshark | [View](Week-2/Labs/IAM_Lab_10.md) | [Images](Week-2/Images/) |
| **Lab 11** | DNS Break & Fix | [View](Week-2/Labs/IAM_Lab_11.md) | [Images](Week-2/Images/) |
| **Lab 12** | Subnetting | [View](Week-2/Labs/IAM_Lab_12.md) | [Images](Week-2/Images/) |
| **Lab 13** | Weekly Review | [View](Week-2/Labs/IAM_Lab_13.md) | [Images](Week-2/Images/) |

---

## 🐧 Week 3: Linux Fundamentals

### What I Learned
| Day | Topic | Key Takeaway |
| :--- | :--- | :--- |
| **Day 15** | Installing Ubuntu Server | Installed Ubuntu 26.04 LTS with static IP (`172.16.0.100/24`) and fixed DNS using Netplan. |
| **Day 16** | Linux File System & Navigation | Learned `pwd`, `ls -la`, `cd`, `mkdir`, `touch`, `cp`, `mv`, `rm`; understood absolute vs relative paths and file permissions (`chmod`, `chown`). |
| **Day 17** | Linux Logs & Security Monitoring | Monitored `/var/log/auth.log`; used `tail -f`, `grep "Failed password"`, and `awk` to detect failed SSH logins. |
| **Day 18** | Linux Services & Process Management | Managed services with `systemctl`; monitored processes with `ps aux`, `top`; checked listening ports with `sudo ss -tulpn`. |
| **Day 19** | Linux Networking Commands | Used `ip addr`, `ip route`, `ping`, `dig`, `nslookup`, `curl`, and `ss -tulpn` for network troubleshooting. |
| **Day 20** | Bash Scripting for Automation | Created 4 scripts: `check_failed_logins.sh`, `count_failed_by_ip.sh`, `system_health.sh`, and `alert_failed_logins.sh`. |
| **Day 21** | Review | Documented all Linux commands and updated portfolio. |

### Key Linux Commands Learned
#### Navigation & File Management
| Command | Purpose |
| :--- | :--- |
| `pwd` | Print Working Directory |
| `ls -la` | List all files (including hidden) with details |
| `cd /` | Go to root directory |
| `cd ~` | Go to home directory |
| `mkdir` | Create a directory |
| `touch` | Create an empty file |
| `cp` | Copy a file |
| `mv` | Move or rename a file |
| `rm` | Remove a file |

#### Log Analysis
| Command | Purpose |
| :--- | :--- |
| `sudo tail -f /var/log/auth.log` | View auth logs in real-time |
| `sudo grep "Failed password" /var/log/auth.log` | Find failed logins |
| `sudo grep "Accepted password" /var/log/auth.log` | Find successful logins |
| `sudo journalctl -xe` | View systemd logs with errors |

#### Service & Process Management
| Command | Purpose |
| :--- | :--- |
| `sudo systemctl status sshd` | Check SSH service status |
| `sudo systemctl start/stop/restart sshd` | Start/Stop/Restart SSH |
| `sudo systemctl enable/disable sshd` | Enable/Disable at boot |
| `ps aux` | List all running processes |
| `top` | Real-time process viewer |
| `kill -9 PID` | Force stop a process |

#### Networking
| Command | Purpose |
| :--- | :--- |
| `ip addr` | Show IP addresses |
| `ip route` | Show routing table |
| `ping -c 4 172.16.0.1` | Test connectivity to DC |
| `dig mydomain.com` | Detailed DNS query |
| `nslookup mydomain.com` | Simple DNS query |
| `curl -v http://172.16.0.1` | HTTP request to DC |
| `sudo ss -tulpn` | List listening ports |

### Bash Scripts Created
1. **`check_failed_logins.sh`** – Shows the last 10 failed login attempts
2. **`count_failed_by_ip.sh`** – Counts failed logins by IP address
3. **`system_health.sh`** – Quick system health check (uptime, memory, disk)
4. **`alert_failed_logins.sh`** – Alerts if more than 10 failed logins detected

### Week 3 Deliverables
| Lab | Topic | Markdown | Images |
| :--- | :--- | :--- | :--- |
| **Lab 14** | Ubuntu Installation | [View](Week-3/Labs/IAM_Lab_14.md) | [Images](Week-3/Images/) |
| **Lab 15** | Linux File System | [View](Week-3/Labs/IAM_Lab_15.md) | [Images](Week-3/Images/) |
| **Lab 16** | Linux Logs | [View](Week-3/Labs/IAM_Lab_16.md) | [Images](Week-3/Images/) |
| **Lab 17** | Linux Services | [View](Week-3/Labs/IAM_Lab_17.md) | [Images](Week-3/Images/) |
| **Lab 18** | Bash Scripting | [View](Week-3/Labs/IAM_Lab_18.md) | [Images](Week-3/Images/) |

---

## 📜 Certifications (In Progress)

| Certification | Status |
| :--- | :--- |
| **Microsoft SC-300** (IAM) | 🟡 Planned (After Month 2) |
| **CompTIA Security+** | 🟡 Planned |

---

## 📂 Portfolio Structure
