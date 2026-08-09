# IAM_LAB_PORTFOLIO
# 🛡️ IAM Lab Portfolio – Active Directory & Networking

**Author:** Jeal Patel  
**Start Date:** July 2026  
**Current Progress:** Weeks 1 & 2 Complete  
**Goal:** Build hands-on skills for IAM, SOC, and System Administration roles.

---

## 📋 Table of Contents
- [Lab Architecture](#-lab-architecture)
- [Week 1: Active Directory Foundation](#-week-1-active-directory-foundation)
- [Week 2: Networking for IAM](#-week-2-networking-for-iam)
- [Week 3: Linux Fundamentals (Coming Soon)](#-week-3-linux-fundamentals-coming-soon)
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
| **Ubuntu Server** | Ubuntu 26.04 LTS – `172.16.0.100/24` (Week 3) |
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
- `IAM_Lab_1.docx` – Day 1: OU Structure & Users
- `IAM_Lab_2.docx` – Day 2: Groups & RBAC
- `IAM_Lab_3.docx` – Day 3: Delegation
- `IAM_Lab_4.docx` – Day 4: Shared Folders
- `IAM_Lab_5.docx` – Day 5: PowerShell Automation
- `IAM_Lab_6.docx` – Day 6: Account Lockouts
- `Week1Summary.docx` – Weekly Review

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
- `Day8_DNS.png` – DNS Manager & `nslookup`
- `Day9_DHCP.png` – DHCP leases
- `Day10_Commands.txt` – Top 10 Network Commands
- `Day11_DNS_Capture.png` – Wireshark DNS capture
- `Day11_Kerberos_Capture.png` – Wireshark Kerberos capture
- `Day11_LDAP_Capture.png` – Wireshark LDAP capture
- `Day11_PCAP_Saved.png` – PCAP file saved
- `Day12_DNS_Broken.png` – DNS failure
- `Day12_DNS_Fixed.png` – DNS restored
- `Day12_DNS_Troubleshooting.txt` – Troubleshooting document
- `Day13_Subnetting.txt` – Subnetting cheat sheet
- `Day14_Network_Diagram.png` – Network diagram
- `Week2_Summary.docx` – Weekly review

---

## 🐧 Week 3: Linux Fundamentals (Coming Soon)

### Planned Topics
| Day | Topic |
| :--- | :--- |
| **Day 15** | Installing Ubuntu Server |
| **Day 16** | Linux File System & Navigation |
| **Day 17** | Linux Logs & Security Monitoring |
| **Day 18** | Linux Services & Process Management |
| **Day 19** | Linux Networking Commands |
| **Day 20** | Bash Scripting for Automation |
| **Day 21** | Weekly Review & Portfolio Update |

---

## 📜 Certifications (In Progress)

| Certification | Status |
| :--- | :--- |
| **Microsoft SC-300** (IAM) | 🟡 Planned (After Month 2) |
| **CompTIA Security+** | 🟡 Planned |

---

## 📂 Portfolio Structure
