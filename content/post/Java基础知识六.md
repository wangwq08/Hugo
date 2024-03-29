---
title: "Java基础知识(六)"
date: 2019-07-22T17:12:07+08:00
draft: false
categories: ["Java"]
tags: ["Java","线程","进程"]
lastmod: 2019-07-23T17:12:07+08:00
---

## 简述线程、进程、程序的基本概念，以及他们之间的关系是什么？

**线程**与进程相似，但线程是一个比进程更小的执行单位。

一个进程在其执行的过程中可以产生多个线程。与进程不同的是同类的多个线程共享同一块内存空间和一组系统资源，所以系统在产生一个线程，
或是在各个线程之间切换工作时，负担要比进程小得多。因此，线程也被称为轻量级进程

**程序**是含有指令和数据得文件，被存储在磁盘或其他的数据存储设备中，也就说程序是静态的代码

**进程**是程序的一次执行过程，是系统运行程序的基本单位，因此进程是动态的。

系统运行一个程序即是一个进程从创建、运行到消亡的过程。简单来说，一个进程就是一个执行中的程序，它在计算机中一个指令接着一个指令地执行。
同时，每个进程还占有某些系统资源和CPU时间，内存空间，文件，输入输出设备的使用权等。换句话说，当程序在执行时，将会被操作系统载入内存中。

线程是进程划分成的更小的运行单位。线程和进程最大的不同在于基本上各进程是独立的，而各线程则不一定，因为同一进程中的线程极有可能相互影响。

从另一个角度来说，进程属于操作系统的范畴，主要是同一段时间内，可以同时执行一个以上的程序，而线程则是在同一程序内几乎同时执行一个以上的程序段。


## 线程有哪些基本状态

Java线程在运行的生命周期中的指定时刻只可能处于下面6种不同状体的其中一个状体（图源《Java并发编程艺术》4.1.4节）

![image1](https://camo.githubusercontent.com/bd21f0c6bf04fe410fa5397897cc47b9278ae5cb/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31392d312d32392f4a6176612545372542412542462545372541382538422545372539412538342545372538412542362545362538302538312e706e67)

线程在生命周期中并不是固定处于莫一个状态而是随着代码的执行在不同状态之间切换。Java线程状态变迁如下图所示（图源《Java并发编程艺术》4.14节）

![image2](https://camo.githubusercontent.com/88ca089de34d29350d6b72ee1b9e9c8f8f8691f2/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31392d312d32392f4a6176612532302545372542412542462545372541382538422545372538412542362545362538302538312545352538462539382545382542462538312e706e67)

由上图可以看出：

线程创建之后，它将处于**NEW(新建)**状态，调用`start()`方法后开始运行，线程处于**READY(可运行)**状态。可运行状态的线程获得了CPU时间片（timeslice）后就处于**RUNNING(运行)**状态。

> 操作系统隐藏Java虚拟机（JVM）中的RUNNABLE和RUNNING状态，它只能看到RUNNABLE状态（图源：[HowToDoInJava：Java Thread Life Cycle and Thread States](https://howtodoinjava.com/java/multi-threading/java-thread-life-cycle-and-thread-states/)）,所以Java系统一般将这两个状态统称为**RUNNABLE（运行中）**状态

![image3](https://camo.githubusercontent.com/916fefa029894b21921d3085f513b9a7f08ebad2/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d332f52554e4e41424c452d56532d52554e4e494e472e706e67)

当线程执行`wait()`方法之后，线程进入**WAITING(等待)**状态。进入等待状态的线程需要依靠其他线程的通知才能够返回到运行状态，而**TIME_WAITING(超时等待)**相当于在等待状态的基础上增加了超
时限制，比如通过`sleep(long millis)`方法或`wait(long millis)`方法可以将Java线程置于TIMED WAITING状态。当超时时间达到后Java线程将会返回到RUNNABLE状态。

当线程调用同步方法时，在没有获取到锁的情况下，线程将会进入到**BLOCKED(阻塞)**状态。线程在执行RUNNABLE的`run()`方法之后，将会进入到**TERMINATED(终止)**状态。

## 关于final关键字的一些总结

final关键字主要用在三个地方：变量、方法、类

1. 对于一个final变量，如果是基本数据类型的变量，则其数值在一旦初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。

2. 当用final修饰一个类时，表明这个类不能被继承。final类中的所有成员方法都会被隐式地指定为final方法。

3. 使用final方法的原因有两个。第一个原因时把方法锁定，以防任何继承类修改它的含义；第二个原因时效率。
在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升（现在的Java版本中已经不需要
再使用final方法进行这些优化了）。类中所有的private方法被隐式地指定为final。

## Java序列化中如果有些字段不想进行序列化，怎么办？

对于不想进行序列化的变量，使用transient关键字修饰。

transient关键字的作用是：阻止实例中那些用此关键字修饰的变量序列化；当对象被反序列化时，被transient修饰的变量值不会被持久和恢复。transient只能修饰变量，不能修饰类和方法。

## 获取用键盘输入常用的两种方法

方法1：通过Scanner

```java
Scanner input = new Scanner(System.in);
String s = input.nextLine();
input.close();
```

方法2：通过BufferedReader

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```


---
[参考资料](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/Java基础知识.md)
