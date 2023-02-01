---
title: "ssh密钥认证"
date: 2016-02-05
tags: ["ssh"]
draft: false
---

使用SSH客户端时，SSH提供两种方式的安全认证。

- 第一种方式是基于账号和密码。
- 第二种方式是基于密钥，需在本地创建一对密钥，并把公有密钥放在需要访问的服务器上。

这里要配置的ssh密钥认证就是基于第二种方式的安全认证。

## SSH密钥认证配置步骤如下：

### 1. 
在本地机器创建公钥，打开终端，执行如下命令，默认回车即可。

```
ssh-keygen -t rsa -C  'your email@domain.com'
```

其中-t 指定密钥类型，默认即 rsa ，可以省略
 其中-C 设置注释文字，比如你的邮箱

### 2. 
将公钥复制到远程ssh服务器，将前一步骤生成的公钥`~/id_rsa.pub`文件，复制到远程ssh服务器对应用户下的`~/.ssh/authorized_keys`文件。

当远程ssh服务器username用户目录下尚未有.ssh目录时使用此方法：

```
cat ~/.ssh/id_rsa.pub | ssh username@hostname "mkdir ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

拆解通用方法：

```
scp ~/.ssh/id_rsa.pub username@hostname:~/ #将公钥文件复制至远程ssh服务器

ssh username@hostname #使用用户名和密码方式登录至远程ssh服务器

mkdir .ssh  #若.ssh目录已存在，可省略此步

cat id_rsa.pub >> .ssh/authorized_keys  #将公钥文件id_rsa.pub文件内容追加到authorized_keys文件
```

### 3. 
快捷登录,完成以上步骤后，即可使用`ssh username@hostname`直接登录远程ssh服务器了