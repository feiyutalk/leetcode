# 098. Validate Binary Search Tree

# Solution

这是一道关于树的题目，现在再来总结一下关于🌲的题目的类型，目前做得比较多的有两种类型:

- 基于递归分治法。(先序、中序和后序)
- 基于层次遍历法。（队列）

这道题是典型的用递归分治法来做的，对于一颗树，要判断它是否是一颗二叉搜索树，我们的判断条件如下:

1. 左右子树都是儿叉搜索树
2. 左子树中所有的节点值都比当前节点值小
3. 右子树中所有的节点值都比当前节点值大

看到三个条件，应该能一下子就意识到，第1个条件用递归就行，第2，3个条件是遍历到节点时的操作因子。紧接着，我们分两个点考虑，首先考虑操作因子: 要判断左子树所有节点是否比当前节点小，只需要遍历左子树就可以了，右子树类似。对于递归，我们之前总结了几个需要考虑的问题:

1. 递归停止的条件
2. 调用函数需要向被调用函数传递的参数
3. 被调用函数需要向调用函数返回什么值

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
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        boolean left = isValidBST(root.left);
        boolean right = isValidBST(root.right);
        if(root.left != null){
            if(!leftInorder(root.left, root.val)) return false;
        }
        if(root.right != null){
            if(!rightInorder(root.right, root.val)) return false;
        }
        return left && right;
    }
    
    private boolean leftInorder(TreeNode node, int val){
        if(node == null)
            return true;
        if(node.val >= val) return false;
        return leftInorder(node.left, val)&&leftInorder(node.right, val);
    }
    
    private boolean rightInorder(TreeNode node, int val){
        if(node == null)
            return true;
        if(node.val <= val) return false;
        return rightInorder(node.left, val)&&rightInorder(node.right, val);
    }
}
```

