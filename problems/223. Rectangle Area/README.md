# 223. Rectangle Area

## #1 分类整合[AC]

### 思路

要求两个矩形在2D平面上的面积$S$，我们对$S$进行分解拆成，$S = S_{r_1} + S_{r_2} -S_{inter}$，其中$S_{r_1}$表示第一个矩形的面积；$S_{r_2}$表示第二个矩形的面积；$S_{inter}$表示两个矩形相交的面积。

### 算法

```java
class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        long bl1 = Math.max(A, E);
        long bl2 = Math.max(B, F);
        long tr1 = Math.min(C, G);
        long tr2 = Math.min(D, H);
        long inter =  Math.max(tr1 - bl1, 0) * Math.max(tr2 - bl2, 0);
        long rec1 = (C - A) * (D - B);
        long rec2 = (G - E) * (H - F);
        return (int)(rec1 + rec2 - inter);
    }
}
```

### 复杂度分析

- 时间复杂度：$O(1)$
- 空间复杂度：$O(1)$

