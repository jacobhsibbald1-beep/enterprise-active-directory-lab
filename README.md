# Enterprise Active Directory Lab

# Overview
I built this Active Directory lab to simulate a small business MSP-style environment using Windows Server 2022 and Windows 10 Pro inside VirtualBox.

The goal was to deploy a working domain controller, configure DNS correctly, join a client machine, validate Kerberos authentication, and troubleshoot real networking issues along the way.

This lab forced me to diagnose problems at multiple layers (network routing, DNS resolution, ARP behaviour, and domain discovery) rather than just following a step-by-step guide.


 # Lab Architecture

# Virtualisation
- Platform: Oracle VirtualBox
- Network Model:
  - Adapter 1: NAT (Internet access)
  - Adapter 2: Internal Network (intnet-lab)

# Domain Controller
- VM Name: WIN-DC
- OS: Windows Server 2022
- IP Address: 192.168.100.10
- Subnet: 255.255.255.0
- DNS: Self (192.168.100.10)
- Roles Installed:
  - Active Directory Domain Services
  - DNS Server

# Domain
- Domain Name: bmits.local

# Client Machine
- VM Name: WIN-CLIENT02
- OS: Windows 10 Pro
- IP Address: 192.168.100.50
- DNS: 192.168.100.10
- Successfully domain joined

# Features Implemented
- Active Directory Domain Services deployment
- AD-integrated DNS zone
- SRV record validation
- Static IP configuration
- Internal network segmentation
- Domain join process
- Kerberos authentication validation
- Organisational Units
- Security groups
- NTFS + Share permissions configuration
- File share with group-based access control

# Validation Performed

# DNS Resolution
nslookup bmits.local  
nslookup -type=SRV _ldap._tcp.dc._msdcs.bmits.local

# Domain Authentication
whoami  
echo %logonserver%  

Confirmed authentication against the domain controller (Kerberos).

# Network Testing
ping 192.168.100.10  
ipconfig  

Verified Layer 2 and Layer 3 connectivity.

# Troubleshooting Experience
During deployment several real-world infrastructure issues were encountered and resolved:

- IPv6 auto-configuration causing routing conflicts
- NAT DNS overriding internal AD DNS
- Incorrect DNS configuration breaking domain join
- Internal virtual network isolation issues
- ARP resolution troubleshooting at Layer 2
- SRV record validation for domain discovery

Each issue was resolved using structured network-layer analysis (L2, L3, DNS, AD).

# Skills Demonstrated
- Active Directory infrastructure deployment
- DNS architecture understanding
- Windows Server role management
- Static IP network design
- Domain authentication flow
- Network troubleshooting methodology
- MSP-style infrastructure build discipline


# Future Roadmap
- Group Policy Object deployment
- Drive mapping via GPO
- DHCP role implementation
- Security baseline hardening
- Windows event log forwarding into Elastic SIEM
- Integration with Linux server environment


# Author
Jacob Sibbald  
Diploma of Information Technology  
Building enterprise-style homelab infrastructure for professional development.
