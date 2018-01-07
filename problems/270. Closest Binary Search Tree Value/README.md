# 270. Closest Binary Search Tree Value

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
    double min = Double.MAX_VALUE;
    int res = 0;
    public int closestValue(TreeNode root, double target) {
        inorder(root, target);
        return res;
    }
    
    public void inorder(TreeNode root, double target){
        if(root == null) return;
        if(Math.abs((double)root.val - target) < min){
            min = Math.abs(root.val - target);
            res = root.val;
        }
        inorder(root.left, target);
        inorder(root.right, target);
    }
}
```

