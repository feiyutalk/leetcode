# 443. String Compression

# Solution

线性表的问题有时候做起来如果不用比较巧妙方法的话，可能会显得非常的繁琐。线性表需要做的一般都是控制下表指针和统计变量的值，这类题型大部分都是二重循环，当然了，重点在第二层循环，是简单的全循环，还是局部循环，这个做题的时候需要留意。

```java
class Solution {
    public int compress(char[] chars) {
        int indexAns = 0, index = 0;
        while(index < chars.length){
            char cur = chars[index];
            int count = 0;
            while(index < chars.length && chars[index] == cur){
                count++;
                index++;
            }
            chars[indexAns++] = cur;
            if(count != 1)
                for(char c : Integer.toString(count).toCharArray())
                    chars[indexAns++] = c;
        }
        return indexAns;
    }
}
```

