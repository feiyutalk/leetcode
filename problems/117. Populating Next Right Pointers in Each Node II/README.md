# 117.  Populating Next Right Pointers in Each Node II

# Description

Follow up for problem "*Populating Next Right Pointers in Each Node*".

What if the given tree could be any binary tree? Would your previous solution still work?

**Note:**

- You may only use constant extra space.

For example,
Given the following binary tree,

```
         1
       /  \
      2    3
     / \    \
    4   5    7
```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```

# Solution

这道题目的需要操作的是每层上的节点，而且具有非常明显的层次特点，所以需要采用层次遍历，这里需要注意的是，在层次遍历的时候有一些题目是需要关注每一层具体有哪一些节点，有一些题目是不需要关注每一层具体有哪一些节点的。现在想想，按照需要关注每一层具体有哪一些节点的模板来写会更加通用，这套模板对于不需要关于每一层具体节点的题目也是适用的。

其实，把这个模板记住，这种题目就变得非常的容易了， 具体可以参考代码，也不是很难懂。

```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        //boudnary condition
        if(root == null)
            return;
        //normal condition
        Queue<TreeLinkNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0; i<size; i++){
                TreeLinkNode cur = queue.poll();
                //last node
                if(i != size - 1)
                    cur.next = queue.peek();
                else 
                    cur.next = null;
                if(cur.left != null)
                    queue.offer(cur.left);
                if(cur.right != null)
                    queue.offer(cur.right);
            }
        }
    }
}
```

