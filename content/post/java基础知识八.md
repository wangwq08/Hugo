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

static关键字主要有以下四种使用场景：

1. **修饰成员变量和成员方法：**被static修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static声明的成员变量属于静态成员变量，静态变量存放在Java内存区域的方法区。调用格式：`类名.静态变量名`  `类名.静态方法名`

2. **静态代码块：**静态代码定义在类中方法外，静态代码块在非静态代码块之前执行(静态代码-->非静态代码-->构造方法)。该类不管创建多少对象，静态代码只执行一次。

3. **静态内部类（static修饰类的话只能修饰内部类）**静态内部类与非静态内部类之间存在一个最大的区别：非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有。没有这个引用就意味着：1.它的创建是不需要依赖外围类的创建。2.它不能使用任何外围类的非static成员变量和方法。

4. **静态导包（用来导入类中的静态资源，1.5之后的新特性）**格式为`import static`这两个关键字连用可以指定导入某个类中的指定静态资源，并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法

### this关键字

this关键字用于引用类的当前实例，例如：

```java
class Manager {
    Employees[] employees;

    void managerEmployees() {
        int totalEmp = this.employees.length;
        System.out.println("Total employees: " + totalEmmp);
        this.report();
    }

    void report() {}
}
```

在上面的示例中，this关键字用于两个地方：

* this.employees.length(): 访问类Manager的当前实例的变量

* this.report(): 调用类Manager的当前实例的方法

此关键字是可选的，这意味着如果上面的示例在不使用此关键字的情况下表现相同。但是使用此关键字可能会使代码更易读或易懂

### super关键字

### 参考


## static关键字详解

### static关键字主要有以下四种使用场景

### 补充内容


---
[参考资料](https://gitee.com/SnailClimb/JavaGuide/blob/master/docs/java/Basis/final%E3%80%81static%E3%80%81this%E3%80%81super.md#)

