# 106. Construct Binary Tree from Inorder and Postorder Traversal

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
    /*
    通过中序和后续构造二叉树
    中序: 
    */
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return doBuild(inorder, 0, inorder.length-1, postorder, 0, postorder.length-1);
    }
    
    public TreeNode doBuild(int[] inorder, int inL, int inR, int[] postorder, int poL, int poR){
        if(inL > inR || poL > poR) return null;
        int rIdx = findRootIdx(inorder, inL, inR, postorder[poR]);
        TreeNode root = new TreeNode(postorder[poR]);
        root.left = doBuild(inorder, inL, rIdx-1, postorder, poL, poL+rIdx-inL-1);
        root.right = doBuild(inorder, rIdx+1, inR, postorder, poL+rIdx-inL, poR-1);
        return root;
    }
    
    private int findRootIdx(int[] inorder, int inL, int inR, int root){
        for(int i=inL; i<=inR; i++){
            if(inorder[i] == root)
                return i;
        }
        return -1;
    }
}
```

