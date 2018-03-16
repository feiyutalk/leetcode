# 144. Binary Tree Preorder Traversal

## #1 递归[AC]

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        helper(root, res);
        return res;
    }
    
    private void helper(TreeNode root, List<Integer> res){
        if(root == null)
            return;
        res.add(root.val);
        helper(root.left, res);
        helper(root.right, res);
    }
}
```

