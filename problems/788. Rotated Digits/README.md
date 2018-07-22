# 788. Rotated Digits

## #1 暴力搜索[AC]

### 思路

1. 对于该数值的每一位，计算其翻转值。如果某一位是不可翻转的，则该数是不可翻转的。
2. 得到翻转后的值，与原值进行比较，如果不同的话，那么就是不符合；如果相同的话， 那么就表示符合。
3. 对每一位数都进行判断，得到最后的结果。

### 算法

```java
class Solution {
    Map<Integer, Integer> map = new HashMap<>();
    public int rotatedDigits(int N) {
        map.put(0,0);
        map.put(1,1);
        map.put(8,8);
        map.put(2,5);
        map.put(5,2);
        map.put(6,9);
        map.put(9,6);
        int res = 0;
        for(int i=1; i<=N; i++)
            if(isValid(i))
                res++;
        return res;
    }
    
    public boolean isValid(int oldVal){
        //System.out.print("oldVal="+oldVal);
        //1. 取出每一位
        //2. 对每一位进行映射，得到新的结果
        //3. 比较旧值和新值
        int backup = oldVal;
        int newVal = 0;
        int count = 0;
        while(oldVal > 0){
            int val = oldVal % 10;
            if(!map.containsKey(val)){
                //System.out.println("can't map");
                return false;
            }
            val = map.get(val);
            oldVal /= 10;
            newVal += (Math.pow(10, count)*val);
            count++;
        }
        //System.out.println("newVal="+newVal);
        return backup != newVal;
    }
}
```

### 复杂度分析

- 时间复杂度：
- 空间复杂度：