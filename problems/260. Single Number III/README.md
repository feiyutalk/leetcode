# 260. Single Number III
## #1 暴力搜索[AC]
我们可以利用HashMap这种数据结构来记录元素及其属性，那么这道题的属性就是该元素出现的次数。当我们把这个数据结构构建起来之后，算法就简单了，只要去遍历就可以了。这样的解法时间复杂度和空间复杂度都是O(n)的。

```java

class Solution {
    public int[] singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        
        for(int num : nums){
            map.put(num, map.getOrDefault(num,0)+1);
        }
        
        ArrayList<Integer> result = new ArrayList<>();
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() == 1)
                result.add(entry.getKey());
        }
        int[] arr = new int[result.size()];
        for(int i=0; i<result.size(); i++){
            arr[i] = result.get(i);
        }
        return arr;
    }
}
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## #2 位操作[AC]

这道题目用位操作来求解有一定的难度。

**思路**

- **第一步**：肯定还是像我们上面的解法一样，所有数进行`异或`，不过最终得到的结果是 a 和 b（假设 a 和 b 是落单的数字）两个值的异或结果 a XOR b，没有直接得到 a 和 b 的值；
- **第二步：**想办法得到 a 或者 b，假设 aXORb 为 `00001001`（F肯定不为0），根据 aXORb 的值我们发现，`值为1的位`（比如从右向左第一位）表示在此位上 a 和 b 的值不同；所以，根据这个特点，我们首先得到从右往左的第一个1，通过`aXORb & -aXORb`得到。
- **第三步**：第二步中得到的了最后一个位置上的1，这个1表示，在该位置上，a和b是不一样的，也就是有可能该位置a为0，b为1；也有可能a为1，b为0。我们根据这个特点来得到a，b。请注意，在这一步，我们仍然遍历整个数组，在结果数组进行存储的时候，我们采用`res ^= num`的方式，还记得吗？那些重复的元素会通过这个操作被过滤掉，只剩下出现一次的元素，而我们在条件里加了`diff & num == 0`这个条件来区分`a`和`b`。

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        if(nums == null || nums.length == 0)
            return new int[0];
        int[] res = new int[2];
        int diff = 0;
        for(int num : nums)
            diff ^= num; 
        // then the diff store the result :  a ^ b
        diff &= -diff; // get the last 1
        for(int num : nums){
            if((diff & num) == 0)
                res[0] ^= num;
            else
                res[1] ^= num;
        }
        return res;
    }
}
```



