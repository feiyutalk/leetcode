# 285. Inorder Successor in BST

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
    private TreeNode target;
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if(root == null || p == null)
            return null;
        List<Integer> res = new ArrayList<>();
        inorder(res, root);
        int index = 0;
        for(int i=0; i<res.size(); i++){
            if(res.get(i) == p.val){
                index = i;
                break;
            }
        }
        if(index == res.size() - 1)
            return null;
        int sucVal = res.get(index + 1);
        find(root, sucVal);
        return target;
    }
    
    private void find(TreeNode root, int val){
        if(root == null)
            return;
        if(root.val == val)
            target = root;
        find(root.left, val);
        find(root.right, val);
    }
    
    private void inorder(List<Integer> res, TreeNode root){
        if(root == null)
            return ;
        inorder(res, root.left);
        res.add(root.val);
        inorder(res, root.right);
    }
}
```

