# 083.  Remove Duplicates from Sorted List 

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
        ListNode cur = head;
        ListNode post = cur.next;
        while(post != null){
            while(cur.val == post.val){
                cur.next = post.next;
                post = cur.next;
                if(post == null)
                    break;
            }
            cur = cur.next;
            if(post != null)
                post = post.next;
        }
        return head;
    }
}
```

