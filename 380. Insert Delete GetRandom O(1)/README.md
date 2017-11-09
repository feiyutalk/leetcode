# 380. Insert Delete GetRandom O(1)

这道题目是构造数据结构的题目，这种题目一般的做法就是用已有的数据结构进行组合。我们需要知道每种数据结构的特点，比如ArrayList()支持随机访问，读写的时间复杂度为O(1)，但是插入删除的时间复杂度为O(n)。HashMap读写，插入删除的时间复杂度都是O(1)，但是需要额外的空间，而且不支持随机访问。

这道题目，我们应该组合ArrayList和HashMap两种数据结构，利用ArrayList提供随机访问的功能，利用HashMap来达到插入和删除的时间复杂度都是O(1)。

除了上面分析，在组合多种数据结构的时候，一个关键问题是如何保持各个数据结构中数据的一致性，比如上面说的ArrayList和HashMap，因为用HashMap来保持插入和删除的时间复杂度为O(1)，但是当对HashMap进行删除的时候，如何也对ArrayList进行删除，而且，保证时间复杂度也为O(1)呢？一般的做法就是将要删除的元素移到指定的位置，然后删除，这个指定的位置一般是数组头或者尾。

所以，总结一下数据构造问题需要解决的两个关键问题：

1. 选择哪些数据结构进行组合，这里要求我们对各个数据结构比较熟悉。
2. 如何保持各个数据结构里面数据的一致。

```java
class RandomizedSet {
    HashMap<Integer, Integer> map;
    List<Integer> nums; 
    Random rand = new Random();
    /** Initialize your data structure here. */
    public RandomizedSet() {
        map = new HashMap<>();
        nums = new ArrayList<>();
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    public boolean insert(int val) {
        if(map.containsKey(val)) return false;
        nums.add(val);
        map.put(val, nums.size()-1);
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    public boolean remove(int val) {
        if(!map.containsKey(val)) return false;
        int index = map.get(val);
        if(index != nums.size()-1){
            int lastone = nums.get(nums.size()-1);
            map.put(lastone, index);
            nums.set(index, lastone);
        }
        nums.remove(nums.size()-1);
        map.remove(val);
        return true;
    }
    
    /** Get a random element from the set. */
    public int getRandom() {
        return nums.get(rand.nextInt(nums.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

