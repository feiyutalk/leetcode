# Description

:star2::star2::star2:

![](/images/Binary_Tree_Maximum_Path_Sum.png)

***
## Analysis
这道题目被标为hard，为想最大的难点在于，没有把问题转化为最大公共祖先的问题，任何两点之间的路径，无论怎么连，都会经过一个公共的祖先。所以，我们可以把这个问题转化为，选定一个公共祖先(遍历)，然后分别向左，向右求最大深度，分别记为maxLeft, maxRight， 然后分别比较root.val, root.val + maxLeft, root.val + maxRight, root.val + maxLeft + maxRight, nowMax， 这五个值中最大的一个最为当前最大值，这属于后序遍历。也是在遍历的过程中加操作因子。属于在遍历完左右子树后才加操作因子。
## Solution 转化为公共祖先，然后对任意祖先采用后续遍历

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
public class Solution {
    int ans;
    public int maxDeep(TreeNode root){
        if(root == null){
            return 0;
        }
        if(root.left == null && root.right == null){
            ans = Math.max(ans, root.val);
            return root.val;
        }
        
        int maxLeft = maxDeep(root.left);
        int maxRight = maxDeep(root.right);

        int temp = Math.max(maxLeft, maxRight) + root.val; 
        temp = Math.max(temp, root.val);
        ans = Math.max(ans, temp);
        ans = Math.max(ans, maxLeft + maxRight + root.val);
        return temp;
    }
    
    public int maxPathSum(TreeNode root) {
        ans = 0x80000000;
        maxDeep(root);
        return ans;
    }
}
```
***
enjoy life, coding now! :D
