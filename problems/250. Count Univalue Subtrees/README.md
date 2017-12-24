# 250. Count Univalue Subtrees

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
    private int res = 0;
    public int countUnivalSubtrees(TreeNode root) {
        helper(root);
        return res;
    }
    
    private boolean helper(TreeNode root){
        if(root == null){
            return true;
        }
        boolean left = helper(root.left);
        boolean right = helper(root.right);
        if(left && right){
            if(root.left == null && root.right == null){
                res += 1;
                return true;
            }else if(root.left == null && root.right != null){
                if(root.val == root.right.val){
                    res += 1;
                    return true;
                }else{
                    return false;
                }
            }else if(root.left != null && root.right == null){
                if(root.val == root.left.val){
                    res += 1;
                    return true;
                }else{
                    return false;
                }
            }else{
                if(root.val == root.left.val && root.val == root.right.val){
                    res += 1;
                    return true;
                }else{
                    return false;
                }
            }
        }else{
            return false;
        }
    }
}
```

