---
title: 在Windows10上用WSL/WSL2优雅开发
date: 2020-10-19 22:00:12
sidebar: true
sidebarDepth: 5
tags: 
- LINUX
categories:
- "杂谈"
isShowComments: true
---

[[toc]]

# 引言
由于电脑带不动虚拟机，而WSL可以使用vscode在win10和WSL直接联合开发（香）

## WSL安装

1.在设置->更新与安全->开发者选项中开启开发人员模式
![](https://dl-harmonyos.51cto.com/images/202010/d74a30341632605a81396183e556d339bb135e.PNG)
2.在控制面板开启 “适用于 Linux 的 windows 子系统”
![](https://dl-harmonyos.51cto.com/images/202010/0317d658993af1bd61f0861fe0ab062ded9115.PNG)
3. 通过Windows应用商店，可以安装自己喜欢的 Linux 发行版，例如Ubuntu 18.04 LTS及以上版本
初次进入Linux子系统需要设置Linux的用户名及密码，之后就不能在输入了，不过用户名密码还是需要记住的，特别是密码
安装完成可以换源加快wsl下载速度，以清华源为例。

一：备份原来的源
```
sudo cp /etc/apt/sources.list /etc/apt/sources_init.list

```


注意，我们操作Ubuntu一般都是要在管理员权限下进行操作的，尤其是要对系统文件进行更改。sudo就是告诉系统使用管理员权限运行后面的命令。敲入回车后输入我们之前设置的密码即可运行。

二：更换清华源
```
sudo vim /etc/apt/sources.list
```

将文件里的内容全部删除（可在vim的命令模式下，使用gg将光标移到文件首行，使用dG命令清空文件），敲入i进入编辑模式，将下面内容粘贴进文件

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

按ESC（或Ctrl + [）退出编辑模式进入命令模式，然后先按“:”，再输入wq，敲入回车，文件即写入成功。

三：更新系统
输入下列命令，等待更新完毕~
```
sudo apt-get update
sudo apt-get upgrade
```

 

(二)设置远程连接




一、系统本身自带的SSH有问题，需要remove一下，重新install一下
```
sudo apt-get remove openssh-server
```
二、然后重新安装
```
sudo apt-get install openssh-server
```
三.然后就是配置ssh的配置文件:

打开配置文件: 
```
sudo vim /etc/ssh/sshd_config

```


写入:
```
Port 2222   #设置ssh的端口号, 由于22在windows中有别的用处, 尽量不修改系统的端口号
PermitRootLogin yes   # 可以root远程登录
PasswordAuthentication yes     # 密码验证登录
AllowUsers sky # 远程登录时的用户名
```
重启服务:
```
 sudo service ssh restart
```
这个时候你自己电脑上的xhell等远程工具是可以连接的了, 但是想要在其他的计算机上访问, 就需要系统开放端口了.

这是后需要到防火墙设置开放2222端口

防火墙->高级设置->入站规则->新建规则

![](https://img-blog.csdn.net/20180928162108931?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xjdXdi/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


端口->下一步

选择tcp  特定本地端口 

![](https://img-blog.csdn.net/20180928162242346?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xjdXdi/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

允许连接, 默认都选上, 下一步填个名字
完成就可以远程或者本地进行wsl开发，原理及过程就相当于一台Linux，可能还有远程的时候可能需要在wsl重启一下ssh,有时使用xshell连接会connect failed,只要sudo service ssh restart一下就行，所以既然都打开了wsl，为啥不直接在wsl的Ubuntu上搞呢。。。。。

3.远程sftp服务
http://filezilla-project.org/download.php?type=client
- xftp

https://www.netsarang.com/zh/all-downloads/

::: tip

https://www.cnblogs.com/jetttang/p/8186315.html

https://dowww.spencerwoo.com


:::

## win操作

Shit+右键——Linux shell


https://www.cnblogs.com/jetttang/p/8186315.html


#停止LxssManager服务
net stop LxssManager  
 
#启动LxssManager服务
net start LxssManager  



### WSL1升级为WSL2
- 查看当前WSL版本号
```
wsl -l -v
```
- 检查运行WSL2的系统要求
WSL2对系统版本有一定要求，键盘选择Win + R，输入winver，点击回车，便可查看当前系统的详细版本。看一下是否满足要求，如果不满足要求，则需要对系统进行升级

×64：version>=1903,build>=18362
arm64:version>=2004,build>=19041

- 下载 Linux 内核更新包
根据系统进行选择：
x64：https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
arm64：https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.ms
- 运行上一步下载的更新包。

- 设置分发版版本
打开PowerShell，执行命令 ：
```
wsl --set-version 分发版名称 版本号
```
例如，将Ubuntu18.04 设置为WSL2的命令为 wsl --set-version Ubuntu-18.04 2
wsl2简介
https://docs.microsoft.com/zh-cn/windows/wsl/about

备注

WSL1更新到WSL2之后发现以前可以从Window文件系统中直接访问的Linux文件的方式不能用了后来在对比了[官网](https://docs.microsoft.com/zh-cn/windows/wsl/compare-versions)的描述之后，原来是WSL2 建议不要跨操作系统使用文件。但是我们仍然可以通过以下方式直接在Window系统的基础上访问到Linux的文件,比如我安装的是Ubuntu-18.04，那么可以通过以下方式
```
\\wsl$\Ubuntu-18.04\
```