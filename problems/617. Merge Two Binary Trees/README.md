# 617. Merge Two Binary Trees

## #1 先序遍历

### 思路

采用先序遍历的方式，对于当前节点，我们需要执行三个操作：

1. 将第二课树的当前节点值加到第一课树上；
2. 考虑第一课树和第二课树的左子树情况：
   - 如果第一课树没有左子树，而第二课树有左子树，此时直接将第二课树的左子树赋给第一棵树；
   - 如果第一课树有左子树，第二课树没有左子树，此时左子树已经完成，不需要继续遍历；
   - 如果第一课和第二棵树都有左子树，递归遍历这两颗子树。
3. 考虑右子树的情况

### 算法

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
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null) return t2;
        if(t2 == null) return t1;
        preorder(t1, t2);
        return t1;
    }
    
    public void preorder(TreeNode t1, TreeNode t2){
        t1.val += t2.val; //先序遍历根节点
        //考虑左子树
        if(t1.left==null && t2.left!=null){
            t1.left = t2.left;
        }else if(t1.left != null && t2.left != null){
            preorder(t1.left, t2.left);
        }
        //考虑右子树
        if(t1.right == null && t2.right != null){
            t1.right = t2.right;
        }else if(t1.right != null && t2.right != null)
            preorder(t1.right, t2.right);
    }
}
```

### 复杂度分析

- 时间复杂度：
- 空间复杂度：