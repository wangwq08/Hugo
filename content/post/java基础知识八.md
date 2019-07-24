---
title: "Java基础知识(八)"
date: 2019-07-24T14:27:57+08:00
draft: false
categories: ["Java"]
tags: ["Java", "关键字"]
---

## final static this super关键字总结

### final关键字

**final 关键字主要用在三个地方：变量、方法、类**

1. 对于一个final变量，如果是基本数据类型的变量，则其数值一旦初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象

2. 当用final修饰一个类时，表明这个类不能被继承。final类中的所有成员方法都会被隐式地指定为final方法

3. 使用final方法的原因有两个。第一个原因是把方法锁定，防止任何继承类修改它的含义；第二个原因是效率。早期的Java实现版本，会将final方法转为内嵌调用。
但是如果方法过于庞大，可能看不到内嵌调用带来的效能提升（现在的Java版本已经不再使用final方法进行优化）。类中所有的private方法都隐式地指定为final。

### static关键字

### this关键字

### super关键字

### 参考


## static关键字详解

### static关键字主要有以下四种使用场景

### 补充内容


---
[参考资料](https://gitee.com/SnailClimb/JavaGuide/blob/master/docs/java/Basis/final%E3%80%81static%E3%80%81this%E3%80%81super.md#)

