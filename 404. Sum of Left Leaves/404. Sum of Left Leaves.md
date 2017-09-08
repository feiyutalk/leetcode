# 404. Sum of Left Leaves
## Description

```
Difficulty: Easy
```

Find the sum of all left leaves in a given binary tree.

Example:

	    3
	   / \
	  9  20
	    /  \
	   15   7
	
	There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
## Solution 1
我们怎么去找到既是叶子节点，又是左孩子的？由于这个节点判定和父节点的关系比较大，因为我们需要知道当前节点是属于父节点的左孩子还是右孩子，所以我们可以考虑采用层次遍历，这种遍历方式，我们可以知道我们当前要遍历的节点是父节点的左孩子还是右孩子。

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
    public int sumOfLeftLeaves(TreeNode root) {
        //boundary condition
        if(root == null)
            return 0;
        //normal condition
        //1.init
        int sum = 0;
        Queue<TreeNode> queue = new LinkedList<>();
        if(root.left == null && root.right == null)
            return sum;
        queue.offer(root);
        //2. while
        while(!queue.isEmpty()){
            TreeNode cur = queue.poll();
            if(cur.left!=null){
                if(cur.left.left == null && cur.left.right == null)
                    sum += cur.left.val;
                else
                    queue.offer(cur.left);
            }
            if(cur.right!=null){
                queue.offer(cur.right);
            }
        }
        return sum;
    }
}

```

***

**enjoy life, coding now! :D**
