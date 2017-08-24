# 107. Binary Tree Level Order Traversal II
## Description

```
Difficulty: Easy
```
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:

Given binary tree [3,9,20,null,null,15,7],

	    3
	   / \
	  9  20
	    /  \
	   15   7

return its bottom-up level order traversal as:

	[
	  [15,7],
	  [9,20],
	  [3]
	]
## Solution 1
  我们需要对树进行层次遍历，而对于层次遍历的算法模板我们应该牢记！涉及到层次遍历的题目，我们只需要把层次遍历的算法模板先搭好，然后结合具体的题目做一些额外的操作即可。这道题，我们可以通过一个map，key是level（层数），value是该层所有元素构成的一个List。然后最后，将level大的先添加到结果List中。

```java

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    class Item{
        TreeNode node;
        int level;
        public Item(TreeNode node, int level){
            this.node = node;
            this.level = level;
        }
    }
    
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        // I
        if(root == null)
            return new ArrayList<List<Integer>>();
        // II
        List<List<Integer>> result = new ArrayList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        int max = 1;
        
        //level search
        //1.initialize
        Queue<Item> queue = new LinkedList<>();
        Set<TreeNode> set = new HashSet<>();
        List<Integer> nodes = new ArrayList<>();
        nodes.add(root.val);
        map.put(1, nodes);
        queue.offer(new Item(root, 1));
        set.add(root);
        
        //2. while
        while(!queue.isEmpty()){
            // 2.1 poll
            Item cur = queue.poll();
            int level = cur.level + 1;
            List<Integer> temp = map.get(level);
            if(temp == null)
                temp = new ArrayList<>();
            // 2.2 left right
            TreeNode curNode = cur.node;
            if(curNode.left != null){
                temp.add(curNode.left.val);
                queue.offer(new Item(curNode.left, level));
                set.add(curNode.left);
            }
            
            if(curNode.right != null){
                temp.add(curNode.right.val);
                queue.offer(new Item(curNode.right, level));
                set.add(curNode.right);
            }
            
            if(!temp.isEmpty())
                map.put(level, temp);
            
            max = level;
        }
        
        for(int i=max-1; i>=1; i--){
            result.add(map.get(i));
        }
        
        return result;
    }
}
```

***

**enjoy life, coding now! :D**
