# 401. Binary Watch

## #1 暴力搜索[AC]

### 思路

我们遍历所有的可能的表示方式，总共有$12*60$种，对于每一种表示方式，判断其位数之和是否等于给定的`num`，如果是的话就有效，将其加入到结果中，否则无效。

### 算法

```java
class Solution {
    public List<String> readBinaryWatch(int num) {
        if(num <= 0) return new ArrayList<String>();
        ArrayList<String> result = new ArrayList<>();
        for(int i=0; i<12; i++){
            for(int j=0; j<60; j++){
                if(Integer.bitCount(i) + Integer.bitCount(j) == num){
                    result.add(String.format("%d:%02d", i, j));
                }
            }
        }
        return result;
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(12*60*32)$
- 空间复杂度：$O(1)$

