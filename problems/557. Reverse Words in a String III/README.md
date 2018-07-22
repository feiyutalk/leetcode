# 557. Reverse Words in a String III

## #1 识别单词[AC]

### 思路

将字符串转为字符数组，然后线性扫描字符数组，通过判断当前是否为空格，来识别字符数组中的单词，一旦识别到单词，就用`i,j`指向单词的起始点和终止点，然后逆序这个单词。

### 算法

```java
class Solution {
    public String reverseWords(String s) {
        /*
        用i,j保存每个单词的起始和终止位置
        用k表示已经遍历到的位置
        */
        if(s == null || s.length() == 0) return s;
        char[] chars = s.toCharArray();
        int i=0, j=0;
        for(int k=0; k<s.length(); k++){
            // System.out.print("k="+k);
           if(chars[k] == ' ')
               continue;
            i = k;
            j = k;
            while(j < s.length() && chars[j] != ' ')
                j++;
            j--;
            k = j;
            for(;i<j; i++, j--){
                char temp = chars[i];
                chars[i] = chars[j];
                chars[j] = temp;
            }
            // System.out.println(",String="+new String(chars));
        }
        return new String(chars);
    }
}
```

### 复杂度分析

- 时间复杂度
- 空间复杂度