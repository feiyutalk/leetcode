# 187. Repeated DNA Sequences

## #1 暴力搜索[AC]

暴力搜索所有可能的长度为10的连续子串，通过数组记录该子串是否出现过，如果出现过，就添加到结果数组中；否则，就将其记录。这里，可以考虑将字符串转化为数值来减少计算复杂度。

```java
class Solution {
    public void reverseWords(char[] str) {
        // 1. reverse the whole sentence
        reverse(str, 0, str.length-1);
        // 2. reverse each word
        int start = 0;
        for(int i=0; i<str.length; i++){
            if(str[i] == ' '){
                reverse(str, start, i-1);
                start = i+1;
            }
        }
        // 3. reverse last word
        reverse(str, start, str.length-1);
    }
    
    private void reverse(char[] str, int start, int end){
        while(start < end){
            char temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
    }
}
```

