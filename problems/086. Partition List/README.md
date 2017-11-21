# 086. Partition List

属于指针问题的向前型，指针向前移动，判断每个节点的值，如果是小于x就保留，如果是大于等于x，就将其添加到另外一个链表中，最后合并两个链表。

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
    public ListNode partition(ListNode head, int x) {
        if(head == null || head.next == null) return head;
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode greater = new ListNode(-1);
        ListNode rear = greater;
        while(head != null){
            if(head.val < x){
                pre = pre.next;
                head = head.next;
            }else{
                pre.next = head.next;
                head.next = rear.next;
                rear.next = head;
                rear = rear.next;
                head = pre.next;
            }
        }
        pre.next = greater.next;
        return dummy.next;
    }
}
```

