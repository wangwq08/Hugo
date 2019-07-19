---
title: "Java基础知识(四)"
date: 2019-07-19T14:30:59+08:00
draft: false
categories: ["Java"]
tags: ["Java"]
---

## hashCode 与 equals（**重要**）

> 重写过hashcode和equals吗？为什么重写equals时必须重写hashCode方法

**hashCode() 介绍**

hashCode的作用是获取哈希码，也称为散列码；它实际上是返回一个int整数。

这个哈希码的作用是确定该对象在哈希表中的索引位置。hashCode()定义在JDK的Object.java中，这就意味着java中的任何类都包含有hashCode()函数

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码（可以快速找到对象）

## **为什么要有hashCode**

**我们先以`HashSet`如何检查重复**为例说明： 

> 当你把对象加入`HashSet`时，`HashSet`会先计算对象的`hashcode`值来判断对象加入的位置，同时也会与其他已经加入的对象的`hashcode`值作比较，
> 如果没有相符的`hashcode`，`HashSet`会假设对象没有重复出现。

> 但是如果发现有相同`hashcode`值的对象，这时会调用`equals()`方法来检查hashcode相等的对象
> 是否真的相同。如果两者相同，`HashSet`就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。
> (《Head first java》)。

> 这样就大大减少了equals的次数，相应就大大提高了执行速度。

因此，可以看出：hashCode()的作用就是获取哈希码，也称为散列码；它实际上返回一个int整数。这个哈希码的作用时确定该对象在哈希表中的索引位置。

**hashCode()在散列表中才有用，在其他情况下没用。**

在散列表中，hashCode()的作用是获取对象的散列码，进而确定该对象在散列表中的位置。

**`hashCode()`与`equals()`的相关规定**

1. 如果两个对象相等，则hashcode一定也是相同的

2. 如果两个对象相等，对两个对象分别调用equals()方法都返回true

3. 两个对象有相同的hashcode值，它们也不一定是相等的

4. 因此，equals方法被覆盖过，则hashCode方法也必须被覆盖

5. hashCode()的默认行为是对堆上的对象产生独特值。如果没有重写hashCode().则该class的两个对象无论如何都不会相等（即使两个对象指向相同的数据）

> **推荐阅读**  [Java hashCode() 和 equals()的若干问题解答](https://www.cnblogs.com/skywang12345/p/3324958.html)


---
[参考资料](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/Java基础知识.md)