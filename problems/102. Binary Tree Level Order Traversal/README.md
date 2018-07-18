# 101. Symmetric Tree
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7

return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
#1 非递归[AC]
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(root == null) return result;
        Vector<TreeNode> q = new Vector<TreeNode>();//没有用自带的队列，直接用动态数组
        TreeNode rear = null;
        TreeNode last = root;
        //根节点入队
        q.add(root);
        List<Integer> row;
        row = new ArrayList<Integer>();
        while(q.size()>0){
            rear = q.get(0);
            q.remove(0);//出队
            row.add(rear.val);
            if(rear.left!=null){
                q.add(rear.left);
            }
            if(rear.right!=null){
                q.add(rear.right);
            }
            if(rear==last){
                result.add(row);
                row = new ArrayList<Integer>();
                if(q.size()>0) last = q.get(q.size()-1);//当每一层的节点刚好出队到最右节点，这时当前节点就是最右节点
            }
        }
        return result;
        
    }
}
```

