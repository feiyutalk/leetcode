# 563. Binary Tree Tilt

# Description

Given a binary tree, return the tilt of the **whole tree**.

The tilt of a **tree node** is defined as the **absolute difference** between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.

The tilt of the **whole tree** is defined as the sum of all nodes' tilt.

```
Input: 
         1
       /   \
      2     3
Output: 1
Explanation: 
Tilt of node 2 : 0
Tilt of node 3 : 0
Tilt of node 1 : |2-3| = 1
Tilt of binary tree : 0 + 0 + 1 = 1
```

# Solution

这道题目，是关于树的题目，树这种数据结构的特点在于它是递归定义的，它是对带有层次性的数据结构的抽象。所以，关于树的题目有很多都是递归求解的。怎么说呢？因为我们遍历树中每个节点的时候最常用的也是递归遍历，在遍历每个结点的时候会加上对应的操作因子，不同的题目可能会对应不同的操作因子，那么对于这道题目，是否也符合这种模式呢?

我想也是符合的，要求解这道题目，我们应该回答以下问题，或者更一般的说，要回答关于树遍历+操作因子的题目，我们应该回答以下问题：

1. 采用何种遍历方式？先序、中序、后序。
2. 递归的停止条件是什么？最常见的是 node == null
3. 递归的返回值是什么？就是说当递归返回的时候，需要向调用函数返回什么？
4. 操作因子是什么？即，遍历到树中的每个结点的时候，我们需要做什么操作。

结合这道题目，我们来一一回答这些题目:

1. 应该采用什么遍历顺序呢？对于这道题目，每个结点，我们需要计算 

   abs(sum(left_subtree) - sum(right_subtree))，所以我们需要先知道左子树元素和以及右子树元素和，所以我们应该用后序遍历。

2. 有了上面的分析，我们也可以回答第4个问题，操作因子是什么，在这里操作因子就是，计算sum(left_subtree) - sum(right_subtree)，并将这一结果累加到一个变量中。

3. 当然了，对于第3个问题我们也可以回答了，我们的应该向调用函数返回的是什么呢，因为调用函数要进行的操作是sum(left_subtree) - sum(right_subtree)，所以我们应该向调用函数返回，sum(subtree)。

4. 最后，递归的停止条件就是当结点为null。

好了，顺着这个思路，我们的代码如下:

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
    int result;
    public int findTilt(TreeNode root) {
        tilt(root);
        return result;
    }
    
    private int tilt(TreeNode root){
        if(root == null)
            return 0;
        int left = tilt(root.left);
        int right = tilt(root.right);
        int sum = Math.abs(left - right);
        result+=sum;
        return left + right + root.val;
    }
}
```

