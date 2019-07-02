---
title: "AIX系统简介"
date: 2018-05-08T18:35:08+08:00
draft: false
categories: ["AIX"]
tags: ["AIX"]
---
## 简介
AIX是Advanced Interactive executive的缩写, 中文名为高级交互执行。
1986年1月推出，是IBM发布的UNIX操作系统。最初，AIX运行在IBMRT/PC(AIX/RT)上。自从1989年以来，AIX成为RS/6000系列工作站和服务器(AIX/6000)的操作系统。
2001年推出的AIX 5L 是AIX发展史上的重要版本，基于标准的开放操作系统，符合The Open Group 的Single UNIX Specification Version 3 的要求。
2017年11月，伴随着新一代Power CPU -Power 6 的诞生，IBM推出了最新的AIX 6 操作系统,在很多方面都进行了革命性的改变和创新,如虚拟化技术、安全架构、开发环境以及持续可用性等方面。

## 入门使用
大多数用户，对于Aix的访问是通过telnet的方法登录到RS6000上,以不同的身份。把本地的机器作为RS6000的一个终端,来完成对RS6000的操作。体现了UNIX系统的特点,UNIX本身就是一个多任务、多用户的并发系统。

通过telnet ip 登录，输入账号及密码，会显示以下消息
```
AIX Version 5
Copyright IBM Corporation, 1982, 2008
Login: test
test's password:

****************************************************************************
*
* Welcome to AIX Version 5.3!
*
*
* Please see the README file in /usr/lpp/bos for information pertinent to 
* this release of the AIX Operating System.
*
*
****************************************************************************
Last unsuccessful login: Fri Dec 28 14:59:34 BEIST 2001 on /dev/pts/0 from 192.3 
Last login: Sat Dec 29 10:13:50 BEIST 2001 on /dev/pts/6 from 192.168.0.133 
[YOU HAVE NEW MAIL] 
```
正常显示以上消息，则登录成功,会出现命令提示符。与UNIX系统相似。操作命令也与UNIX基本相同
非root用户提示符一般为$ root用户提示符一般为#
不同命令的提示符与shell有关。B shell 和 K shell的提示符使用$
Aix 中为 K shell

## 参考资料
可以通过[这里](https://www.ibm.com/developerworks/cn/aix/newto/)详细了解AIX的使用，以及对于UNIX新手也可以很好的入门命令行的使用和Vi编辑器的使用。


