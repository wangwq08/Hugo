---
title: "Git介绍与使用"
date: 2019-07-30T16:42:49+08:00
draft: false
categories: ["Git"]
tags: ["Git"]
---

## 关于Git是什么？

[Git](https://git-scm.com/)是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。Git是[Linus Torvalds](https://baike.baidu.com/item/%E6%9E%97%E7%BA%B3%E6%96%AF%C2%B7%E6%9C%AC%E7%BA%B3%E7%AC%AC%E5%85%8B%E7%89%B9%C2%B7%E6%89%98%E7%93%A6%E5%85%B9/1034429?fromtitle=Linus%20Torvalds&fromid=9336769)为了帮助管理Linux内核开发而开发的一个开放源码的版本控制软件。

## Git的基本命令

* 查看当前状态

```
git status
```

* 添加
```
git add .
```

* 提交

```
git commit -m "message"
```

* 推送

```
git push
```

* 拉取

```
git pull
```

* 初始化

```
git init
```

* 邮箱和用户名

       **仓库的用户名和邮箱设置，与每次提交的记录有关，如果用户名不一致，提交后会发现不是一个git用户，无法正确显示贡献值，而且GitHub的贡献值统计是以邮箱作为标识**

```
//查看本目录的仓库邮箱和用户
git config user,email
git config user.name

//修改本目录的仓库邮箱和用户
git config user.email "邮箱地址"
git config user.name "用户名"
```

     **当有多个git用户的时候，如公司内部的用户，和私人用户。这时候就需要区分清楚全局的用户设置和局部的用户设置**

```
//查看全局仓库的用户名和邮箱
git config --global user.email
git config --global user.name

//修改全局仓库的用户名和邮箱
git config --global uesr.email "邮箱地址"
git config --global user.name "用户名"
```

* 代理设置

```
//查看当前代理设置
git config --global http.proxy

//设置当前代理
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'

//删除代理
git config --global --unset https.proxy
git config --global --unset http.proxy

```

* 查看所有设置

```
git config --list
```

* 克隆远程仓库

```
git clone url
```

## Git与Github的关系

GitHub是一个面向开源及私有软件项目的托管平台，因为只支持git作为唯一的版本库格式进行托管。因此叫GitHub.

2018年6月4日，微软宣布，通过75亿美元的股票交易收购代码托管平台GitHub.

我一般使用GitHub与Git的流程是：

1. 在GitHub上建立一个目标仓库

2. 在本地，使用`git clone` 克隆到本地，进行代码编写

3. 编写完成后，`git push`到远程仓库，也就是GitHub中，进行保存。

4. 下一次修改前，首先进行`git pull`. 拉取最新版本。

这只是其中一种，比较简单的方式。还有其他实现方式，待实践后进行补充。Github中也有很多知识需要学习，如分支管理。GitHub也包含了很多优秀的开源项目可以学习。

> 我没有温柔，唯独有这点英勇。