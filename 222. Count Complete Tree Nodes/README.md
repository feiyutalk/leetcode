# 222. Count Complete Tree Nodes

通过二分搜索的办法来求解这道题目，因为，对于完全二叉树，除了最后一层叶子节点外，其他层节点都是满的。这样的话，我们可以先统计一下树的高度`h`，然后我们就可以就算出`1~h-1`的节点数，以及如果这个颗是满二叉树，总的节点数$2^h$-1，还有就是如果最后一层是满的，最后一层总的节点数$2^{h-1}$。

现在我们在最后一层里面做二分搜索，我们想找到第一个空的节点的下标k，因为只要找到这个下标，就可以知道最后一层的节点个数，又因为完全二叉树前`h-1`层的节点总数为$2^{h-1}-1$。将两者相加就可以得到完全二叉树的节点个数了。

这个二分搜索属于大于等于的问题，套用相应的模板进行求解即可。在二分搜索的算法里，最后l,r指针肯定会指向同一个位置，如果二分搜索是等于的问题，我们可以在while循环里面返回结果，如果是大于等于问题，我们只要返回最后l的位置即可，所以我们的循环退出条件改成`while(l < r)`。此时，有可能是等于目标值，也有可能大于目标值。但是都是满足我们的条件的。

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
    public int countNodes(TreeNode root) {
        if(root == null) return 0;
        int depth = 0;
        TreeNode temp = root;
        while(temp!=null){
            temp = temp.left;
            depth++;
        }
        int num = (int)(Math.pow(2, depth-1));
        int l=0, r=num-1;
        if(!isNullNode(root, r, num, depth))
            return num*2 - 1;
        
        while(l < r){
            int mid = l + (r-l)/2;
            if(isNullNode(root, mid, num, depth)){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        return num - 1 + l;
    }
    
    private boolean isNullNode(TreeNode root, int k, int num, int depth){
        int d = 0;
        while(root != null){
            num /= 2;
            if(k >= num){
                root = root.right;
                k -= num;
            }else{
                root = root.left;
            }
            d++;
        }
        return d != depth;
    }
}
```



