# 297.Serialize and Deserialize Binary Tree

# Description

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree

```
    1
   / \
  2   3
     / \
    4   5
```

as  "[1,2,3,null,null,4,5]" , just the same as  how LeetCode OJ serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

# Solution

序列化和反序列在平时写稍微大点的项目的时候还是经常遇到的，特别是在对象持久化，网络传输的时候经常会考虑对象的序列化和反序列化。大部分的语言中已经集成了Serials和Deserials的方法，所以，平时也没怎么考虑过序列化和反序列化的算法，今天这道题目做起来还是比较费劲的，参考着答案写的。

整个的思路在于，序列化过程将树变成String，而反序列化过程将String变成树。这边用到还是递归的算法，在树里面也是比较常见的，记得在树的递归中，要回答的问题是，采用的什么方式递归遍历？这里比较容易想到的是采用先序遍历，也就是先将根结点值保存在String中，然后序列化左子树，最后序列化右子树。递归的停止条件是什么？在树递归里，90%都是node == null的时候返回。递归的返回值是什么？在序列化过程中，递归的返回值可以存放到全局变量中，无需向调用函数返回具体值，在反序列化过程中，递归的返回值是构造出来的子树。递归遍历过程中，对于每个遍历到的结点，操作因子是什么？在序列化过程中，操作因子就是将结点的值，保存在String中，在反序列化过程中，操作因子就是读取String中的值，构造出一个节点出来。

实际上，我们可能还漏掉一个递归需要考虑的问题，调用函数需要向递归被调用函数传递什么呢？在序列化过程时，可以传递存放结果字符串的参数；在反序列化过程中，需要传递序列化后的String。

所以，再次总结一下，关于树递归问题，需要考虑的5个点:

1. 采用哪种递归方式遍历？先序，中序，后序；
2. 递归停止条件是什么？一般情况下都是 node == null；
3. 递归过程中，调用函数需要向被调用函数，传递什么？有时候，我们需要将结果参数，在没一轮递归过程中传递，以将每一轮的结果保存到结果参数中。对应的是递归函数的输入参数。
4. 递归过程中，当遍历到每个结点的时候，执行的操作因子是什么？
5. 递归过程中，被调用函数，需要向调用函数返回什么？  对应的是return 返回值。

说起来有点抽象，如果还是不懂的话，youtube上这道题目的讲解，也可以听一听，在回头来看这里的解答:

- [Youtube题目讲解](https://www.youtube.com/watch?v=JL4OjKV_pGE)

最后，来看一下代码吧:

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuffer sb = new StringBuffer();
        doSerialize(root, sb);
        return sb.toString();
    }
    
    private void doSerialize(TreeNode root, StringBuffer sb){
        if(root == null){
            sb.append("#").append(" ");
            return;
        }
        sb.append(root.val).append(" ");
        doSerialize(root.left, sb);
        doSerialize(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Queue<String> nodes = new LinkedList();
        nodes.addAll(Arrays.asList(data.split(" ")));
        return doDeserialize(nodes);
    }
    
    private TreeNode doDeserialize(Queue<String> data){
        String val = data.remove();
        if(val.equals("#")){
            return null;
        }else{
            TreeNode node = new TreeNode(Integer.valueOf(val));
            node.left = doDeserialize(data);
            node.right = doDeserialize(data);
            return node;
        }
        
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

