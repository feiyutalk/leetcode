# 369. Plus One Linked List

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
    public ListNode plusOne(ListNode head) {
        if(head == null) return null;
        // 1. reverse the linkedlist
        ListNode rhead = reverse(head);
        // 2. add
        int carry = 1;
        ListNode dummy = new ListNode(-1);
        dummy.next = rhead;
        ListNode pre = dummy;
        ListNode cur = rhead;
        while(carry != 0 && cur != null){
            carry = (cur.val + carry);
            cur.val = carry % 10;
            carry /= 10;
            cur = cur.next;
            pre = pre.next;
        }
        if(carry != 0){
            ListNode node = new ListNode(carry);
            node.next = pre.next;
            pre.next = node;
        }
        return reverse(dummy.next);
    }
    
    private ListNode reverse(ListNode head){
        /*
        1->2->3
        */
        ListNode dummy = new ListNode(-1);
        dummy.next = null;
        ListNode post = head.next;
        while(head != null){
            head.next = dummy.next;
            dummy.next = head;
            head = post;
            if(post != null)
                post = post.next;
        }
        return dummy.next;
    }
}
```

