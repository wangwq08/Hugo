---
title: "Java疑难点(一)"
date: 2019-08-12T11:47:04+08:00
draft: false
categories: ["Java"]
tags: ["Java", "equals", "整型"]
---

## 正确使用`equals()`方法

Object的equals方法容易抛空指针异常，应该使用常量或确定有值的对象来调用equals.

举例：

```java
//不能使用一个值为null的引用类型变量来调用非静态方法，否则抛出异常
String str = null;
if (str.equals("wangwq08")) {
    ...
} else {
    ...
}
```

运行上面的程序会抛出空指针异常，第二行的判断语句修改后，就不会抛出异常了。

```java
"wangwq08".equals(str);  //false
```

推荐使用`java.util.Objects#equals`(JDK7引入的工具类)

```java
Object.equals(null, "wangwq08");  //false
```

查看`java.utils.Objects#equals`的源码就知道原因了。

```java
public static boolean equals(Object a, Object b) {
    //可以避免空指针异常。如果a==null的话，此时a.equals(b)不会得到执行，避免出现空指针异常
    return (a == b) || (a != null && a.equals(b));
}
```

**注意**

推荐阅读[java中equals方法造成空指针异常的原因及解决方案](https://blog.csdn.net/tick_tock97/article/details/72824894)

* 每种原始类型都有一个默认值。int默认值为0，boolean默认值为false。null是任何引用类型的默认值。不严格的说是所有Object类型的默认值

* 可以使用==或者!=操作来比较null值，但是不能使用其他算法或逻辑操作，在java中，null==null将返回true

* 不能使用一个值为null的引用类型变量来调用非静态方法，否则会抛出异常。

## 整型包装类值的比较

所有整型包装类对象值的比较必须使用equals方法

例子

```java
Integer x = 3;
Integer y = 3;
System.out.println(x == y); //true

Integer a = new Integer(3);
Integer b = new Integer(3);
System.out.println(a == b); //false
System.out.println(a.equals(b)); //true
```

当使用自动装箱方式创建一个Interger对象时，当数值在-128~ 127时，会将创建的Integer对象缓存起来，当下次再出现该数值时，直接从缓存中取出对应的Integer对象，上述代码中
x和y引用的是相同的Integer对象。

**注意：**如果IDE(idea/Eclipse)安装了阿里巴巴的p3c插件，插件监测到使用 == 的话进行报错提示。

> In all the good times I find myself longing for change



