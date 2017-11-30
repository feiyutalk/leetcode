# 104. Maximum Depth of Binary Tree

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
    private int max = 0;
    public int maxDepth(TreeNode root) {
        if(root == null)
            return 0;
        helper(root, 1);
        return max;
    }
    
    private void helper(TreeNode root, int path){
        if(root == null)
            return;
        if(root.left == null && root.right == null){
            max = Math.max(max, path);
        }
        helper(root.left, path+1);
        helper(root.right, path+1);
    }
}
```

