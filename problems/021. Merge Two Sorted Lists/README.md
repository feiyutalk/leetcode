# 21. Merge Two Sorted Lists

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null)
            return l2;
        if(l2 == null)
            return l1;
        ListNode dummy = new ListNode(-1);
        ListNode tail = dummy;
        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                ListNode cur = new ListNode(l1.val);
                cur.next = tail.next;
                tail.next = cur;
                tail = cur;
                l1 = l1.next;
            }else{
                ListNode cur = new ListNode(l2.val);
                cur.next = tail.next;
                tail.next = cur;
                tail = cur;
                l2 = l2.next;
            }
        }
        
        while(l1 != null){
            ListNode cur = new ListNode(l1.val);
            cur.next = tail.next;
            tail.next = cur;
            tail = cur;
            l1 = l1.next;
        }
        
        while(l2 != null){
            ListNode cur = new ListNode(l2.val);
            cur.next = tail.next;
            tail.next = cur;
            tail = cur;
            l2 = l2.next;
        }
        return dummy.next;
    }
}
```

