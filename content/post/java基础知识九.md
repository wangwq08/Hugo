---
title: "Java基础知识(九)"
date: 2019-07-27T09:56:38+08:00
draft: false
categories: ["Java"]
tags: ["Java","Collections","Arrays"]
---

# Collections工具类和Arrays工具类常见方法

## Collections

Collections 工具类常用方法

1. 排序

2. 查找替换操作

3. 同步控制（不推荐，需要线程安全的集合类型时，考虑使用JUC包下的并发集合）

### **排序操作**

```java
void reverse(List list) //反转
void shuffle(List list) //随机排序
void sort(List list) //按自然排序的升序排序
void sort(List list, int i, int j) //交换两个索引位置的元素
void rotate(List list, int distance) //旋转，当distance为正数时，list后distance个元素整体移到前面，当distance为负数时，将list的前distance个元素整体移动到后面
```

**示例代码**

```java
ArrayList<Integer> arrayList = new ArrayList<Integer>();
    arrayList.add(-1);
    arrayList.add(3);
    arrayList.add(-5);
    arrayList.add(7);
	arrayList.add(4);
	arrayList.add(-9);
	arrayList.add(-7);
    System.out.println("原始数组：" + arrayList);
    Collections.reverse(arrayList);
    System.out.println("Collections.reverse(arrayList):" + arrayList);

	Collections.rotate(arrayList, 4);
	System.out.println("Collections.rotate(arrayList, 4):");
	System.out.println(arrayList);

	// void sort(List list),按自然排序的升序排序
	Collections.sort(arrayList);
	System.out.println("Collections.sort(arrayList):");
	System.out.println(arrayList);

	// void shuffle(List list),随机排序
	Collections.shuffle(arrayList);
	System.out.println("Collections.shuffle(arrayList):");
	System.out.println(arrayList);

	// void swap(List list, int i , int j),交换两个索引位置的元素
	Collections.swap(arrayList, 2, 5);
	System.out.println("Collections.swap(arrayList, 2, 5):");
	System.out.println(arrayList);

	// 定制排序的用法
	Collections.sort(arrayList, new Comparator<Integer>() {

	@Override
	public int compare(Integer o1, Integer o2) {
			return o2.compareTo(o1);
		}
	});
	System.out.println("定制排序后：");
	System.out.println(arrayList);
```

### **查找、替换操作**

```java
int binarySearch(List list, Object key); //对list进行二分查找，返回索引，注意list必须是有序的
int max(Collection coll) //根据元素的自然顺序，返回最大的元素，类比int min(Collection coll)
int max(Collection coll, Comparator c) //根据定制排序，返回最大元素，排序规则由Comparator类控制，类比 int min(Collection coll, Comparator c)
void fill(List list, Object obj) //用指定的元素代替指定list中的所有元素
int frequency(Collection c, Object o) //统计元素出现次数
int indexOfSublist(List list, List target) //统计target在list中第一次出现的索引，找不到则返回-1.类比 int lastIndexOfSublist(List source, list target)
boolean replaceAll(List list, Object oldVal, Object newVal) //新元素替换旧元素
```

**示例代码**

```java
		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(-1);
		arrayList.add(3);
		arrayList.add(3);
		arrayList.add(-5);
		arrayList.add(7);
		arrayList.add(4);
		arrayList.add(-9);
		arrayList.add(-7);
		ArrayList<Integer> arrayList2 = new ArrayList<Integer>();
		arrayList2.add(-3);
		arrayList2.add(-5);
		arrayList2.add(7);
		System.out.println("原始数组:");
		System.out.println(arrayList);

		System.out.println("Collections.max(arrayList):");
		System.out.println(Collections.max(arrayList));

		System.out.println("Collections.min(arrayList):");
		System.out.println(Collections.min(arrayList));

		System.out.println("Collections.replaceAll(arrayList, 3, -3):");
		Collections.replaceAll(arrayList, 3, -3);
		System.out.println(arrayList);

		System.out.println("Collections.frequency(arrayList, -3):");
		System.out.println(Collections.frequency(arrayList, -3));

		System.out.println("Collections.indexOfSubList(arrayList, arrayList2):");
		System.out.println(Collections.indexOfSubList(arrayList, arrayList2));

		System.out.println("Collections.binarySearch(arrayList, 7):");
		// 对List进行二分查找，返回索引，List必须是有序的
		Collections.sort(arrayList);
		System.out.println(Collections.binarySearch(arrayList, 7));
```

### **同步控制**

Collections提供了多个`synchronizedXxx()`方法，该方法可以将指定集合包装成线程同步的集合，从而解决多线程并发访问集合时的线程安全问题。

我们知道HashSet、TreeSet、ArrayList, LinkedList, HashMap, TreeMap都是线程不安全的。Collection提供了多个静态方法可以把它们包装成线程同步的集合。


## Arrays类的常见操作

1. 排序：`sort()`

2. 查找：`binarySearch()`

3. 比较：`equals()`

4. 填充：`fill()`

5. 转列表：`asList()`

6. 转字符串：`toString()`

7. 复制：`copyOf()`

### 

---
[参考资料](https://gitee.com/SnailClimb/JavaGuide/blob/master/docs/java/Basis/Arrays,CollectionsCommonMethods.md)

