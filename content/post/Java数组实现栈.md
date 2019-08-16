---
title: "Java数组实现栈"
date: 2019-08-15T11:41:29+08:00
draft: false
categories: ["数据结构"]
tags: ["数据结构", "数组", "栈"]
---

[GitHub](https://github.com/wangwq08/BlogCode/tree/master/src/main/java/com/wangwq/blogcode)

## 栈的定义及特性

* 栈的定义： 栈(stack)是一个数据集合，可以理解为只能在一端进行插入或删除操作的列表

* 栈的特点： 后进先出（last-in, first-out）简称LIFO表。类似一摞书

![image](https://img2018.cnblogs.com/blog/1311506/201809/1311506-20180921142000463-953388146.png)

## 栈的概念和基本操作

### 栈的概念：

* 栈顶： 允许插入和删除的这一端称为栈顶

* 栈底： 另外固定的一端称为栈底

* 空栈： 不含任何元素的栈称为空栈

### 栈的基本操作：

* 进栈（压栈）：push

* 出栈： pop

* 取栈顶：gettop(查看栈顶元素，但不取走)

![image](https://img2018.cnblogs.com/blog/1311506/201809/1311506-20180921142200385-1413827597.png)

## 实现

实现一个栈，要求这个栈具有push()、pop()(返回栈顶元素并出栈)、peek()(返回栈顶元素不出栈)、isEmpty()、size()这些基本方法

注意：每次入栈之前需要先判断栈的容量是否够用，如果不够就用Arrays.copyOf()进行扩容：

```java
public class MyStack {
    private int[] storage; //存放栈中元素的数组
    private int capacity; //栈的容量
    private int count; //栈中元素数量
    private static final int GROW_FACTOR = 2;

    //TODO: 不带初始容量的构造方法，默认容量为8
    public MyStack() {
        this.capacity = 8;
        this.storage = new int[8];
        this.count = 0;
    }

    //TODO:带初始容量的构造方法
    public MyStack(int initialCapacity) {
        if (initialCapacity < 1) 
            throw new IllegalArgumentException("Capacity too small.");
        
        this.capacity = initialCapacity;
        this.storage = new int[initialCapacity];
        this.count = 0;
    }

    //TODO: 入栈
    public void push(int value) {
        if (count == capacity) {
            ensureCapacity();
        }
        storage[count++] = value;
    }

    //TODO: 确保容量大小
    public void ensureCapacity() {
        int newCapacity = capacity * GROW_FACTOR;
        storage = Arrays.copeOf(storage, newCapacity);
        capacity = newCapacity;
    }

    //TODO:返回栈顶元素并出栈
    private int pop() {
        count--;
        if (count == -1)
            throw new IllegalArgumentException("Stack is empty.");
        
        return storage[count];
    }

    //TODO:返回栈顶元素不出栈
    private int peek() {
        if (count == 0) {
            throw new IllegalArgumentException("Stack is empty");
        } else {
            return storage[count - 1];
        }
    }

    //TODO:判断栈是否为空
    private boolean isEmpty() {
        return count == 0;
    }

    //TODO:返回栈中元素的个数
    private int size() {
        return count;
    }
}
```

## 验证

```java
    public static void main(String[] args) {
        MyStack myStack = new MyStack();
        for(int i = 1; i< 9; i++) {
            myStack.push(i);
        }

        System.out.println(myStack.peek()); //8
        System.out.println(myStack.size()); //8

        for(int i = 0; i < 8; i++) {
            System.out.println(myStack.pop());
        }
        System.out.println(myStack.isEmpty()); //true
        myStack.pop(); //Exception java.lang.IllegalArgumentException: Stack is empty
    }
```

[参考资料](https://github.com/Snailclimb/JavaGuide/blob/master/docs/java/Java%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E9%A2%98.md)

> An empty street, A empty house, A hole inside my heart.