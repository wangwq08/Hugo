---
title: "Java基础知识(二)"
date: 2019-07-18T11:48:45+08:00
draft: false
categories: ["Java"]
tags: ["Java"]
---

## 1、构造器Constructor是否可以被override?

父类的私有属性和构造方法并不能被继承。所以Constructor也就不能被override(重写)。

但是可以被overload(重载)，所以你可以看到一个类中有多个构造函数的情况。

## 2、重载和重写的区别

* 重载： 发生在一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同，发生在编译时

* 重写: 发生在父子类中，方法名、参数列表必须相同，返回值范围小于等于父类。抛出的异常范围小于等于父类，访问修饰范围大于等于父类。
如果父类方法访问修饰符为private 则子类就不能重写该方法。

## 3、Java面向对象编程三大特性：封装 继承 多态

### **封装**

封装把一个对象的属性私有化，同时提供一些可以被外界访问的属性的方法，如果属性不想被外界访问，我们大可不必提供方法给外界访问。

但是如果一个类没有提供给外界访问的方法，那么这个类就没有什么意义了。

### **继承**

继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能。

但不能选择性地继承父类。通过使用继承可以非常方便地复用以前的代码。

**关于继承需要记住三点**

> 1、子类拥有父类对象所有的属性和方法（包括私有属性和私有方法）。但是父类中的私有属性和方法子类是无法访问，只是拥有

> 2、子类可以拥有自己属性和方法，即子类可以对父类进行扩展

> 3、子类可以用自己的方式实现父类的方法

### **多态**

所谓多态就是指程序中定义的引用变量所指向的具体类型和通过改引用变量发出的方法调用在编程时不确定，而是在程序运行期间才确定，
即一个引用变量到底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须由程序运行期间才能确定。

在Java中有两种形式可以实现多态：继承（多个子类对同一方法的重写）和接口（实现接口并覆盖接口中同一方法）

## String/StringBuffer/StringBuilder的区别是什么？String为什么是不可变的？

**可变性**

简单的来说，`String`类中使用`final`关键字修饰字符数组来保存字符串，`private final char value[]`,所以`String`对象是不可变的。而`StringBuilder`与`StringBuffer`都继承自`AbstractStringBuilder`类，在`AbstractStringBuilder`中也是使用字符数组保存字符串`char[]value`,但是没用用`final`关键字修饰，所以这两种对象都是可变的。

`StringBuilder`与`StringBuffer`的构造方法都是调用父类构造方法也就是`AbstractStringBuilder`实现的

`AbstractStringBuilder.java`

```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    char[] value;
    int count;
    AbstractStringBuilder() {

    }
    AbstractStringBuilder(int capacity) {
        value = new char[capacity]
    }
}
```
**线程安全性**

`String`中的对象是不可变的，也就可以理解为常量，线程安全。

`AbstractStringBuilder`是`StringBuilder`与`StringBuffer`的公共父类，定义了一些字符串的基本操作，如`expandCapacity`、`append`、`insert` 、`indexOf()`等公共方法。

`StringBuffer`对方法加了同步锁或者对调用的方法加了同步锁，所以线程是安全的

`StringBuilder`并没有对方法加同步锁，所以是非线程安全的。

**性能**

每次对`String`类型进行改变的时候，都会生成一个新的String对象，然后将指针指向新的String对象。

`StringBuffer`每次都会对`StringBuffer`对象本身进行操作，而不是生成新的对象并改变对象引用。

相同情况下使用`StringBuilder`相比使用`StringBuffer`仅能获得10%-15%左右的性能提升，但却要冒多线程不安全的风险。

**对于三者使用的总结**

1、操作少量的数据：适用String

2、单线程操作字符串缓冲区下操作大量数据：适用于StringBuilder

3、多线程操作字符串缓冲区下操作大量数据：适用于StringBuffer



---
[参考资料](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/Java%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86.md#8-%E5%AD%97%E7%AC%A6%E5%9E%8B%E5%B8%B8%E9%87%8F%E5%92%8C%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%B8%B8%E9%87%8F%E7%9A%84%E5%8C%BA%E5%88%AB)
