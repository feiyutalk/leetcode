# 113. Path Sum II

# Description

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and sum = 22,

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

return

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

# Solution

这道题目的主要矛盾在于需要遍历到每个叶子节点，但是在访问叶子节点的时候，需要把从根节点到该叶子节点的路径记录下来，这种场景是非常符合层次遍历的特点的，层次遍历要求从上往下，一层一层的遍历。而且前面也总结了层次遍历的模板了，所以写起来应该是比较快的。

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
        List<Integer> ancestors;
        public Item(TreeNode node, List<Integer> ancestors){
            this.node = node;
            this.ancestors = ancestors;
        }
    }
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        //boundary condition
        if(root == null)
            return new ArrayList<List<Integer>>();
        if(root.left == null && root.right == null){
            if(root.val == sum){
                ArrayList<List<Integer>> result = new ArrayList<>();
                result.add(Arrays.asList(new Integer(root.val)));
                return result;
            }
        }
        //normal condition
        Queue<Item> queue = new LinkedList<>();
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        queue.offer(new Item(root, Arrays.asList(new Integer(root.val))));
        while(!queue.isEmpty()){
            Item cur = queue.poll();
            TreeNode curNode = cur.node;
            List<Integer> curAncestors = cur.ancestors;
            if(curNode.left != null){
                if(isLeaf(curNode.left)){
                    if(getPathSum(curAncestors, curNode.left.val) == sum){
                        List<Integer> temp = new ArrayList<>(curAncestors);
                        temp.add(curNode.left.val);
                        result.add(temp);
                    }
                }else{
                    List<Integer> temp = new ArrayList<>(curAncestors);
                    temp.add(curNode.left.val);
                    queue.offer(new Item(curNode.left, temp));
                }
            }
            if(curNode.right != null){
                if(isLeaf(curNode.right)){
                    if(getPathSum(curAncestors, curNode.right.val) == sum){
                        List<Integer> temp = new ArrayList<>(curAncestors);
                        temp.add(curNode.right.val);
                        result.add(temp);
                    }
                }else{
                    List<Integer> temp = new ArrayList<>(curAncestors);
                    temp.add(curNode.right.val);
                    queue.offer(new Item(curNode.right, temp));
                }
            }
        }
        return result;
    }
    
    private boolean isLeaf(TreeNode node){
        return node.left == null && node.right == null;
    }
    
    private int getPathSum(List<Integer> ancestors, int val){
        int sum = val;
        for(int path : ancestors){
            sum += path;
        }
        return sum;
    }
}
```

