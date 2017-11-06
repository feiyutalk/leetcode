# 365. Water and Jug Problem

# Description

You are given two jugs with capacities *x* and *y* litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly *z* litres using these two jugs.

If *z* liters of water is measurable, you must have *z* liters of water contained within **one or both buckets** by the end.

Operations allowed:

- Fill any of the jugs completely with water.
- Empty any of the jugs.
- Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

**Example 1:** (From the famous [*"Die Hard"* example](https://www.youtube.com/watch?v=BVtQNK_ZUJg))

```
Input: x = 3, y = 5, z = 4
Output: True
```

**Example 2:**

```
Input: x = 2, y = 6, z = 5
Output: False
```

# Solution

这是一道数论的题目，一直想着每天学点数学，一是对于数学的兴趣，二是因为数学实在是有用，但是苦于每天都有做不完的事，希望后面能挤出一点时间每天学点数学吧，加油。关于怎么求解，直接看Discuss吧。

```java
class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
        //boundary condition
        if(x+y<z) return false;
        if(x==z || y==z || x+y == z) return true;
        //normal condition
        return z%gcd(x, y) == 0;
    }
    
    public int gcd(int a, int b){
        while(b != 0){
            int temp = b;
            b = a%b;
            a = temp;
        }
        return a;
    }
}
```

