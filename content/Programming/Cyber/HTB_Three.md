---
id: HTB_Three
aliases: []
tags: []
---

## Entry Point

```
10.129.227.248
```

## nmap

```
Stats: 0:02:09 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 97.18% done; ETC: 21:20 (0:00:04 remaining)
Nmap scan report for 10.129.29.187
Host is up (0.14s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 178.63 seconds
```

## ssh-audit

```
# general
(gen) banner: SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.7
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
(fin) ssh-ed25519: SHA256:SOh8txgAJ4TzqEuP3O3tPMks/4cr2ICEgIoFydCyUl0
(fin) ssh-rsa: SHA256:vo4vqpVJmd/ls4HRYuNXqLTWaZKcqfeZXUGdn7F5awQ

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

need to learn how to digest this

## gobuster

```
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:             http://thetoppers.htb
[+] Method:          GET
[+] Threads:         10
[+] Wordlist:        subdomains-top1million-5000.txt
[+] User Agent:      gobuster/3.6
[+] Timeout:         10s
[+] Append Domain:   true
===============================================================
Starting gobuster in VHOST enumeration mode
        -- This is the default implementation.
===============================================================
Found: s3.thetoppers.htb Status: 404 [Size: 21]
Found: gc._msdcs.thetoppers.htb Status: 400 [Size: 306]
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
===============================================================
```

subdomain s3.thetoppers is what we need, some aws service

## AWS S3

![aws_htbThreeaws.png](assets/imgs/aws_htbThreeaws.png)

At this point, I am just going along with the writeup because I feel no need
to bang my head over aws rn.

![aws_htbThreeaws01.png](assets/imgs/aws_htbThreeaws01.png)

two files, .htaccess and index.php, also an images/ dir

The real vuln lies in the fact that you can also cp files into the web root, and then visit them in a browser to then RCE

![aws_htbThreeawspwn.png](assets/imgs/aws_htbThreeawspwn.png)

and we are in. :)

so now we write a payload for a revshell, listener, and serve it to the server.

![htb_awsThreeshell.png](assets/imgs/htb_awsThreeshell.png)

pwned.
