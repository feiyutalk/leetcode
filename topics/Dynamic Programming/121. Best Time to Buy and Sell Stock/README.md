# 121. Best Time to Buy and Sell Stock

我们需要在数组中，查找到两个数值的最大差值，而且需要满足第二个数值大于第一个数值。我们可以形式化为如下的数学表达式:

$max(prices[j] - prices[i]), for every i and j such that j > i$

## #1 暴力求解法 [TLE]

```java
public class Solution {
    public int maxProfit(int prices[]) {
        int maxprofit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            for (int j = i + 1; j < prices.length; j++) {
                int profit = prices[j] - prices[i];
                if (profit > maxprofit)
                    maxprofit = profit;
            }
        }
        return maxprofit;
    }
}
```

通过搜索所有的解空间， 然后记录下最大的差值，最后返回该差值。

### 复杂度分析

- **时间复杂度** $O(n^2)$, 循环执行了 $\frac {n(n-1)}{2}$次。
- **空间复杂度** $O(1)$，只用到一个变量来记录最大的profit

## #2 一次遍历[AC]

假设输入数组为: [7, 1, 5, 3, 6, 4]， 数组图像如下:

![](https://leetcode.com/media/original_images/121_profit_graph.png)

我们通过一个变量来记录目前为止最小的价格，每遍历到一个值，判断该值是否比当前最小值来得小，如果是的话， 就更新最小值；否则， 就更新收益。

```java
public class Solution {
    public int maxProfit(int prices[]) {
        int minprice = Integer.MAX_VALUE;
        int maxprofit = 0;
        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minprice)
                minprice = prices[i];
            else if (prices[i] - minprice > maxprofit)
                maxprofit = prices[i] - minprice;
        }
        return maxprofit;
    }
}
```

#### 复杂度分析:

- **时间复杂度** $O(n)$
- **空间复杂度** $O(1)$

