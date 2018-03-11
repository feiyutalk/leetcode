# 095. Unique Binary Search Trees II

# #1 递归(AC)

这道题目我们采用递归的构建方式，因为是二叉搜索树，所有左子树的值比根节点小，右子树的值比根节点大。我们递归的遍历根节点每一种可能的取值，对于每一种取值val, 左子树的范围在[min, k-1]，右子树的范围在[k+1, max]，然后递归的左，右子树。此时，被调用函数向调用函数返回的应该是一个List，记录每一种可能的构建情况的根节点。

这虽然也是树类型常见的递归的题目，但是可以看到此时被调用函数向调用函数返回的一个子树的集合，这是之前没有遇到过的。

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
    public List<TreeNode> generateTrees(int n) {
        return doGenerate(1, n);
    }
    
    private List<TreeNode> doGenerate(int min, int max){
        List<TreeNode> result = new ArrayList<>();
        if(min > max) return result;
        for(int val=min; val<=max; val++){
            List<TreeNode> left = doGenerate(min, val-1);
            List<TreeNode> right = doGenerate(val+1, max);
            if(left.size() == 0 && right.size() == 0){
                TreeNode root = new TreeNode(val);
                result.add(root);
            }else if(right.size() == 0){
                for(TreeNode lnode: left){
                    TreeNode root = new TreeNode(val);
                    root.left = lnode;
                    result.add(root);
                }
            }else if(left.size() == 0){
                for(TreeNode rnode : right){
                    TreeNode root = new TreeNode(val);
                    root.right = rnode;
                    result.add(root);
                }
            }else{
                for(TreeNode lnode : left){
                    for(TreeNode rnode : right){
                        TreeNode root = new TreeNode(val);
                        root.left = lnode;
                        root.right = rnode;
                        result.add(root);
                    }
                }
            }
        }
        return result;
    }
    
}
```

