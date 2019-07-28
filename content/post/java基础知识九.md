---
title: "Java基础知识(九)"
date: 2019-07-27T09:56:38+08:00
draft: false
categories: ["Java"]
tags: ["Java","Collections","Arrays"]
lastmod: 2019-07-28T09:56:38+08:00
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

### 排序`sort()`

```java
        int a[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
        Arraysd.sort(a);
        System.out.println("Arrays.sort(a):");
        for (int i : a) {
            System.out.print(i);
        }
        System.out.println();

		// sort(int[] a,int fromIndex,int toIndex)按升序排列数组的指定范围
		int b[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		Arrays.sort(b, 2, 6);
		System.out.println("Arrays.sort(b, 2, 6):");
		for (int i : b) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int c[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// parallelSort(int[] a) 按照数字顺序排列指定的数组(并行的)。同sort方法一样也有按范围的排序
		Arrays.parallelSort(c);
		System.out.println("Arrays.parallelSort(c)：");
		for (int i : c) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// parallelSort给字符数组排序，sort也可以
		char d[] = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		Arrays.parallelSort(d);
		System.out.println("Arrays.parallelSort(d)：");
		for (char d2 : d) {
			System.out.print(d2);
		}
		// 换行
		System.out.println();
```

在做算法面试题的时候，我们还可能会经常遇到对字符串排序的情况`Array.sort()`对每个字符串的特定位置进行比较。然后按照升序排序

```java
String[] strs = { "abcdehg", "abcdefg", "abcdeag" };
Array.sort(strs);
System.out.println(Arrays.toString(strs)); //{ abcdeag, abcdefg, ancdehg }
```

### 查找：`binarySearch()`

```java
		// *************查找 binarySearch()****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		// 排序后再进行二分查找，否则找不到
		Arrays.sort(e);
		System.out.println("Arrays.sort(e)" + Arrays.toString(e));
		System.out.println("Arrays.binarySearch(e, 'c')：");
		int s = Arrays.binarySearch(e, 'c');
		System.out.println("字符c在数组的位置：" + s);

```

### 比较：`equals()`

```java
		// *************比较 equals****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		char[] f = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		/*
		* 元素数量相同，并且相同位置的元素相同。 另外，如果两个数组引用都是null，则它们被认为是相等的 。
		*/
		// 输出true
		System.out.println("Arrays.equals(e, f):" + Arrays.equals(e, f));
```

### 填充：`fill()`

```java
		// *************填充fill(批量初始化)****************
		int[] g = { 1, 2, 3, 3, 3, 3, 6, 6, 6 };
		// 数组中所有元素重新分配值
		Arrays.fill(g, 3);
		System.out.println("Arrays.fill(g, 3)：");
		// 输出结果：333333333
		for (int i : g) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		// 数组中指定范围元素重新分配值
		Arrays.fill(h, 0, 2, 9);
		System.out.println("Arrays.fill(h, 0, 2, 9);：");
		// 输出结果：993333666
		for (int i : h) {
			System.out.print(i);
		}
```

### 转列表：`asList()`

```java
		// *************转列表 asList()****************
		/*
		 * 返回由指定数组支持的固定大小的列表。
		 * （将返回的列表更改为“写入数组”。）该方法作为基于数组和基于集合的API之间的桥梁，与Collection.toArray()相结合 。
		 * 返回的列表是可序列化的，并实现RandomAccess 。
		 * 此方法还提供了一种方便的方式来创建一个初始化为包含几个元素的固定大小的列表如下：
		 */
		List<String> stooges = Arrays.asList("Larry", "Moe", "Curly");
		System.out.println(stooges);
```

### 转字符串：`toString()`

```java
		// *************转字符串 toString()****************
		/*
		* 返回指定数组的内容的字符串表示形式。
		*/
		char[] k = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		System.out.println(Arrays.toString(k));// [a, f, b, c, e, A, C, B]
```

### 复制：`copyOf()`

```java
		// *************复制 copy****************
		// copyOf 方法实现数组复制,h为数组，6为复制的长度
		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		int i[] = Arrays.copyOf(h, 6);
		System.out.println("Arrays.copyOf(h, 6);：");
		// 输出结果：123333
		for (int j : i) {
			System.out.print(j);
		}
		// 换行
		System.out.println();
		// copyOfRange将指定数组的指定范围复制到新数组中
		int j[] = Arrays.copyOfRange(h, 6, 11);
		System.out.println("Arrays.copyOfRange(h, 6, 11)：");
		// 输出结果66600(h数组只有9个元素这里是从索引6到索引11复制所以不足的就为0)
		for (int j2 : j) {
			System.out.print(j2);
		}
		// 换行
		System.out.println();
```

---
[参考资料](https://gitee.com/SnailClimb/JavaGuide/blob/master/docs/java/Basis/Arrays,CollectionsCommonMethods.md)

> 梦与想丢低很远，但对返工厌倦。

