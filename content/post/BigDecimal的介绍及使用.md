---
title: "BigDecimal的介绍及使用"
date: 2019-08-12T12:23:54+08:00
draft: false
categories: ["Java"]
tags: ["java", "BigDecimal"]
---

## BigDecimal的用处

> 《阿里巴巴Java开发手册》提到：浮点数之间的等值判断，基本数据类型不能用 == 来比较，包装数据类型不能用equals来判断。

具体原理和浮点数的编码有关，这里使用实例说明

```java
float a = 1.0f - 0.9f;
float b = 0.9f - 0.8f;

System.out.println(a); //0.100000024
System.out.println(b); //0.099999964
System.out.println(a == b); //false
```

根据基本的数学知识，很显然输出并不是想要的结果（**精度丢失**）。如何解决这个问题呢？一种很常用的方法是：**使用BigDecimal来定义浮点数的值，再进行浮点数的运算操作**

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b); //0.1
BigDecimal y = b.subtract(c); //0.1
System.out.println(x.equals(y));  //true
```

## BigDecimal的大小比较

`a.compareTo(b)`: 返回-1表示小于，0表示等于，1表示大于

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");

System.out.println(a.compareTo(b));  //1
```

## BigDecimal保留几位小数

通过`setScale`方法设置保留几位小数及保留规则。保留规则有多种，IDEA可以自动提示。

```java
BigDecimal m = new BigDecimal("1.255433");
BigDecimal n = m.setScale(3, BigDecimal.ROUND_HALF_DOWN);
System.out.println(n); //1.255
```

## BigDecimal 的使用注意事项

**注意** 在使用BigDecimal时，为了防止精度丢失，推荐使用它的BigDecimal(String)构造方法来创建对象。

```java
BigDecimal recommend1 = new BigDecimal("0.1");
BigDecimal recommend2 = new BigDecimal.valueOf(0.1);
```

> 《阿里巴巴开发手册》中对这部分内容有所提及,如下图所示。

![image](https://camo.githubusercontent.com/b1c115758fbdca06d975ccb2ea9d948184d8478f/68747470733a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f323031392f372f426967446563696d616c2e706e67)

## 总结

BigDecimal主要用来操作（大）浮点数，BigInteger主要用来操作大整数（超过long类型）

BigDecimal的实现利用到了BigInteger，所不同的是BigDecimal加入了小数位的概念。