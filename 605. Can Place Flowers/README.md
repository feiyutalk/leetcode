# 605. Can Place Flowers

# Description

Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number **n**, return if **n** new flowers can be planted in it without violating the no-adjacent-flowers rule.

**Example 1:**

```
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True
```

**Example 2:**

```
Input: flowerbed = [1,0,0,0,1], n = 2
Output: False
```

# Solution

这道题目，我直接采用的是贪心的算法，从左往右遍历，如果有位置就直接插入了，这样是合理的。虽然一时不知道怎么证明，但是按照这个思路写代码是通过的。

只是考虑两个端点的时候，有点繁琐，代码反而写得挺多的。

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        //boundary condition
        if(n == 0)
            return true;
        if(flowerbed == null || flowerbed.length == 0)
            return false;
        if(flowerbed.length == 1)
            return flowerbed[0] == 0;
        // first plot
        if(flowerbed[0] == 0 && flowerbed[1] == 0){
            n--;
            flowerbed[0] = 1;
        }
        if(n == 0)
            return true;
        //normal condition
        for(int i=1; i<flowerbed.length-1; i++){
            if(flowerbed[i] == 0){
                if(flowerbed[i-1] == 0 && flowerbed[i+1] == 0){
                    flowerbed[i] = 1;
                    n--;
                }
                if(n == 0)
                    return true;
            }
        }
        //last plot
        if(flowerbed[flowerbed.length-2] == 0 && flowerbed[flowerbed.length-1] == 0){
            n--;
            flowerbed[0] = 1;
        }
        if(n == 0)
            return true;
        return false;
    }
}
```

