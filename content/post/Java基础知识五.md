---
title: "Java基础知识(五)"
date: 2019-07-22T08:34:36+08:00
draft: false
categories: ["Java"]
tags: ["Java"]
---

## 为什么Java中只有值传递？

**按值调用（call by value）表示方法接收的是调用者提供的值，而按引用调用（call by reference）表示方法接收的是调用者提供的变量地址**

**一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值**

**Java程序设计语言总是采用按值调用。也就说，方法得到的是所有参数值的一个拷贝。即方法不能修改传递给它的任何参数变量的内容**

## 举例说明

**example1**

```java
public static void main(String[] args) {
    int num1 = 10;
    int num2 = 20;

    swap(num1,num2);

    System.out.println("num1 = " + num1);
    System.out.println("num2 = " + num2);
}

public static void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

    System.out.println("a = " + a);
    System.out.println("b = " + b);
}
```

**结果**

```
a = 20
b = 10
num1 = 10
num2 = 20
```

**解析**

![image1](https://camo.githubusercontent.com/ab46506b1a5ce09a516051c35f981e55255337f9/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d32372f32323139313334382e6a7067)

在swap方法中，a b的值进行交换，并不会影响到num1、num2。因为a b 的值，只是从num1 num2 的复制过来。

也就是说，a b 相当于num1 num2的副本，副本的内容无论怎么修改，都不会影响到原件本身。

**通过例子1，已经明白一个方法不能修改一个基本数据类型的参数，而对象引用作为参数就不一样**

**example2**

```java
public static void main(String[] args) {
    int[] arr = { 1, 2, 3, 4, 5 };
    System.out.println(arr[0]);
    change(arr);
    System.out.println(arr[0]); 
}

public static void change(int[] array) {
    //将数组的第一个元素变为0
    array[0] = 0;
}
```

**结果**
```
1
0
```

**解析**

![image2](https://camo.githubusercontent.com/b7bad9506150c29bb8d7debd3905bd7a71cd6611/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d32372f333832353230342e6a7067)

array被初始化arr的拷贝是一个对象的引用，也就是说array和arr指向的是同一个数组对象。因此，外部对引用对象的改变会反映到所对应的对象上。

**在example2中可以看到，实现一个改变对象参数状态的方法不是一件难事。理由是，方法得到是对象引用的拷贝，对象引用及其他的拷贝同时引用同一个对象**

很多程序设计语言（特别是C++和Pascal提供了两种参数传递的方式：值调用和引用调用）。有些人认为Java程序设计语言对对象采用的是引用调用，实际上，这种理解不对。

通过一个反例来阐述这个问题。

**example3**

```java
public class Test {
    public static void main(String[] args) {
        Student s1 = new Student("小张");
        Student s2 = new Student("小李");
        
        Test.swap(s1, s2);

        System.out.println("s1: " + s1.getName());
        System.out.println("s2: " + s2.getNmae());
    }

    public static void swap(Student x, Student y) {
        Student temp = x;
        x = y;
        y = temp;
        
        System.out.println("x: " + x.getName());
        System.out.println("y: " + y.getName());
    }
}
```

**结果**

```
x: 小李
y: 小张
s1: 小张
s2: 小李
```

**解析**

交换之前：

![image3](https://camo.githubusercontent.com/9d6dd0313695d309280675cd3251b47432a28814/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d32372f38383732393831382e6a7067)

交换之后:

![image4](https://camo.githubusercontent.com/6bea9b0ed65609d699207ab787f631f7ba0a9246/687474703a2f2f6d792d626c6f672d746f2d7573652e6f73732d636e2d6265696a696e672e616c6979756e63732e636f6d2f31382d392d32372f33343338343431342e6a7067)

通过上面两张图可以看出：**方法并没有改变存储在变量s1和s2中的对象引用。swap方法的参数x和y被初始化为两个对象引用的的拷贝，这个方法交换的是这两个拷贝**

**总结**

Java程序设计语言对对象采用的不是引用调用，实际上，对象引用是按值传递

总结一下Java中方法参数的使用情况：

* 一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）

* 一个方法可以改变一个对象参数的状态

* 一个方法不能让对象参数引用一个新的对象

## 参考

《Java核心技术卷Ⅰ》基础知识第十版第四章4.5小节

---
[参考资料](https://github.com/Snailclimb/JavaGuide/blob/master/docs/essential-content-for-interview/MostCommonJavaInterviewQuestions/%E7%AC%AC%E4%B8%80%E5%91%A8%EF%BC%882018-8-7%EF%BC%89.md)

