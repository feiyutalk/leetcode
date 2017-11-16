# 687. Longest Univalue Path

# Description

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

**Note:** The length of path between two nodes is represented by the number of edges between them.

**Example 1:**

Input:

```
              5
             / \
            4   5
           / \   \
          1   1   5
```

Output:

```
2
```

**Example 2:**

Input:

```
              1
             / \
            4   5
           / \   \
          4   4   5
```

Output:

```
2
```

# Solution

这是一道关于求解二叉树最长路径的问题，只是在求最长路径的时候加了条件。二叉树最长路径的求解使用到的是递归算法， 具体的做法就是先求解出左子树的最长路径，再求解出右子树的最长路径，然后做遍历的操作因子判断，这个判断有两点：一是判断当前构成的最大路径是否比当前保存的最大路径大，如果是的话就更新；二是向调用函数返回该分支的最长路径，这个值等于`Math.max(left,right)+1`。

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
    int maxLength = 0;
    public int longestUnivaluePath(TreeNode root) {
        //boundary condition
        if(root == null)
            return 0;
        getLength(root, root.val);
        return maxLength;
    }
    
    private int getLength(TreeNode root, int val){
        if(root == null)
            return 0;
        int left = getLength(root.left, root.val);
        int right = getLength(root.right, root.val);
        maxLength = Math.max(maxLength, left+right);
        if(root.val == val)
            return Math.max(left, right)+1;
        return 0;
    }
}
```



