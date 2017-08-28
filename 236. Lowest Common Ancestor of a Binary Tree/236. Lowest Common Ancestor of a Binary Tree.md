# 236. Lowest Common Ancestor of a Binary Tree
## Description

```
Difficulty: Medium
```
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

	        _______3______
	       /              \
	    ___5__          ___1__
	   /      \        /      \
	   6      _2       0       8
	         /  \
	         7   4
For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
## Solution 1
  首先，问题是求解两个节点的最近的公共祖先，但是我们大概考虑一下会发现，这个公共祖先可能和两个节点在树中的位置有关。

1. 如果两个节点有一个是根节点，那么该节点就是所要的结果。
2. 如果两个节点都不是根节点，两个节点如果一个在左子树，一个在右子树，那这时候直接返回当前的根节点就行了 。
3. 如果两个节点都在左子树，或者两个节点都在右子树。递归求解。

以上就是严格的分类情况，那么这时候我们需要考虑想求解哪些情况，这对于我们代码编写的复杂度有帮助（我们想要先求解简单的情况，复杂情况不直接求解，而是通过排除简单的情况之后直接得到复杂的情况）。第一种情况最简单，可以先求！现在分析情况二，这个时候我们需要去判断p是否在左子树q在右子树或者p在右子树q在左子树，比较复杂，考虑情况三，递归求解代码简单，可以先写情况三。

```java

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        //I
        if(root == null || p == null || q == null)
            return null;
        // II
        if(root == p || root == q)
            return root;
        TreeNode left = lowestCommonAncestor(root.left, p ,q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left != null && right != null)
            return root;
        return left != null ? left : right;
    }
}
```

***

**enjoy life, coding now! :D**
