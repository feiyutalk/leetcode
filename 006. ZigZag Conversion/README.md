# 6. ZigZag Conversion
## Description

```
Difficulty: Medium
```

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

	P   A   H   N
	A P L S I I G
	Y   I   R

And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

	string convert(string text, int nRows);

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".


ZigZag Pattern:

	Δ=2n-2    1                           2n-1                         4n-3
	Δ=        2                     2n-2  2n                    4n-4   4n-2
	Δ=        3               2n-3        2n+1              4n-5       .
	Δ=        .           .               .               .            .
	Δ=        .       n+2                 .           3n               .
	Δ=        n-1 n+1                     3n-3    3n-1                 5n-5
	Δ=2n-2    n                           3n-2                         5n-4
## Solution 1. StringBuffer数组
这道题目的难点并不在于算法本身，其实上算法和数据结构应该分不开的，题目有的需要复杂的数据结构简单的算法，有的简单的数据结构复杂的算法等等。那么这道题目的算法其实就是依次取字符串中的字符，然后从上往下排列，紧着从左下角往右上角排列，重复进行此过程。难点在于，我们选择什么样的数据结构比较好处理这个问题。如果选择二维数组的话，其实上也可以，就是需要预先去求解数组的大小，所以我们这边采用StringBuffer[]这种数据结构。

```java

class Solution {
    public String convert(String s, int numRows) {
        // boundary condition
        if(s == null)
            return null;
        if(s.length() == 0 || numRows<1)
            return "";
        // normal condition
        // init data structure
        StringBuffer[] buffers = new StringBuffer[numRows];
        for(int i=0; i<buffers.length; i++)
            buffers[i] = new StringBuffer();
        char[] chars = s.toCharArray();
        int count = 0;
        
        // algorithm
        while(count<s.length()){
            // up ---> down
            for(int i=0; i<numRows && count<s.length(); i++){
                buffers[i].append(chars[count++]);
            }
            
            // down left  ---> up right
            for(int i=numRows-2; i>=1 && count<s.length(); i--){
                buffers[i].append(chars[count++]);
            }
        }
        
        for(int i=1; i<buffers.length; i++){
            buffers[0].append(buffers[i]);
        }
        return buffers[0].toString();
    }
}
```

***

**enjoy life, coding now! :D**
