---
title: "Node Sass报错的解决办法"
date: 2019-08-06T21:08:08+08:00
draft: false
categories: ["node"]
tags: ["node", "vue"]
---

## 前言

最近准备尝试一个前后端的开发项目，在GitHub上找了好久，最终找到了一个商城项目。克隆在本地运行前端项目

## 运行过程

```
cd 项目路径
npm install
npm run dev
```

简单的几条命令却报了一大堆错，之前也写过Vue项目，深知前端环境配置的坑，多数是版本、依赖下载问题。

## Node环境遇到的坑

### npm install报错

```
npm ERR! code EINTEGRITY
```

解决方式

```
npm cache clean --force //清楚缓存
npm install -g npm //升级版本
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

如果仍然报错，多次执行清除缓存。

### Vue启动环境报错

```
Error: `sass-loader` requires `node-sass` >=4 but node-sass is already
```

解决方式

```
npm i node-sass-D   //升级版本
```

前端的环境配置总是会遇到各种各样的坑，每次都需要花费大量的时间在配置上。

不过谁让前端好看呢，看脸的世界哈哈哈。看到别人写的界面，自己也总想去学习。

加油吧。

> Just you shoot for the stars. If it feels right


