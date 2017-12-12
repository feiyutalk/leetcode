# 663. Equal Tree Partition

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
   boolean equal = false;
    long total = 0;
    
    public boolean checkEqualTree(TreeNode root) {
        if (root.left == null && root.right == null) return false;
        total = getTotal(root);
        checkEqual(root.left);
        checkEqual(root.right);
        return equal;
    }
    
    private long getTotal(TreeNode root) {
        if (root == null) return 0;
        return getTotal(root.left) + getTotal(root.right) + root.val;
    }
    
    private long checkEqual(TreeNode root) {
        if (root == null || equal) return 0;
        
        long curSum = checkEqual(root.left) + checkEqual(root.right) + root.val;
        if (total - curSum == curSum) {
            equal = true;
            return 0;
        }
        return curSum;
    }
}
```

