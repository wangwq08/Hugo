---
title: "Hugo博客搭建基本知识"
date: 2019-06-26T19:26:00+08:00
draft: false
categories: ["博客搭建"]
description: ["从零开始搭建属于自己的静态网站"]
tags: ["Hugo"]
---

## 关于Hugo

Hugo是由Go语言实现的静态网站生成器。简单、易用、高校、容易扩张、快速部署。
[中文文档](https://www.gohugo.org/)

## 其他工具

* Hexo也是静态网站生成器，基本思想同Hugo部署过程类似，不过Hexo需要安装node环境及对应的插件，较为麻烦
* Typecho是一种轻量级博客，使用PHP编写，动态网站，包括前后端，需要部署数据库、服务器
* Wordpress是使用PHP语言开发的博客平台，逐步演化成内容管理系统，功能强大，扩展性强，静态化差

## Why Hugo

* Hugo相较于其他工具，部署方便，只需要一个安装包运行即可，对环境兼容性强
* Hugo的主题丰富，且使用方便，只需替换配置文件即可
* Hugo可以支持Mac\Linux\Windows多平台
* 搭建博客的初衷是记录和思考，简洁是一个要求，避免过多的功能分散内容的注意力

## Hugo搭建基本过程
>以下过程为windows系统环境，执行

* 首先下载操作系统对应的Hugo包。[Hugo Releases](https://github.com/gohugoio/hugo/releases)
* 检查是否安装成功。生成站点
```
hexo new site sitename
```
* 下载对应主题[theme](https://themes.gohugo.io/)
```
cd /themes
git clone https://github.com/onweru/hugo-swift-theme.git
```
* 替换主题配置文件，将目标主题文件的config.toml，替换掉根目录的config.toml
* 创建文章,创建后的文章在content文件下
```
hugo new post/hello.md
```
* 运行Hugo,浏览器里打开： http://localhost:1313
```
hugo server
```
>注意，以上命令并不会生成草稿页面，如果未生成任何文章，请去掉文章头部的 draft=true 再重新生成。

## Todo
* 完成linux下环境的搭建
* 尝试部署到Github和VPS
* 思考不同终端的更新博客方式
* 尝试博客及配置的备份方式和迁移



