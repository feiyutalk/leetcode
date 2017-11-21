# 234. Palindrome Linked List

判断链表是否对称，首先，我们需要构造出逆置链表，然后用指针前向法来判断两个链表元素值完全一样。

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
    public boolean isPalindrome(ListNode head) {
        if(head == null)
            return true;
        if(head.next == null)
            return true;
        ListNode cur = head;
        ListNode dummy2 = new ListNode(-1);
        while(cur != null){
            ListNode temp = new ListNode(cur.val);
            temp.next = dummy2.next;
            dummy2.next = temp;
            cur = cur.next;
        }
        cur = head;
        ListNode cur2 = dummy2.next;
        while(cur != null){
            if(cur.val != cur2.val) return false;
            cur = cur.next;
            cur2 = cur2.next;
        }
        return true;
    }
}
```

