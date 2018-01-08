# 61. Rotate List

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
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || head.next == null) return head;
        int length = getLength(head);
        k = k % length;
        if(k == 0) return head;
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode cur = head;
        int count = length - k;
        while(count != 0){
            pre = pre.next;
            cur = cur.next;
            count--;
        }
        // rotate
        // 1. find the last node
        ListNode last = cur;
        while(last.next != null){
            last = last.next;
        }
        pre.next = last.next;
        last.next = dummy.next;
        dummy.next = cur;
        return dummy.next;
    }
    
    private int getLength(ListNode cur){
        int length = 0;
        while(cur != null){
            length++;
            cur = cur.next;
        }
        return length;
    }
    
}
```

