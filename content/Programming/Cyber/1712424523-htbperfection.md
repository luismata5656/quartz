---
id: 1712424523-htbperfection
aliases:
  - htb_perfection
tags: []
---

# htb_perfection

> Started on: 2024-04-06

## Host Information

TARGET_IP: 10.10.11.253
TARGET_OS: linux

## Enumeration

### nmap

```
# Nmap 7.94SVN scan initiated Sat Apr  6 11:37:09 2024 as: nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -p- -oN /home/two/Boxes/Perfection/enum/results/10.10.11.253/scans/_full_tcp_nmap.txt -oX /home/two/Boxes/Perfection/enum/results/10.10.11.253/scans/xml/_full_tcp_nmap.xml 10.10.11.253
Nmap scan report for 10.10.11.253
Host is up, received user-set (0.062s latency).
Scanned at 2024-04-06 11:37:09 MDT for 30s
Not shown: 65533 closed tcp ports (conn-refused)
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 80:e4:79:e8:59:28:df:95:2d:ad:57:4a:46:04:ea:70 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMz41H9QQUPCXN7lJsU+fbjZ/vR4Ho/eacq8LnS89xLx4vsJvjUJCcZgMYAmhHLXIGKnVv16ipqPaDom5cK9tig=
|   256 e9:ea:0c:1d:86:13:ed:95:a9:d0:0b:c8:22:e4:cf:e9 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBqNwnyqGqYHNSIjQnv7hRU0UC9Q4oB4g9Pfzuj2qcG4
80/tcp open  http    syn-ack nginx
| http-methods:
|_  Supported Methods: GET HEAD
|_http-title: Weighted Grade Calculator
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Apr  6 11:37:39 2024 -- 1 IP address (1 host up) scanned in 30.17 seconds
```

### rustscan

```bash
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
🌍HACK THE PLANET🌍

[~] The config file is expected to be at "/home/two/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.
Open 10.10.11.253:22
Open 10.10.11.253:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-06 11:37 MDT
Initiating Ping Scan at 11:37
Scanning 10.10.11.253 [2 ports]
Completed Ping Scan at 11:37, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 11:37
Completed Parallel DNS resolution of 1 host. at 11:37, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 11:37
Scanning 10.10.11.253 [2 ports]
Discovered open port 80/tcp on 10.10.11.253
Discovered open port 22/tcp on 10.10.11.253
Completed Connect Scan at 11:37, 0.06s elapsed (2 total ports)
Nmap scan report for 10.10.11.253
Host is up, received syn-ack (0.062s latency).
Scanned at 2024-04-06 11:37:15 MDT for 1s

PORT   STATE SERVICE REASON
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.17 seconds
```

## Exploration

This is obviously web exploitation, there is a information disclosure vuln at the bottom of the site:

![HTB_Perfection001.png](assets/imgs/HTB_Perfection001.png)

Got the ruby version:

![HTB_Perfection_002.png](assets/imgs/HTB_Perfection_002.png)

## Foothold

## Privilege Escalation

# Refeerences

-
