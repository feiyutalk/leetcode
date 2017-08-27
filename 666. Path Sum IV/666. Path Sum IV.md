# 666. Path Sum IV
## Description

```
Difficulty: Easy
```

If the depth of a tree is smaller than 5, then this tree can be represented by a list of three-digits integers.

For each integer in this list:

1. The hundreds digit represents the depth D of this node, 1 <= D <= 4.

2. The tens digit represents the position P of this node in the level it belongs to, 1 <= P <= 8. The position is the same as that in a full binary tree.

3. The units digit represents the value V of this node, 0 <= V <= 9.
Given a list of ascending three-digits integers representing a binary with the depth smaller than 5. You need to return the sum of all paths from the root towards the leaves.

Example 1:

	Input: [113, 215, 221]
	Output: 12
	Explanation: 
	The tree that the list represents is:
	    3
	   / \
	  5   1
	
	The path sum is (3 + 5) + (3 + 1) = 12.

Example 2:

	Input: [113, 221]
	Output: 4
	Explanation: 
	The tree that the list represents is: 
	    3
	     \
	      1
	
	The path sum is (3 + 1) = 4.
## Solution 1
  首先，题目提到了满二叉树，那么满二叉树的一些最重要的性质我们需要牢记:

1.可以对满二叉树进行编号(从1开始)，这样编完号之后，对于任意节点i，它的父节点编号为i/2,它的左孩子的编号为2 * i-1,它的右孩子的编号为2 * i。

整个题目还是一个关于树的问题，它要求的是路径和！那这时候，需要考虑用什么样的遍历方式，这边想到的是层次遍历，因为路径，是从上往下走的，所以和层次遍历的模式比较相近。那层次遍历的时候，我们需要的额外操作就是记录下每个节点，从根到它这个节点的路径和，
我们采用一个map来存储。

这道题目和之前树的题目的不同点在于，需要自己根据额外的信息来获得当前节点的左右孩子。对于任意的一个三位数代表的节点 ijk，如果获得它的左右孩子。
 左:(i+1)(2j-1)?
 右:(i+1)(2j)?

```java

class Solution {
    public int pathSum(int[] nums) {
        // I
        if(nums == null || nums.length == 0)
            return 0;
        
        // II
        // 1. init
        // 1.1 init queue set 
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> set = new HashSet<>();
        int result = 0;
        Map<Integer, Integer> map = new HashMap<>();
        // 1.2 visit first node
        map.put(nums[0], getUnit(nums[0]));
        queue.offer(nums[0]);
        set.add(nums[0]);
        
        // 2. while
        while(!queue.isEmpty()){
            // 2.1 poll node
            Integer cur = queue.poll();
            int left = -1;
            int right = -1;
            // 2.2 judge left & right
            if((left = getLeft(cur, nums)) > 0){
                map.put(left, map.get(cur) + getUnit(left));
                queue.offer(left);
                set.add(left);
            }
            if((right = getRight(cur, nums)) > 0){
                map.put(right, map.get(cur) + getUnit(right));
                queue.offer(right);
                set.add(right);
            }
            //路径和是从根节点 到 叶子节点的， 所以我们需要判断当前是否为叶子节点
            if(left == -1 && right == -1)
                result += map.get(cur);
        }
        return result;
    }
    
    public int getUnit(int num){
        return num % 10;
    }
    
    public int getTen(int num){
        return (num/10) % 10;
    }
    
    public int getHundred(int num){
        return (num/100) % 10;
    }
    
    public int getLeft(int cur, int[] nums){
        int ten = getTen(cur);
        int hundred = getHundred(cur);
        for(int num : nums){
            if(getHundred(num) == hundred + 1 && getTen(num) == (2*ten - 1))
                return num;
        }
        return -1;
    }
    
    public int getRight(int cur, int[] nums){
        int ten = getTen(cur);
        int hundred = getHundred(cur);
        for(int num : nums){
            if(getHundred(num) == hundred + 1 && getTen(num) == (2*ten))
                return num;
        }
        return -1;
    }
}
```

***

**enjoy life, coding now! :D**
