# 024. Swap Nodes in Pairs

# Description

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4`, you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may **not** modify the values in the list, only nodes itself can be changed.

# Solution

这道题目本来想用链表最常规的做法来做的，就是设置各种指针，然后交换，做了一会发现实在是有点繁琐，最后看了Discuss，找到了个递归版本的，觉得非常的不错，也很好理解，直接拿过来了。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        //boundary condition
        if(head == null || head.next == null)
            return head;
        //normal condition
        ListNode next = head.next;
        head.next = swapPairs(head.next.next);
        next.next = head;
        return next;
    }
}
```



