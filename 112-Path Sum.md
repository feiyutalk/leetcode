# Description

:star2:

![](/images/112. Path Sum)

***
## Analysis
记得考研的时候，因为大一大二基本没有学习，对树是啥都没有什么大的概念，当时理解树是递归定义的，树的递归遍历，前中后序遍历，三句话就遍历完一棵树，什么鬼，想了好几天才想明白:disappointed_relieved:。现在研究生也考上了，也是研一下了， 发现再来做树的题目，还是会遇到很多障碍。:sob:。。这道题目的第一想法是采用先序遍历，当节点是叶子节点的时候，加上我们的判别因子。通过遍历然后对具体问题加判别因子，这应该算是解决树算法的一种模式了，，能改解决挺多树的问题的。

## Solution 先序遍历加判别因子

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 * 
 * 想法
 * 在遍历的过程中加上判别因子，判别因子的位置加在出现根节点的地方。
 * 采用先序遍历
 */
public class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;
        List<Integer> pathNum = new ArrayList<Integer>();
        List<Integer> finish = new ArrayList<Integer>();
        inorder(root, sum, pathNum, false, finish);
        return finish.size() != 0;
    }
    
public void inorder(TreeNode root, int sum, List<Integer> pathNum, boolean find, List<Integer> finish){
        if(find || root == null){
            return ;
        }
        pathNum.add(root.val);
        if(root.left == null && root.right == null){
            if(getSum(pathNum) == sum){
                System.out.println(pathNum);
                find = true;
                finish.add(1);
                return ;
            }
        }
        
        inorder(root.left, sum, pathNum, find, finish);
        inorder(root.right, sum, pathNum, find, finish);
        pathNum.remove(new Integer(root.val));
    }
    
    public int getSum(final List<Integer> pathNum){
        int sum = 0;
        for(int num : pathNum){
            sum += num;
        }
        return sum;
    }
}
```

## Improve
当进一步思考的时候，发现，这道题目确实可以转化为递归的问题，不同的子树对应不同的sum，这样问题就变得更加简单了

## Solution 递归求解
```java
public class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null) return false;
    
        if(root.left == null && root.right == null && sum - root.val == 0) return true;
    
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```
***
enjoy life, coding now! :D