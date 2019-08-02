---
title: "Informix查询日期第一天"
date: 2019-08-02T18:14:57+08:00
draft: false
categories: ["informix"]
tags: ["数据库", "日期"]
---

## 前言

当涉及到实现报表功能的时候，往往会需要不同的时间维度，例如当日、当月、当年的数据。

数据库中一般都有对应的函数去实现，不需要重新去实现。

## 获取当天日期

```sql
select today from tmp_01;
2019-08-02
```

## 获取当月的第一天

```sql
select today,mdy(month (today),01,year (today)) from tmp_01;
2019-08-02	2019-08-01
```

## 获取当年的第一天

```sql
select today,mdy(01,01,year(today)) from tmp_01;
2019-08-02	2019-01-01
```

**以上语句是针对informix数据，不同数据库的实现方式不同**

> 有些伤痕像场大火，把心烧焦难以复活。

