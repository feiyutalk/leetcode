# 111. Minimum Depth of Binary Tree
Given a binary tree, find its minimum depth.</br>
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.</br>
Note: A leaf is a node with no children.</br>
Example:</br>
Given binary tree [3,9,20,null,null,15,7]</br>
```
    3
   / \
  9  20
    /  \
   15   7
```
# 1 递归[AC]
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
    private int min = Integer.MAX_VALUE;
    public int minDepth(TreeNode root) {
        if(root == null)
            return 0;
        helper(root, 1);
        return min;
    }
    
    private void helper(TreeNode root, int path){
        if(root == null)
            return;
        if(root.left == null && root.right == null)
            min = Math.min(min, path);
        helper(root.left, path+1);
        helper(root.right, path+1);
    }
}
```
# 2 非递归[AC]
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
import java.util.Vector;

class Solution {
    public int minDepth(TreeNode root) {
        Vector<TreeNode> s = new Vector<TreeNode>();
        int level = 1;
        TreeNode cur = root;
        TreeNode last = root;//记录每层最右节点
        if(root==null){
            return 0;
        }
        s.add(cur);
        while(cur!=null||s.size()>0){
            cur = s.get(0);
            s.remove(0);
            if(cur.left==null&&cur.right==null){
                return level;
            }
            if(cur.left!=null){
                s.add(cur.left);
            }
            if(cur.right!=null){
                s.add(cur.right);
            }
            if(last==cur){
                level++;
                last=s.get(s.size()-1);
            }
        }
        return level;
    }
}
```
