---
title: "Java泛型详解及实现"
date: 2019-08-16T12:19:04+08:00
draft: false
categories: ["Java"]
tags: ["Java", "泛型"]
---

## 定义

在学习编程语言的变量时，都会了解一个变量的类型，函数的参数类型，那时候有个想法，参数的类型可以是参数吗？
那时候，仅仅只是听过泛型这个词，最近在使用的过程中，了解到了泛型的魅力。

> 首先我们知道，参数有形参和实参两种，常见的是定义方法时有形参，调用方法时传递实参。每个参数都有自己的类型。

>  泛型的本质是参数化类型，也就是在泛型使用过程中，操作的数据类型指定为一个参数，通过实参的数据类型，控制形参的数据类型。

## 举例说明

```java
List arrayList = new ArrayList();
arrayList.add("aaaa");
arrayList.add(100);

for (int i = 0; i < arrayList.size(); i++) {
    String item = (String) arrayList.get(i);  //强类型转换
    System.out.println("泛型测试", "item=" + item);
}
```

运行上面的程序会报异常：

```java
java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String
```

ArrayList中的元素类型可以为任意类型，分别添加了一个String 一个Integer,读取的时候使用String的方式，便出现了类型错误。

类似于这种类型转换的问题，可以通过泛型在编译阶段解决。

修改list的初始化代码，编译器可以在编译阶段发现类似问题

```java
List<String> arrayList = new ArrayList<String>();
...
//arrayList.add(100);在编译阶段，会报错。
```

**泛型类型只在编译阶段有效，泛型类型在逻辑上可以看成是多个不同的类型，实际都是相同的基本类型。**

## 实现最小值函数

设计一个泛型的获取数组最小值的函数，并且这个方法只能接受Number的子类，并且实现了Comparable接口。

```java
//注意： Number并没有实现Comparable
private static <T extends Number & Comparable<? super T>> T min(T[] values) {
    if(values == null || values.length == 0) 
        return null;
    T min = values[0];
    for(int i = 1; i < values.length; i++) {
        if(min.compareTo(values[i]) > 0)
            min = values[i];
    }
    return min;
}
```

测试：

```java
int minInteger = min(new Integer[] {1, 2, 3});  //result:1
double minDouble = min(new Double[] {1.2, 2.2, -1d});  //result: -1d
String typeError = min(new String[] {"1", "3"}); //报错
```


> 参考资料，[java 泛型详解](https://blog.csdn.net/s10461/article/details/53941091)、[泛型应用](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/Java%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E9%A2%98.md)


> 一个人去吃饭逛街，跟自己晚安又失眠。