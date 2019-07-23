---
title: "Java基础知识(七)"
date: 2019-07-23T09:44:20+08:00
draft: false
categories: ["Java"]
tags: ["Java", "异常", "IO流"]
---

## Java中的异常处理

### Java异常类层次结构图

![image1](https://camo.githubusercontent.com/27aa104d93ba0738be0f3d2e7d5b096c1619d12d/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d322f457863657074696f6e2e706e67)

在Java中，所有的异常都有一个共同的祖先java.lang包中的**Throwable类**。

Throwable：有两个重要的子类：**Exception(异常)**和**Error(错误)**，二者都是Java异常处理的重要子类，各自都包含大量子类。

**Error(错误): 是程序无法处理的错误**，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时JVM(Java虚拟机)出现的问题。
例如，Java虚拟机运行错误(Virtual MachineError)，当JVM不再有继续执行操作所需的内存资源时，将出现OutOfMemoryError。这些异常发生时，Java虚拟机(JVM)一般
会选择线程终止。

这些错误表示故障发生于虚拟机自身、或者发生在虚拟机试图执行应用时，如Java虚拟机运行错误(Virtual MachineError)、类定义错误(NoClassDefFoundError)等，这些错误
是不可查的，因为它们在应用程序的控制和处理能力之外，而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说，即使发生了错误，本质上也不应该试图去处理它所引起的异常
状况。在Java中，错误通过Error的子类描述。

**Exception(异常)：是程序本身可以处理的异常。**Exception类有一个重要的子类RuntimeException。RuntimeException异常由Java虚拟机抛出。NullPointException(要访问的变量没有引用任何对象时，抛出该异常)、ArithmeticException(算术运算异常，一个整数除以0时，抛出该异常)和ArrayIndexOutOfBoundsException(下标越界异常)。

**异常和错误的区别：异常能被程序本身可以处理，错误是无法处理**

### Throwable类常用方法

* public string getMessage();返回异常发生时的详细信息

* public string toString();返回异常发生时的简要描述

* public string getLocallizedMessage();返回异常对象的本地化信息。使用Throwable的子类覆盖这个方法，可以声称本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与getMessage()返回的记过相同

* public void printStackTrace();在控制台上打印Throwable对象封装的异常信息。

### 异常处理总结

* **try块：**用于捕获异常。其后可以接零个或多个catch块，如果没有catch块，则必须跟一个finally块。

* **catch块：**用于处理try捕获到的异常

* **finally块：**无论是否捕获或处理异常，finally块里的语句都会被执行。当在try块或catch块中遇到return语句时，finally语句块将在方法返回之前被执行

### 以下4种特殊情况，finally块不会被执行：

1. 在finally语句块第一行发生了异常。因为在其他行，finally块还是会得到执行

2. 在前面的代码种用了System.exit(int)已退出了程序。exit是带参函数；若该语句在异常语句之后，finally会执行。

3. 程序所在的线程死亡

4. 关闭CPU

**注意：**当try语句和finally语句都有return语句时，在方法返回之前，finally语句的内容将被执行，并且finally语句的返回值将会覆盖原始的返回值。如下：

```java
public static int f(int value) {
    try {
        return value * value;
    } finally {
        if (value == 2) {
            return 0;
        }
    }
}

```

如果调用f(2)，返回值将是0，因为finally语句的返回值覆盖了try语句的返回值。


## Java中IO流分为几种？BIO,NIO,AIO有什么区别？

### Java种IO流分为几种？

* 按照流的流向分，可以分为输入流和输出流

* 按照操作单元划分，可以划分为字节流和字符流

* 按照流的角色划分为节点流和处理流

Java io流涉及40多个类，看上去乱，实际上有规则，并且彼此之间有紧密的联系。Java io流的40多个类都是从如下4个抽象类基类中派生出来

* InputStream/Reader: 所有的输入流的基类，前者是字节输入流，后者是字符输入流

* OutputStream/Writer: 所有的输出流的基类，前者是字节输出流，后者是字符输出流

按操作方式分类结构图

![image3](https://camo.githubusercontent.com/639ec442b39898de071c3e4fd098215fb48f11e9/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f494f2d2545362539332538442545342542442539432545362539362542392545352542432538462545352538382538362545372542312542422e706e67)

按操作对象分类结构图

![image4](https://camo.githubusercontent.com/4a44e49ab13eacac26cbb0e481db73d6d11181b7/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392d362f494f2d2545362539332538442545342542442539432545352541462542392545382542312541312545352538382538362545372542312542422e706e67)

### BIO,NIO,AIO有什么区别？

