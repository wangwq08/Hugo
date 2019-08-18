---
title: "Leetcode修炼1"
date: 2019-08-18T19:48:24+08:00
draft: false
categories: ["Leetcode"]
tags: ["Leetcode", "股票买卖"]
---

## Leetcode 121. 买卖股票的最佳时机

[GitHub](https://github.com/wangwq08/BlogCode/blob/master/src/main/java/com/wangwq/blogcode/Leetcode/Leetcode121.java)

给定一个数组，它的第i个元素是一支给定股票第i天的价格

如果你最多只允许完成一笔交易（买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

示例 1：

```
输入：[7, 1, 5, 3, 6, 1]
输出：5
```

解释： 在第2天（股票价格 = 1）的时候买入，在第5天（股票价格 = 6）的时候卖出，最大利润 = 6 - 1 = 5.

```
注意利润不能是 7 - 1 = 6， 因为卖出价格需要大于买入价格
```

示例 2：

```
输入：[7, 6, 4, 3, 1]
输出：0
```

解释：在这种情况下，没有交易完成，所以最大利润为0

## 题解

分析： 记录两个状态，一个是最大利润，另一个是遍历过的子序列的最小值，知道之前的最小值，可以算出当前天可能的最大利润是多少

```java
public class Solution {
    public static int maxProfit(int[] prices) {
        // 7 1 5 3 6 4
        int maxProfit = 0;
        int minNum = Integer.MAX_VALUE;
        for(int i = 0; i < prices.length; i++) {
            if(Integer.MAX_VALUE != minNum && prices[i] - minNum > maxProfit) {
                maxProfit = prices[i] - minNum;
            }

            if(prices[i] < minNum) {
                minNum = prices[i];
            }
        }
        return maxProfit;
    }

    public static void main(String[] args) {
        int[] prices = { 7, 1, 5, 3, 6, 4 };

        int maxProfit = maxProfit(prices);
        
        System.out.println(maxProfit);
    }
}
```

[参考资料](https://segmentfault.com/a/1190000018809812?utm_source=tag-newest)

> 我站在你左侧，却像隔着银河。
