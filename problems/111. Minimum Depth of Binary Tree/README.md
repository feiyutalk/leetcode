# 111. Minimum Depth of Binary Tree

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
    private int min = Integer.MAX_VALUE;
    public int minDepth(TreeNode root) {
        if(root == null)
            return 0;
        helper(root, 1);
        return min;
    }
    
    private void helper(TreeNode root, int path){
        if(root == null)
            return;
        if(root.left == null && root.right == null)
            min = Math.min(min, path);
        helper(root.left, path+1);
        helper(root.right, path+1);
    }
}
```

