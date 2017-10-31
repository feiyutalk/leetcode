# 94. Binary Tree Inorder Traversal

# Description

Given a binary tree, return the *inorder* traversal of its nodes' values.

For example:
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return `[1,3,2]`.

# Solution

这道题目挺奇怪的，就考了一个树的中序遍历，直接使用递归中序遍历就可以了，可能还有其他的解法吧，先不管了，直接写中序遍历就可以AC了。

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        doInorder(root, result);
        return result;
    }
    
    private void doInorder(TreeNode root, List<Integer> result){
        if(root == null)
            return;
        doInorder(root.left, result);
        result.add(root.val);
        doInorder(root.right, result);
    }
}
```

