# 082.  Remove Duplicates from Sorted List II

这是关于链表的题目，链表题目的特点就是需要多个指针来存储链表变换时，各个节点直接的关系，一般包含如下节点:

- dump 用于指向第一个节点，LeetCode上的head节点一般指第一个节点，我们这里用dump作为“头节点”。该节点主要用于，在操作完链表后，可以通过该dump节点返回结果，即`return dump.next()`
- pre 节点，用于保存操作节点的前驱
- cur 节点， 用于保存当前操作的节点
- next节点，用于保存操作节点的后继

有了，这几个指针，然后画一个草图，该操作后，指针的变换关系搞清楚，一般就不会出问题了。

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
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode dump = new ListNode(-1);
        dump.next = head;
        ListNode pre = dump;
        ListNode cur = head;
        ListNode next = head.next;
        while(next != null){
            boolean duplicated = false;
            while(cur.val == next.val){
                duplicated = true;
                next = next.next;
                if(next == null){//end
                    pre.next = null;
                    return dump.next;
                }
            }
            if(duplicated){
                pre.next = next;
            }else{
                pre = pre.next;
            }
            cur = next; 
            next = next.next;
        }
        return dump.next;
    }
}
```



