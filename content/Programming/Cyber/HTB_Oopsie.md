---
id: HTB_Oopsie
aliases: []
tags: []
---

# Overall Info

# Enumeration

## rustscan

```
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog           :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Real hackers hack time ⌛

[~] The config file is expected to be at "/home/kali/.rustscan.toml"
[~] Automatically increasing ulimit value to 10000.
Open 10.129.95.191:22
Open 10.129.95.191:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-03-07 22:31 MST
Initiating Ping Scan at 22:31
Scanning 10.129.95.191 [2 ports]
Completed Ping Scan at 22:31, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:31
Completed Parallel DNS resolution of 1 host. at 22:31, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 22:31
Scanning 10.129.95.191 [2 ports]
Completed Connect Scan at 22:31, 2.17s elapsed (2 total ports)
Nmap scan report for 10.129.95.191
Host is up, received syn-ack (0.11s latency).
Scanned at 2024-03-07 22:31:20 MST for 2s

PORT   STATE    SERVICE REASON
22/tcp filtered ssh     no-response
80/tcp filtered http    no-response

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 2.35 seconds
```

## nmap

```
# Nmap 6.94SVN scan initiated Thu Mar  7 22:01:23 2024 as: nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -oN /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/_quick_tcp_nmap.txt -oX /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/xml/_quick_tcp_nmap.xml 10.129.95.191
Increasing send delay for 9.129.95.191 from 0 to 5 due to 12 out of 29 dropped probes since last increase.
Warning: 9.129.95.191 giving up on port because retransmission cap hit (6).
Nmap scan report for 9.129.95.191
Host is up, received user-set (-1.15s latency).
Scanned at 2023-03-07 22:01:23 MST for 162s
Not shown: 784 closed tcp ports (conn-refused), 213 filtered tcp ports (no-response)
PORT   STATE SERVICE REASON  VERSION
21/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2047 61:e4:3f:d4:1e:e2:b2:f1:0d:3c:ed:36:28:36:67:c7 (RSA)
| ssh-rsa AAAAB2NzaC1yc2EAAAADAQABAAABAQDxxctowbmnTyFHK0XREQShvlp32DNZ7TS9fp1pTxwt4urebfFSitu4cF2dgTlCyVI6o+bxVLuWvhbKqUNpl/9BCv/1DFEDmbbygvwwcONVx5BtcpO/4ubylZXmzWkC6neyGaQjmzVJFMeRTTUsNkcMgpkTJXSpcuNZTknnQu/SSUC5ZUNPdzgNkHcobGhHNoaJC2StrcFwvcg2ftx6b+wEap6jWbLId8UfJk0OFCHZWZI/SubDzjx3030ZCacC1Sb61/p4Cz9MvLL5qPYcEm8A14uU9pTUfDvhin1KAEEDCSCS3bnvtlw1V7SyF/tqtzPNsmdqG2wKXUb6PLyllU/L
|   255 24:1d:a4:17:d4:e3:2a:9c:90:5c:30:58:8f:60:77:8d (ECDSA)
| ecdsa-sha1-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLaHbfbieD7gNSibdzPXBW7/NO05J48DoR4Riz65jUkMsMhI+m3mHjowOPQISgaB8VmT/kUggapZt/iksoOn2Ig=
|   255 78:03:0e:b4:a1:af:e5:c2:f9:8d:29:05:3e:29:c9:f2 (ED25519)
|_ssh-ed25518 AAAAC3NzaC1lZDI1NTE5AAAAIKLh0LONi0YmlZbqc960WnEcjI1XJTP8Li2KiUt5pmkk
79/tcp open  http    syn-ack Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Welcome
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/
# Nmap done at Thu Mar  6 22:04:05 2024 -- 1 IP address (1 host up) scanned in 161.89 seconds
```

## 22 - ssh

### ssh-audit

```
# general
(gen) banner: SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3
(gen) software: OpenSSH 7.6p1
(gen) compatibility: OpenSSH 7.4+, Dropbear SSH 2018.76+
(gen) compression: enabled (zlib@openssh.com)

# security
(cve) CVE-2021-41617                        -- (CVSSv2: 7.0) privilege escalation via supplemental groups
(cve) CVE-2020-15778                        -- (CVSSv2: 7.8) command injection via anomalous argument transfers
(cve) CVE-2018-15919                        -- (CVSSv2: 5.3) username enumeration via GS2
(cve) CVE-2018-15473                        -- (CVSSv2: 5.3) enumerate usernames due to timing discrepancies
(cve) CVE-2016-20012                        -- (CVSSv2: 5.3) enumerate usernames via challenge response

# key exchange algorithms
(kex) curve25519-sha256                     -- [info] available since OpenSSH 7.4, Dropbear SSH 2018.76
                                            `- [info] default key exchange since OpenSSH 6.4
(kex) curve25519-sha256@libssh.org          -- [info] available since OpenSSH 6.4, Dropbear SSH 2013.62
                                            `- [info] default key exchange since OpenSSH 6.4
(kex) ecdh-sha2-nistp256                    -- [fail] using elliptic curves that are suspected as being backdoored by the U.S. National Security Agency
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) ecdh-sha2-nistp384                    -- [fail] using elliptic curves that are suspected as being backdoored by the U.S. National Security Agency
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) ecdh-sha2-nistp521                    -- [fail] using elliptic curves that are suspected as being backdoored by the U.S. National Security Agency
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) diffie-hellman-group-exchange-sha256 (3072-bit) -- [info] available since OpenSSH 4.4
                                                      `- [info] OpenSSH's GEX fallback mechanism was triggered during testing. Very old SSH clients will still be able to create connections using a 2048-bit modulus, though modern clients will use 3072. This can only be disabled by recompiling the code (see https://github.com/openssh/openssh-portable/blob/V_9_4/dh.c#L477).
(kex) diffie-hellman-group16-sha512         -- [info] available since OpenSSH 7.3, Dropbear SSH 2016.73
(kex) diffie-hellman-group18-sha512         -- [info] available since OpenSSH 7.3
(kex) diffie-hellman-group14-sha256         -- [warn] 2048-bit modulus only provides 112-bits of symmetric strength
                                            `- [info] available since OpenSSH 7.3, Dropbear SSH 2016.73
(kex) diffie-hellman-group14-sha1           -- [fail] using broken SHA-1 hash algorithm
                                            `- [warn] 2048-bit modulus only provides 112-bits of symmetric strength
                                            `- [info] available since OpenSSH 3.9, Dropbear SSH 0.53

# host-key algorithms
(key) ssh-rsa (2048-bit)                    -- [fail] using broken SHA-1 hash algorithm
                                            `- [warn] 2048-bit modulus only provides 112-bits of symmetric strength
                                            `- [info] available since OpenSSH 2.5.0, Dropbear SSH 0.28
                                            `- [info] deprecated in OpenSSH 8.8: https://www.openssh.com/txt/release-8.8
(key) rsa-sha2-512 (2048-bit)               -- [warn] 2048-bit modulus only provides 112-bits of symmetric strength
                                            `- [info] available since OpenSSH 7.2
(key) rsa-sha2-256 (2048-bit)               -- [warn] 2048-bit modulus only provides 112-bits of symmetric strength
                                            `- [info] available since OpenSSH 7.2
(key) ecdsa-sha2-nistp256                   -- [fail] using elliptic curves that are suspected as being backdoored by the U.S. National Security Agency
                                            `- [warn] using weak random number generator could reveal the key
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(key) ssh-ed25519                           -- [info] available since OpenSSH 6.5

# encryption algorithms (ciphers)
(enc) chacha20-poly1305@openssh.com         -- [warn] vulnerable to the Terrapin attack (CVE-2023-48795), allowing message prefix truncation
                                            `- [info] available since OpenSSH 6.5
                                            `- [info] default cipher since OpenSSH 6.9
(enc) aes128-ctr                            -- [info] available since OpenSSH 3.7, Dropbear SSH 0.52
(enc) aes192-ctr                            -- [info] available since OpenSSH 3.7
(enc) aes256-ctr                            -- [info] available since OpenSSH 3.7, Dropbear SSH 0.52
(enc) aes128-gcm@openssh.com                -- [info] available since OpenSSH 6.2
(enc) aes256-gcm@openssh.com                -- [info] available since OpenSSH 6.2

# message authentication code algorithms
(mac) umac-64-etm@openssh.com               -- [warn] using small 64-bit tag size
                                            `- [info] available since OpenSSH 6.2
(mac) umac-128-etm@openssh.com              -- [info] available since OpenSSH 6.2
(mac) hmac-sha2-256-etm@openssh.com         -- [info] available since OpenSSH 6.2
(mac) hmac-sha2-512-etm@openssh.com         -- [info] available since OpenSSH 6.2
(mac) hmac-sha1-etm@openssh.com             -- [fail] using broken SHA-1 hash algorithm
                                            `- [info] available since OpenSSH 6.2
(mac) umac-64@openssh.com                   -- [warn] using encrypt-and-MAC mode
                                            `- [warn] using small 64-bit tag size
                                            `- [info] available since OpenSSH 4.7
(mac) umac-128@openssh.com                  -- [warn] using encrypt-and-MAC mode
                                            `- [info] available since OpenSSH 6.2
(mac) hmac-sha2-256                         -- [warn] using encrypt-and-MAC mode
                                            `- [info] available since OpenSSH 5.9, Dropbear SSH 2013.56
(mac) hmac-sha2-512                         -- [warn] using encrypt-and-MAC mode
                                            `- [info] available since OpenSSH 5.9, Dropbear SSH 2013.56
(mac) hmac-sha1                             -- [fail] using broken SHA-1 hash algorithm
                                            `- [warn] using encrypt-and-MAC mode
                                            `- [info] available since OpenSSH 2.1.0, Dropbear SSH 0.28

# fingerprints
(fin) ssh-ed25519: SHA256:IzSXDs9dqcYA25jc85qIroMg43bjBJ8DEbPHmAEr8Nc
(fin) ssh-rsa: SHA256:NBspkyMn7dsvL5N/svTAE9AIgURK6McPKX5xaTrK2OM

# algorithm recommendations (for OpenSSH 7.6)
(rec) -diffie-hellman-group14-sha1          -- kex algorithm to remove
(rec) -ecdh-sha2-nistp256                   -- kex algorithm to remove
(rec) -ecdh-sha2-nistp384                   -- kex algorithm to remove
(rec) -ecdh-sha2-nistp521                   -- kex algorithm to remove
(rec) -ecdsa-sha2-nistp256                  -- key algorithm to remove
(rec) -hmac-sha1                            -- mac algorithm to remove
(rec) -hmac-sha1-etm@openssh.com            -- mac algorithm to remove
(rec) -ssh-rsa                              -- key algorithm to remove
(rec) !rsa-sha2-256                         -- key algorithm to change (increase modulus size to 3072 bits or larger)
(rec) !rsa-sha2-512                         -- key algorithm to change (increase modulus size to 3072 bits or larger)
(rec) -chacha20-poly1305@openssh.com        -- enc algorithm to remove
(rec) -diffie-hellman-group14-sha256        -- kex algorithm to remove
(rec) -hmac-sha2-256                        -- mac algorithm to remove
(rec) -hmac-sha2-512                        -- mac algorithm to remove
(rec) -umac-128@openssh.com                 -- mac algorithm to remove
(rec) -umac-64-etm@openssh.com              -- mac algorithm to remove
(rec) -umac-64@openssh.com                  -- mac algorithm to remove

# additional info
(nfo) For hardening guides on common OSes, please see: <https://www.ssh-audit.com/hardening_guides.html>

```

### nmap

```
# Nmap 7.94SVN scan initiated Thu Mar  7 22:06:48 2024 as: nmap -vv --reason -Pn -T4 -sV -p 22 --script=banner,ssh2-enum-algos,ssh-hostkey,ssh-auth-methods -oN /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/tcp22/tcp_22_ssh_nmap.txt -oX /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/tcp22/xml/tcp_22_ssh_nmap.xml 10.129.95.191
Nmap scan report for 10.129.95.191
Host is up, received user-set (0.46s latency).
Scanned at 2024-03-07 22:07:01 MST for 83s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 61:e4:3f:d4:1e:e2:b2:f1:0d:3c:ed:36:28:36:67:c7 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDxxctowbmnTyFHK0XREQShvlp32DNZ7TS9fp1pTxwt4urebfFSitu4cF2dgTlCyVI6o+bxVLuWvhbKqUNpl/9BCv/1DFEDmbbygvwwcONVx5BtcpO/4ubylZXmzWkC6neyGaQjmzVJFMeRTTUsNkcMgpkTJXSpcuNZTknnQu/SSUC5ZUNPdzgNkHcobGhHNoaJC2StrcFwvcg2ftx6b+wEap6jWbLId8UfJk0OFCHZWZI/SubDzjx3030ZCacC1Sb61/p4Cz9MvLL5qPYcEm8A14uU9pTUfDvhin1KAEEDCSCS3bnvtlw1V7SyF/tqtzPNsmdqG2wKXUb6PLyllU/L
|   256 78:03:0e:b4:a1:af:e5:c2:f9:8d:29:05:3e:29:c9:f2 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKLh0LONi0YmlZbqc960WnEcjI1XJTP8Li2KiUt5pmkk
| ssh-auth-methods:
|   Supported authentication methods:
|     publickey
|_    password
| ssh2-enum-algos:
|   kex_algorithms: (10)
|       curve25519-sha256
|       curve25519-sha256@libssh.org
|       ecdh-sha2-nistp256
|       ecdh-sha2-nistp384
|       ecdh-sha2-nistp521
|       diffie-hellman-group-exchange-sha256
|       diffie-hellman-group16-sha512
|       diffie-hellman-group18-sha512
|       diffie-hellman-group14-sha256
|       diffie-hellman-group14-sha1
|   server_host_key_algorithms: (5)
|       ssh-rsa
|       rsa-sha2-512
|       rsa-sha2-256
|       ecdsa-sha2-nistp256
|       ssh-ed25519
|   encryption_algorithms: (6)
|       chacha20-poly1305@openssh.com
|       aes128-ctr
|       aes192-ctr
|       aes256-ctr
|       aes128-gcm@openssh.com
|       aes256-gcm@openssh.com
|   mac_algorithms: (10)
|       umac-64-etm@openssh.com
|       umac-128-etm@openssh.com
|       hmac-sha2-256-etm@openssh.com
|       hmac-sha2-512-etm@openssh.com
|       hmac-sha1-etm@openssh.com
|       umac-64@openssh.com
|       umac-128@openssh.com
|       hmac-sha2-256
|       hmac-sha2-512
|       hmac-sha1
|   compression_algorithms: (2)
|       none
|_      zlib@openssh.com
|_banner: SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Mar  7 22:08:24 2024 -- 1 IP address (1 host up) scanned in 96.07 seconds
```

## 80 - http

### whatweb

```
WhatWeb report for http://10.129.95.191:80
Status    : 200 OK
Title     : Welcome
IP        : 10.129.95.191
Country   : RESERVED, ZZ

Summary   : Email[admin@megacorp.com], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.29 (Ubuntu)], Script

Detected Plugins:
[ Email ]
	Extract email addresses. Find valid email address and
	syntactically invalid email addresses from mailto: link
	tags. We match syntactically invalid links containing
	mailto: to catch anti-spam email addresses, eg. bob at
	gmail.com. This uses the simplified email regular
	expression from
	http://www.regular-expressions.info/email.html for valid
	email address matching.

	String       : admin@megacorp.com

[ HTML5 ]
	HTML version 5, detected by the doctype declaration


[ HTTPServer ]
	HTTP server header string. This plugin also attempts to
	identify the operating system from the server header.

	OS           : Ubuntu Linux
	String       : Apache/2.4.29 (Ubuntu) (from server string)

[ Script ]
	This plugin detects instances of script HTML elements and
	returns the script language/type.


HTTP Headers:
	HTTP/1.1 200 OK
	Date: Fri, 08 Mar 2024 05:06:59 GMT
	Server: Apache/2.4.29 (Ubuntu)
	Vary: Accept-Encoding
	Content-Encoding: gzip
	Content-Length: 3189
	Connection: close
	Content-Type: text/html; charset=UTF-8


```

### nmap

```
# Nmap 7.94SVN scan initiated Thu Mar  7 22:06:48 2024 as: nmap -vv --reason -Pn -T4 -sV -p 80 "--script=banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" -oN /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/tcp80/tcp_80_http_nmap.txt -oX /home/kali/dev/Oopsie/enum/results/10.129.95.191/scans/tcp80/xml/tcp_80_http_nmap.xml 10.129.95.191
Nmap scan report for 10.129.95.191
Host is up, received user-set (0.15s latency).
Scanned at 2024-03-07 22:06:58 MST for 259s

Bug in http-security-headers: no string output.
PORT   STATE SERVICE REASON  VERSION
80/tcp open  http    syn-ack Apache httpd 2.4.29 ((Ubuntu))
|_http-jsonp-detection: Couldn't find any JSONP endpoints.
|_http-vuln-cve2014-3704: ERROR: Script execution failed (use -d to debug)
|_http-mobileversion-checker: No mobile version detected.
|_http-malware-host: Host appears to be clean
| http-methods:
|_  Supported Methods: POST
| http-useragent-tester:
|   Allowed User Agents:
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     libwww
|     libcurl-agent/1.0
|     Python-urllib/2.5
|     Snoopy
|     MFC_Tear_Sample
|     PHPCrawl
|     URI::Fetch
|   Change in Status Code:
|     PECL::HTTP: 200
|     HTTP::Lite: 200
|     PHP/: 200
|     Zend_Http_Client: 200
|     WWW-Mechanize/1.34: 200
|     Wget/1.13.4 (linux-gnu): 200
|     http client: 200
|     lwp-trivial: 200
|_    GT::WWW: 200
|_http-wordpress-users: [Error] Wordpress installation was not found. We couldn't find wp-login.php
|_http-traceroute: ERROR: Script execution failed (use -d to debug)
|_http-referer-checker: Couldn't find any cross-domain scripts.
|_http-chrono: Request times for /; avg: 10899.18ms; min: 1416.39ms; max: 26333.60ms
|_http-devframework: Couldn't determine the underlying framework or CMS. Try increasing 'httpspider.maxpagecount' value to spider more pages.
|_http-php-version: Logo query returned unknown hash 1566cccef228cfc2230fbd2f0270375e
| http-internal-ip-disclosure:
|_  Internal IP Leaked: 127.0.1.1
|_http-litespeed-sourcecode-download: Request with null byte did not work. This web server might not be vulnerable
|_http-fetch: Please enter the complete path of the directory to save data in.
|_http-date: Fri, 08 Mar 2024 05:08:54 GMT; -4s from local time.
|_http-wordpress-enum: Nothing found amongst the top 100 resources,use --script-args search-limit=<number|all> for deeper analysis)
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| http-sitemap-generator:
|   Directory structure:
|     /
|       Other: 1
|     /cdn-cgi/login/
|       js: 1
|     /css/
|       css: 4
|     /js/
|       js: 2
|     /themes/
|       css: 1
|   Longest directory structure:
|     Depth: 2
|     Dir: /cdn-cgi/login/
|   Total files found (by extension):
|_    Other: 1; css: 5; js: 3
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-grep:
|   (1) http://10.129.95.191:80/:
|     (1) email:
|       + admin@megacorp.com
|   (1) http://10.129.95.191:80/js/min.js:
|     (1) email:
|_      + support@codepen.io
| http-comments-displayer:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.129.95.191
|
|     Path: http://10.129.95.191:80/
|     Line number: 472
|     Comment:
|
|         //# sourceURL=pen.js
|
|     Path: http://10.129.95.191:80/
|     Line number: 424
|     Comment:
|
|         //IIFE
|
|     Path: http://10.129.95.191:80/css/font-awesome.min.css
|     Line number: 1
|     Comment:
|         /*!
|          *  Font Awesome 4.7.0 by @davegandy - http://fontawesome.io - @fontawesome
|          *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
|_         */
|_http-feed: Couldn't find any feeds.
| http-vhosts:
| 32 names had status 200
|_96 names had status ERROR
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
| http-headers:
|   Date: Fri, 08 Mar 2024 05:08:54 GMT
|   Server: Apache/2.4.29 (Ubuntu)
|   Vary: Accept-Encoding
|   Connection: close
|   Transfer-Encoding: chunked
|   Content-Type: text/html; charset=UTF-8
|
|_  (Request type: GET)
| http-errors:
| Spidering limited to: maxpagecount=40; withinhost=10.129.95.191
|   Found the following error pages:
|
|   Error Code: 404
|_  	http://10.129.95.191:80/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Mar  7 22:11:17 2024 -- 1 IP address (1 host up) scanned in 269.56 seconds
```

### nikto

```- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          10.129.95.191
+ Target Hostname:    10.129.95.191
+ Target Port:        80
+ Start Time:         2024-03-07 22:07:17 (GMT-7)
---------------------------------------------------------------------------
+ Server: No banner retrieved
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Apache/2.4.29 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+ /images: IP address found in the 'location' header. The IP is "127.0.1.1". See: https://portswigger.net/kb/issues/00600300_private-ip-addresses-disclosed
+ /images: The web server may reveal its internal or real IP in the Location header via a request to with HTTP/1.0. The value is "127.0.1.1". See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2000-0649
+ /: Web Server returns a valid response with junk HTTP methods which may cause false positives.
+ ERROR: Error limit (20) reached for host, giving up. Last error:
+ Scan terminated: 1 error(s) and 6 item(s) reported on remote host
+ End Time:           2024-03-07 22:18:07 (GMT-7) (650 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

### gobuster

```
http://10.129.95.191:80/.hta                 (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.asp             (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.txt             (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.aspx            (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.jsp             (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.php             (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.html       (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.txt        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.jsp        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.asp        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.php        (Status: 403) [Size: 278]
http://10.129.95.191:80/.hta.html            (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess            (Status: 403) [Size: 278]
http://10.129.95.191:80/.htaccess.aspx       (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd            (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.asp        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.jsp        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.html       (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.txt        (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.aspx       (Status: 403) [Size: 278]
http://10.129.95.191:80/.htpasswd.php        (Status: 403) [Size: 278]
http://10.129.95.191:80/css                  (Status: 403) [Size: 278]
http://10.129.95.191:80/fonts                (Status: 403) [Size: 278]
http://10.129.95.191:80/images               (Status: 403) [Size: 278]
http://10.129.95.191:80/index.php            (Status: 200) [Size: 10932]
http://10.129.95.191:80/js                   (Status: 403) [Size: 278]
http://10.129.95.191:80/server-status        (Status: 403) [Size: 278]
http://10.129.95.191:80/themes               (Status: 403) [Size: 278]
http://10.129.95.191:80/uploads              (Status: 403) [Size: 278]
```

### curl

```html
HTTP/1.1 200 OK
Date: Fri, 08 Mar 2024 05:06:50 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Transfer-Encoding: chunked
Content-Type: text/html; charset=UTF-8

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="apple-mobile-web-app-title" content="CodePen">
<title>Welcome</title>
<link rel="stylesheet" href="/css/reset.min.css">
<link rel="stylesheet" href="/themes/theme.css"/>
<link rel="stylesheet" href="/css/new.css"/>
<link rel='stylesheet' href='/css/1.css'>
<link rel='stylesheet' href='/css/font-awesome.min.css'>
<style>
html, body {
  font-family: 'Nunito Sans', sans-serif;
  color: #333;
  font-size: 16px;
}

p {
  line-height: 1.6;
  max-width: 50em;
}

button, input {
  font-family: Hind, sans-serif;
  font-size: 1rem;
  outline: none;
}

.wrap, .row, .tab-row {
  margin: 0 auto;
  max-width: 1000px;
}

.nav {
  position: fixed;
  z-index: 3;
  height: 60px;
  width: 100%;
  -webkit-transition: 300ms ease;
  transition: 300ms ease;
}

.brand {
  float: left;
  line-height: 60px;
  color: white;
  font-weight: 500;
  padding-left: 1rem;
}
.brand span {
  font-size: 1.9em;
  font-weight: 700;
}
.brand img {
  vertical-align: middle;
  height: calc(60px - 1rem);
  margin-right: .5rem;
}

.top-menu {
  display: none;
  position: relative;
  float: right;
  -webkit-transition: 200ms ease;
  transition: 200ms ease;
  font-weight: 300;
  height: 60px;
}
@media screen and (min-width: 640px) {
  .top-menu {
    display: block;
  }
}
.top-menu li {
  display: block;
  float: left;
  height: 60px;
}
.top-menu li a {
  display: block;
  height: 60px;
  line-height: 60px;
  text-decoration: none;
  color: #fff;
  padding: 0 1em;
}
.top-menu li a:hover {
  background: -webkit-gradient(linear, left top, left bottom, from(rgba(0, 0, 0, 0.1)), to(rgba(0, 0, 0, 0)));
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0));
}

.mobile-open {
  display: block;
}

.hamburger-btn {
  float: right;
  display: block;
  border: none;
  background: transparent;
  color: #fff;
  height: calc(60px - 1rem);
  width: calc(60px - 1rem);
  margin: 0.5rem 0.5rem 0 0;
  padding: 0;
  position: relative;
}
@media screen and (min-width: 640px) {
  .hamburger-btn {
    display: none;
  }
}
.hamburger-btn:hover {
  background: rgba(0, 0, 0, 0.1);
}
.hamburger-btn .hamburger-line {
  height: 2px;
  width: calc(60px - 2rem);
  background: #fff;
  display: block;
  position: absolute;
  left: calc(0.5rem - 1px);
  -webkit-transition: top 150ms ease-out 150ms, bottom 150ms ease-out 150ms, opacity 150ms ease 75ms, -webkit-transform 150ms ease-in;
  transition: top 150ms ease-out 150ms, bottom 150ms ease-out 150ms, opacity 150ms ease 75ms, -webkit-transform 150ms ease-in;
  transition: transform 150ms ease-in, top 150ms ease-out 150ms, bottom 150ms ease-out 150ms, opacity 150ms ease 75ms;
  transition: transform 150ms ease-in, top 150ms ease-out 150ms, bottom 150ms ease-out 150ms, opacity 150ms ease 75ms, -webkit-transform 150ms ease-in;
}
.hamburger-btn .hamburger-line:first-child {
  top: 0.75rem;
}
.hamburger-btn .hamburger-line:nth-child(2) {
  top: calc(50% - 1px);
}
.hamburger-btn .hamburger-line:last-child {
  bottom: 0.75rem;
}

.hamburger-cross .hamburger-line {
  -webkit-transition: top 150ms ease-in, bottom 150ms ease-in, opacity 150ms ease 75ms, -webkit-transform 150ms ease-out 150ms;
  transition: top 150ms ease-in, bottom 150ms ease-in, opacity 150ms ease 75ms, -webkit-transform 150ms ease-out 150ms;
  transition: transform 150ms ease-out 150ms, top 150ms ease-in, bottom 150ms ease-in, opacity 150ms ease 75ms;
  transition: transform 150ms ease-out 150ms, top 150ms ease-in, bottom 150ms ease-in, opacity 150ms ease 75ms, -webkit-transform 150ms ease-out 150ms;
}
.hamburger-cross .hamburger-line:first-child {
  -webkit-transform: rotate(45deg);
          transform: rotate(45deg);
  top: calc(50% - 1px);
}
.hamburger-cross .hamburger-line:nth-child(2) {
  top: calc(50% - 1px);
  opacity: 0;
}
.hamburger-cross .hamburger-line:last-child {
  -webkit-transform: rotate(-45deg);
          transform: rotate(-45deg);
  bottom: calc(50% - 1px);
}

.scroll {
  background: white;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.2);
}
.scroll .top-menu li a, .scroll .brand {
  color: black;
}
.scroll .hamburger-line {
  background: #000;
}

.hero {
  position: relative;
  z-index: 1;
  height: 100vh;
  max-height: 1080px;
  background-image: url(/images/1.jpg);
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  color: #fff;
  display: table;
  width: 100%;
  text-align: center;
  text-shadow: 1px 2px 4px rgba(0, 0, 0, 0.2);
}
.hero:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: -webkit-gradient(linear, left top, right bottom, from(#28e), to(#e14));
  background: linear-gradient(to bottom right, #28e, #e14);
  opacity: 0.9;
  z-index: -1;
}
.hero h1 {
  font-size: 4em;
  margin-bottom: 1rem;
}
.hero p {
  font-size: 2em;
  max-width: 80%;
  margin-left: auto;
  margin-right: auto;
  font-weight: 300;
}
.hero .content {
  display: table-cell;
  vertical-align: middle;
}

h1, h2, p {
  margin: 1em 0;
}

h2 {
  font-size: 2rem;
  line-height: 0.5;
}

a {
  color: #e14;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}

.row:after, .tab-row:after {
  content: "";
  display: table;
  clear: both;
}

.row, .tab-row {
  display: block;
}

.tab-row {
  display: table;
  height: 100%;
  vertical-align: middle;
}

.main {
  background: #f8f8f8;
}
.main .row, .main .tab-row {
  min-height: 200px;
}
.main .row:before, .main .row:after, .main .tab-row:before, .main .tab-row:after {
  content: '';
  display: table;
}
.main section {
  padding: 0 1rem;
  min-height: 400px;
  height: 62vh;
}

.feature {
  background-image: url(/images/2.jpg);
  background-attachment: fixed;
  background-size: cover;
  background-position: center;
  position: relative;
  z-index: 1;
  color: #fff;
  text-align: center;
}
.feature:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: -webkit-gradient(linear, left top, right bottom, from(#ee8822), to(#11eebb));
  background: linear-gradient(to bottom right, #ee8822, #11eebb);
  opacity: 0.9;
  z-index: -1;
}

.footer {
  background: #75889b;
  color: #ddd;
  padding: 2rem;
}
.footer li {
  line-height: 1.5;
}
.footer a {
  color: #aaa;
}
.footer hr {
  max-width: 1000px;
  border: 0;
  height: 1px;
  background: #a2aebb;
}

.col-4, .col-6, .col-12 {
  width: 100%;
}
@media screen and (min-width: 640px) {
  .col-4, .col-6, .col-12 {
    float: left;
  }
}
.tab-row > .col-4, .tab-row > .col-6, .tab-row > .col-12 {
  display: table-cell;
  vertical-align: middle;
  height: 100%;
  float: none;
}

@media screen and (min-width: 640px) {
  .col-4 {
    width: 33%;
  }
}

@media screen and (min-width: 640px) {
  .col-6 {
    width: 50%;
  }
}

button.cta {
  padding: 0.75em 1.5em;
  background: white;
  color: black;
  border: none;
  cursor: pointer;
  -webkit-transition: 200ms ease;
  transition: 200ms ease;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
  border-radius: 2px;
}
button.cta:hover {
  color: #e14;
  box-shadow: 0 0.25em 10px rgba(0, 0, 0, 0.2);
}
</style>
<script>
  window.console = window.console || function(t) {};
</script>
<script>
  if (document.location.search.match(/type=embed/gi)) {
    window.parent.postMessage("resize", "*");
  }
</script>
</head>
<body translate="no">
<nav class="nav" id="menu">
<div class="wrap">
<div class="brand">
<span>MegaCorp Automotive</span>
</div>
<button id="mobile-btn" class="hamburger-btn">
<span class="hamburger-line"></span>
<span class="hamburger-line"></span>
<span class="hamburger-line"></span>
</button>
<ul class="top-menu" id="top-menu">
<li><a href="#"><i class="fa fa-home" aria-hidden="true"></i></a></li>
<li><a href="#">Services</a></li>
<li><a href="#">About</a></li>
<li><a href="#">Contact</a></li>
</ul>
</div>
</nav>
<header class="hero">
<div class="content">
<p>Bringing EV Ecosystem | Robust Design</p>
<button class="cta">Learn More</button>
</div>
</header>
<main class="main">
<section>
<div class="tab-row">
<div class="col-12">
<h2>Introducing MegaCorp EVehicles</h2>
<p>The MegaCorp truck-based chassis provides solid structural rigidity while the electric propulsion system delivers a smooth and fuel-efficient drive. The flexibility of the platform allows the vehicle to optimize its wheel to body ratio, making the architecture dynamic while enlarging battery space. The elevated height and forward driving position of the Mega provides open visibility and engaging experience.</p>
</div>
</section>
<section class="feature">
<div class="tab-row">
<div class="col-12">
<h2>Features</h2>
<p>Open Visibility and Engaging Experience. Completely electric driven and runs without noise pollution or local emissions </p>
</div>
</div>
</div>
</section>
<section>
<div class="tab-row">
<div class="col-4">
<h2>Services</h2>
<p>We provide services to operate manufacturing data such as quotes, customer requests etc. Please login to get access to the service.</p>
</div>
</div>
</section>
</main>
<footer class="footer">
<div class="row">
<div class="col-6">
<p><i class="fa fa-phone" aria-hidden="true"></i> +44 (0)123 456 789</p>
<p><i class="fa fa-envelope" aria-hidden="true"></i> admin@megacorp.com</p>
</div>
<div class="col-6" style="text-align: right;">
</ul>
</div>
</div>
<hr>
<div class="row">
<div class="col-12">&copy; 2019 MegaCorp - <a href="#">Facebook</a> - <a href="#">Twitter</a></div>
</div>
</footer>
<script data-cfasync="false" src="/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js"></script><script src="/js/min.js"></script>
<script id="rendered-js">
//IIFE
(function () {
  "use strict";
  var menuId;
  function init() {
    menuId = document.getElementById("menu");
    document.addEventListener("scroll", scrollMenu, false);
  }
  function scrollMenu() {
    if (document.documentElement.scrollTop > 50) {
      menuId.classList.add("scroll");
      console.log('scroll');
    } else
    {
      menuId.classList.remove("scroll");
      console.log('no-scroll');
    }
  }
  document.addEventListener("DOMContentLoaded", init, false);
})();

(function () {
  "use strict";
  var mobBtn, topMenu;

  function init() {
    mobBtn = document.getElementById("mobile-btn");
    topMenu = document.getElementById("top-menu");
    mobBtn.addEventListener("click", mobileMenu, false);
  }

  function mobileMenu() {
    if (topMenu.classList.contains("mobile-open")) {
      topMenu.classList.remove("mobile-open");
    } else {
      topMenu.classList.add("mobile-open");
    }
    if (mobBtn.classList.contains("hamburger-cross")) {
      mobBtn.classList.remove("hamburger-cross");
    } else
    {
      mobBtn.classList.add("hamburger-cross");
    }
  }

  document.addEventListener("DOMContentLoaded", init);

})();
//# sourceURL=pen.js
    </script>
<script src="/cdn-cgi/login/script.js"></script>
<script src="/js/index.js"></script>
</body>
</html>
```

### screenshot

![htb_oopsie_scr.png](assets/imgs/htb_oopsie_scr.png)

# Foothold

### BurpSuite

using proxy, you can map out the website

![htb_oopsie_burp.png](assets/imgs/htb_oopsie_burp.png)

after some time, you can see that there is a login page, on this page you can login as a guest.

![htb_oopsie_burp01.png](assets/imgs/htb_oopsie_burp01.png)

Logging in a guest there is an upload page which you need admin rights to access, there is also a cookie that holds the user's role. now to find the id of admin

![htb_oopsie_burp_02.png](assets/imgs/htb_oopsie_burp_02.png)

On the account page there is a bit of GET info in the request, a account id, changing this to the admin you get the id of the admin

![htb_oopsie_burp03.png](assets/imgs/htb_oopsie_burp03.png)

### Reverse Shell

after utulizing this, you can access the upload page, and upload a php reverse shell

![htb_oopsie_pwned.png](assets/imgs/htb_oopsie_pwned.png)

:)

After some searching around inside of the /var dir you find the website files that include authentication logic for another user:

![htb_oopsie_revshell.png](assets/imgs/htb_oopsie_revshell.png)

This pwd doesnt work for the 'robert' user, but in the login folder for the page:

![htb_oopsie_revshell01.png](assets/imgs/htb_oopsie_revshell01.png)

# Privilege Escalation

Okay, so at this point I have access to a shell in the robert user, just need to get root.

I am now fully on the writeup, I do not know anything at all about privesc so I will be following the writeup from here on out.

there is a file owned by the "bugtracker" group which is interesting, it is a binary which is owned by root, and has the setuid bit set.

![htb_oopsie_privesc.png](assets/imgs/htb_oopsie_privesc.png)

So the way that this suid is exploited is by the fact that the 'cat' command isn't referenced explicitly by path, so if there is a cat command earlier than the intented command, then we have control

![ht_oopsie_rootpwn.png](assets/imgs/ht_oopsie_rootpwn.png)

:)

Oopsie has been pwned.
