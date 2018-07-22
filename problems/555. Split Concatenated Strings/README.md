# 555. Split Concatenated Strings

## #1 深度优先搜索[TLE]

### 思路

通过深度优先遍历所有可能的组合，然后对每种可能的组合，遍历所有可能的切分点。

### 算法

```java
class Solution {
    String res = "";
    public String splitLoopedString(String[] strs) {
        dfs(strs, "", 0, strs.length);
        return res;
    }
    
    public void dfs(String[] strs, String s, int i, int n){
        if(i < n){
            dfs(strs, s + strs[i], i+1, n);
            dfs(strs, s + new StringBuffer(strs[i]).reverse().toString(), i+1, n);
        }else{
            for(int j=0; j<s.length(); j++){
                String cut = s.substring(j) + s.substring(0, j);
                if(cut.compareTo(res) > 0)
                    res = cut;
            }
        }
    }
}
```

### 复杂度分析

## #2 广度优先遍历[MLE]

### 思路

想法和上面是一样的，就是在枚举的时候采用广度优先的做法。

### 算法

```java
class Solution {
    public String splitLoopedString(String[] strs) {
        String res = "";
        Queue<String> queue = new LinkedList<>();
        queue.offer("");
        int i=0, j=0;
        while(i < strs.length){
            String cur = queue.poll();
            queue.offer(cur+strs[i]);
            queue.offer(cur + new StringBuffer(strs[i]).reverse().toString());
            j++;
            if(j == 1<<i){
                i++;
                j=0;
            }
        }
        while(!queue.isEmpty()){
            String cur = queue.poll();
            for(int k=0; k<cur.length(); k++){
                String cut = cur.substring(k) + cur.substring(0, k);
                if(cut.compareTo(res) > 0)
                    res = cut;
            }
        }
        return res;
    }
}
```

### 复杂度分析

## #3 优化枚举

### 思路

### 算法

```java
class Solution {
    public String splitLoopedString(String[] strs) {
        for(int i=0; i<strs.length; i++){
            String rev = new StringBuffer(strs[i]).reverse().toString();
            if(rev.compareTo(strs[i]) > 0)
                strs[i] = rev;
        }
        String res = "";
        for(int i=0; i<strs.length; i++){
            String rev = new StringBuffer(strs[i]).reverse().toString();
            for(String s : new String[]{strs[i], rev}){
                for(int k=0; k<s.length(); k++){
                    StringBuffer temp = new StringBuffer();
                    temp.append(s.substring(k));
                    for(int j=i+1; j<strs.length; j++)
                        temp.append(strs[j]);
                    for(int j=0; j<i; j++){
                        temp.append(strs[j]);
                    }
                    temp.append(s.substring(0, k));
                    if(temp.toString().compareTo(res) > 0)
                        res = temp.toString();
                }
            }
        }
        return res;
    }
}
```

