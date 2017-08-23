# 662. Maximum Width of Binary Tree
## Description

```
Difficulty: Medium
```

Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a full binary tree, but some nodes are null.

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the null nodes between the end-nodes are also counted into the length calculation.

## Solution 1
  我们首先需要知道满二叉树的特点。我们可对满二叉树按层序编号:约定编号从根节点起（根节点编号为1），自上而下，自左向右。对于任意给定的一个编号为i的节点:

1. 它的父亲的编号为i/2 
2. 它的左孩子的编号为2*i
3. 它的右孩子的编号为2*i+1

  我们可以采用层次遍历，对每个元素得到它的层次以及编号，并把同一层次上的所有节点的编号都保存下来，最后对每个层次的节点编号序列去求最大宽度。

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
    public int widthOfBinaryTree(TreeNode root) {
        Map<Integer, List<Integer>> result = levelSearch(root);
        int max = 0;
        for(List<Integer> list : result.values()){
            max = Math.max(max, list.get(list.size()-1) - list.get(0) + 1);
        }
        return max;
    }
    
    public Map<Integer, List<Integer>> levelSearch(TreeNode root){
        Map<Integer, List<Integer>> result = new HashMap<>();
        Queue<Item> queue = new LinkedList<>();
        queue.offer(new Item(root, 1, 0));
        List<Integer> list = new ArrayList<>();
        list.add(1);
        result.put(0, list);
        while(queue.size() != 0){
            Item item = queue.poll();
            int number = item.number;
            int level = item.level + 1;
            if(item.node.left != null){
                List<Integer> numbers = result.get(level);
                if(numbers == null)
                    numbers = new ArrayList<>();
                numbers.add(number*2);
                result.put(level, numbers);
                queue.offer(new Item(item.node.left, number*2, level));
            }
             if(item.node.right != null){
                List<Integer> numbers = result.get(level);
                if(numbers == null)
                    numbers = new ArrayList<>();
                numbers.add(number*2+1);
                result.put(level, numbers);
                queue.offer(new Item(item.node.right, number*2+1, level));
            }
        }
        return result;
    }
    
    class Item{
        TreeNode node;
        int number;
        int level;
        public Item(TreeNode node, int number, int level){
            this.node = node;
            this.number = number;
            this.level = level;
        }
    }
}
```

***

**enjoy life, coding now! :D**
