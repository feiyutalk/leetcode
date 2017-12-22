# 298. Binary Tree Longest Consecutive Sequence

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
    private int res = 1;
    public int longestConsecutive(TreeNode root) {
        if(root == null)
            return 0;
        helper(root, 1, root.val);
        return res;
    }
    
    private void helper(TreeNode root, int count, int value){
        if(root == null)
            return;
        if(root.val == value+1){
            count++;
            res = Math.max(res, count);
        }else{
            count = 1;
        }
        helper(root.left, count, root.val);
        helper(root.right, count, root.val);
    }
}
```

