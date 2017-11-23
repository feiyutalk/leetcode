# 141. Linked List Cycle

这个题目需要判断链表中是否有环，可以设置两个指针，一个是快指针，一个是慢指针，快指针每次走两步，慢指针每次走一步。如果最后两个指针相遇了，就代表有环。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast)
                return true;
        }
        return false;
    }
}
```

