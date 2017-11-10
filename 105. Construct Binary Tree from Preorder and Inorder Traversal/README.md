# 105. Construct Binary Tree from Preorder and Inorder Traversal

# Solution

这道题目是树里面比较经典的题目了，根据先序中序构造二叉树，当然也可以根据后序中序构造二叉树，方法当然是采用递归来做了。但是，容易出错的地方就是下标，做的时候需要用一个特例来把下标控制好，举特例的时候记得把值和变量对应上，这样才不会出错。

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        //boundary condition
        if(preorder == null || preorder.length == 0 || inorder == null || inorder.length == 0)
            return null;
        return doBuild(preorder, inorder, 0, preorder.length, 0, inorder.length);
    }
    
    private TreeNode doBuild(int[] preorder, int[] inorder, int preL, int preR, int inL, int inR){
        if(preL > preorder.length-1 || inL > inR) return null;
        //1. build root node
        TreeNode root = new TreeNode(preorder[preL]);
        //2. divide left, right 
        int rootIndex = findRootIndex(inorder, preorder[preL]);
        TreeNode left = doBuild(preorder, inorder, preL+1, preL+rootIndex, inL, rootIndex-1);
        TreeNode right = doBuild(preorder, inorder, preL+rootIndex-inL+1, preR, rootIndex+1, inR);
        root.left = left;
        root.right = right;
        return root;
    }
    
    private int findRootIndex(int[] inorder, int root){
        int index = 0;
        for(int i=0; i<inorder.length; i++){
            if(inorder[i] == root){
                index = i;
                break;
            }
        }
        return index;
    }
}
```

