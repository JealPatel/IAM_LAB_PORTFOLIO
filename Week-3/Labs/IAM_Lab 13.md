**Complete Lab Setup Report: Ubuntu Server Installation & Network Configuration**

**Name:** Jeal Patel\
**Date:** August 2026\
**Lab Week:** Week 3 – Day 15\
**Objective:** Install Ubuntu Server 26.04 LTS on VirtualBox, configure networking, and integrate it into the existing Active Directory lab environment.

**Lab Environment**

| Component | Details |
|-----------------------|----------------------------------------------|
| **Host Machine** | Laptop with 8 GB RAM, Windows 11 |
| **Virtualization** | Oracle VirtualBox 7.x |
| **Domain Controller** | Windows Server 2019 (DC-Server) – 172.16.0.1 |
| **Windows Client** | Windows 11 Pro – 172.16.0.50 |
| **New VM** | Ubuntu Server 26.04 LTS – 172.16.0.100/24 |
| **Network** | Internal Network (intnet) |
| **Domain** | mydomain.com |
| **DNS Server** | 172.16.0.1 (DC-Server) |

**Step 1: Downloading Ubuntu Server ISO**

**Action:**\
Downloaded Ubuntu Server 26.04 LTS ISO from the official Ubuntu website.

**File:**\
ubuntu-26.04-live-server-amd64.iso (~3 GB)

**Storage:**\
Saved to D:\Downloads\\to save space on the C: drive.

**Step 2: Creating the Virtual Machine**

**Action:**\
Created a new VM in VirtualBox with the following specifications:

| Setting | Value |
|----------------|-------------------------------|
| **Name** | Ubuntu-Lab |
| **Folder** | D:\VirtualBox VMs\Ubuntu-Lab |
| **Type** | Linux |
| **Version** | Ubuntu (64-bit) |
| **RAM** | 2048 MB (2 GB) |
| **Processors** | 2 |
| **Storage** | 20 GB (dynamically allocated) |
| **Network** | Internal Network (intnet) |

**Step 3: Installing Ubuntu Server**

**Action:**\
Booted the VM from the ISO and followed the installation steps.

| Step | Selection |
|----------------|----------------------------------------------------------|
| **Language** | English |
| **Keyboard** | English (US) |
| **Network** | Manual configuration (Static IP) |
| **Proxy** | None |
| **Mirror** | Default (skipped due to no internet) |
| **Storage** | Use entire disk (LVM) |
| **Profile** | Name: labuser, Server: ubuntu-lab, Password: P@ssw0rd123 |
| **SSH** | Install OpenSSH server |
| **Snaps** | Skipped |
| **Ubuntu Pro** | Skipped |

**Step 4: Network Configuration (Static IP)**

**Challenge:**\
During installation, the network interface failed to get an IP address via DHCP.

**Root Cause:**\
The VM was set to Internal Network (intnet), and the DHCP server on the Domain Controller was not active or was unreachable.

**Solution:**\
Configured a static IP address manually during installation.

| Setting | Value |
|-------------------|---------------|
| **IP Address** | 172.16.0.100 |
| **Subnet Mask** | 255.255.255.0 |
| **Gateway** | 172.16.0.1 |
| **DNS Server** | 172.16.0.1 |
| **Search Domain** | mydomain.com |

**Final Network Configuration File (**/etc/netplan/00-installer-config.yaml**):**

yaml

network:

version: 2

ethernets:

enp0s3:

addresses:

\- 172.16.0.100/24

match:

macaddress: 08:00:27:9d:ef:a3

nameservers:

addresses:

\- 172.16.0.1

search:

\- mydomain.com

routes:

\- to: default

via: 172.16.0.1

set-name: enp0s3

**Step 5: Verifying Connectivity**

**Ping Test to Domain Controller**

bash

ping 172.16.0.1 -c 4

**Result:**

text

64 bytes from 172.16.0.1: icmp_seq=1 ttl=128 time=1.87 ms

64 bytes from 172.16.0.1: icmp_seq=2 ttl=128 time=1.13 ms

64 bytes from 172.16.0.1: icmp_seq=3 ttl=128 time=1.39 ms

64 bytes from 172.16.0.1: icmp_seq=4 ttl=128 time=0.832 ms

4 packets transmitted, 4 received, 0% packet loss

**DNS Resolution Test**

bash

nslookup mydomain.com

**Result:**

text

Server: 127.0.0.53

Address: 127.0.0.53#53

Non-authoritative answer:

Name: mydomain.com

Address: 172.16.0.1

Name: mydomain.com

Address: 10.0.2.15

Name: mydomain.com

Address: fd17:625c:f037:2:520e:e648:e656:bc7b

**Ping Test to Domain Name**

bash

ping mydomain.com -c 4

**Result:**

text

PING mydomain.com (172.16.0.1) 56(84) bytes of data.

64 bytes from 172.16.0.1: icmp_seq=1 ttl=128 time=0.5 ms

**Problems Faced and Solutions**

**Problem 1: Unattended Installation Option**

**Issue:**\
During VM creation, the "Set up unattended guest OS installation" option was checked by default.

**Solution:**\
Unchecked the box to perform a manual installation (better for learning).

**Problem 2: DHCP Autoconfiguration Failed**

**Issue:**\
Ubuntu installer showed autoconfiguration failed on the network interface.

**Cause:**\
The VM was on an Internal Network (intnet) without a working DHCP server.

**Solution:**\
Configured a static IP manually during installation.

**Problem 3: "Mirror Check Failed" Error**

**Issue:**\
During installation, the mirror check failed with the error:

text

Mirror check failed

**Cause:**\
The VM had no internet access (Internal Network only).

**Solution:**\
Selected \[ Continue \] and proceeded with the installation using only files from the ISO.

**Problem 4: DNS Resolution Error (127.0.0.53#53 timed out)**

**Issue:**\
After installation, nslookup mydomain.com failed with:

text

;; communications error to 127.0.0.53#53: timed out

**Cause:**\
The DNS server was not configured in the Netplan file.

**Solution:**\
Edited /etc/netplan/00-installer-config.yaml and added:

yaml

nameservers:

addresses:

\- 172.16.0.1

search:

\- mydomain.com

Then applied the configuration:

bash

sudo netplan apply

**Problem 5: Netplan Syntax Error**

**Issue:**\
YAML syntax error due to incorrect indentation in the Netplan file.

**Solution:**\
Used proper YAML formatting (2 spaces for indentation) and verified with:

bash

sudo netplan apply
