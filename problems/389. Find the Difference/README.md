# 389. Find the Difference

## #1 统计型数据结构[AC]

### 思路

输入是两个字符串，而我们需要做的是查找两个字符串中字符的区别，然后找到字符串`t`比字符串`s`多的那个字符。所以，我们关注的不是字符串本身，而是字符串中字符的分布情况。我们可以把字符串中的每个字符出现的次数统计出来，得到“字符统计型”数据结构。然后比较这两个数据结构中字符的差异情况即可。

### 算法

```java
class Solution {
    public char findTheDifference(String s, String t) {
        if(s == null || s.length() == 0)
            return t.charAt(0);
        int[] sCount = new int[26];
        int[] tCount = new int[26];
        // get s's char number
        for(int i=0; i<s.length(); i++)
            sCount[s.charAt(i) - 'a']++;
        // get t's char number
        for(int i=0; i<t.length(); i++)
            tCount[t.charAt(i) - 'a']++;
        // find difference 
        for(int i=0; i<26; i++)
            if(sCount[i] != tCount[i])
                return (char)('a' + i);
        return 'a';
    }
}
```

### 复杂性分析：

- 时间复杂性：$O(length(s))$
- 空间复杂性：$O(1)$

## #2 异或位运算[AC]

### 思路

还记得异或的性质吗？简单来说，异或就是**相同为0，不同为1**。所以，两个一模一样的数进行异或得到的结果肯定是0。嗯，这个性质不错。更一般话，出现偶数的数异或的结果是0，出现奇数次的数异或的结果是该数本身。因为，`s`和`t`里面，除了新增的那个数，其他的数出现的次数都是偶数，所以，我们可以通过异或将他们消去。此外0异或任何数都是任何数本身。

### 算法

```java
class Solution {
    public char findTheDifference(String s, String t) {
        if(s == null || s.length() == 0)
            return t.charAt(0);
        char res = 0;
        for(int i=0; i<s.length(); i++)
            res ^= s.charAt(i);
        for(int i=0; i<t.length(); i++)
            res ^= t.charAt(i);
        return res;
    }
}
```

### 复杂性分析：

- 时间复杂性：$O(length(s))$
- 空间复杂性：$