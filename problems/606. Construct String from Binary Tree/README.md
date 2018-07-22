# 606. Construct String from Binary Tree

## #1 控制递归条件

### 思路

对于当前节点的不同状态，执行不同的递归条件，从而可用控制加括号的方式。

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
    public String tree2str(TreeNode t) {
        StringBuffer sb = new StringBuffer();
        preorder(t, sb);
        return sb.toString();
    }
    
    public void preorder(TreeNode t, StringBuffer sb){
        if(t == null)
            return;
        if(t.left!= null && t.right != null){
            sb.append("" + t.val);
            // 左子树
            sb.append("(");
            preorder(t.left, sb);
            sb.append(")");

            // 右子树
            sb.append("(");
            preorder(t.right, sb);
            sb.append(")");
        }else if(t.left == null && t.right != null){
            sb.append("" + t.val);
            sb.append("(");
            sb.append(")");
            sb.append("(");
            preorder(t.right, sb);
            sb.append(")");
        }else if(t.right == null && t.left != null){
            sb.append("" + t.val);
            // 左子树
            sb.append("(");
            preorder(t.left, sb);
            sb.append(")");
        }else{
            sb.append("" + t.val);
        }
    }
}
```

### 复杂度分析

- 时间复杂度
- 空间复杂度

