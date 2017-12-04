# 538. Convert BST to Greater Tree

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
    public TreeNode convertBST(TreeNode root) {
        List<Integer> seq = new ArrayList<>();
        inorder(root, seq);
        return root;
    }
    
    private void inorder(TreeNode root, List<Integer> seq){
        if(root == null)
            return ;
        inorder(root.right, seq);
        seq.add(root.val);           
        root.val = sum(seq);
        inorder(root.left, seq);
    }
    
    private int sum(List<Integer> seq){
        int sum = 0;
        for(Integer val : seq)
            sum += val;
        return sum;
    }
}
```

