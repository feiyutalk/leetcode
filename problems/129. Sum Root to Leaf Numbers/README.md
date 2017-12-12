# 129. Sum Root to Leaf Numbers

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
    private int sum = 0;
    public int sumNumbers(TreeNode root) {
        helper(root, 0);
        return sum;
    }
    
    private void helper(TreeNode root, int curSum){
        if(root == null) return;
        if(root.left == null && root.right == null){
            sum += (curSum*10 + root.val);
        }
        helper(root.left, curSum*10+root.val);
        helper(root.right, curSum*10+root.val);
    }
}
```

