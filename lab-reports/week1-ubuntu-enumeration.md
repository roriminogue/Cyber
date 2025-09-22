markdown# Week 1: Ubuntu Target Enumeration

**Date:** 22/09/2025
**Target:** Ubuntu 24.04 LTS (192.168.56.20)
**Attacker:** Kali Linux (192.168.56.10)

## Lab Environment
- **Kali Linux:** 192.168.56.10 (Attack Machine)
- **Ubuntu Target:** 192.168.56.20 (Target Machine)
- **Network:** VirtualBox Host-Only Adapter (Isolated)

## Initial Scan - Fresh Ubuntu
Nmap 7.95 scan initiated Mon Sep 22 02:56:35 2025 as: /usr/lib/nmap/nmap -sV -sC -O -oN ubuntu-services-scan.txt 192.168.56.20
Nmap scan report for 192.168.56.20
Host is up (0.0018s latency).
Not shown: 998 closed tcp ports (reset)

**Finding:** Default Ubuntu desktop has no exposed services - secure by default!

## Services Installed
To create a realistic target environment:
- OpenSSH Server (remote administration)
- Apache2 Web Server (web hosting)

## Full Service Scan Results
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.14 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 cd:f2:78:50:89:b1:d8:27:a2:2d:52:40:a9:e5:e9:f4 (ECDSA)
|_  256 ba:ee:2a:e3:cd:30:7f:b3:fc:3f:c1:96:99:fe:71:f4 (ED25519)
80/tcp open  http    Apache httpd 2.4.58 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.58 (Ubuntu)

## Verification Tests
- ✅ SSH Login: Successfully authenticated as vboxuser
- ✅ Apache: Default page serving at http://192.168.56.20

## Security Observations
1. SSH accepts password authentication (potential brute-force vector)
2. Apache version disclosed in headers (Apache/2.4.58)
3. Ubuntu version visible in SSH banner
4. No firewall rules configured
5. Default Apache page reveals OS information

## Next Steps
- Install DVWA for web vulnerability testing
- Configure fail2ban for SSH protection
- Test for weak SSH passwords
- Enumerate web directories with Gobuster
