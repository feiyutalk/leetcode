# 160. Intersection of Two Linked Lists

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;
        int lengthA = getLength(headA);
        int lengthB = getLength(headB);
        if(lengthA > lengthB){
            int diff = lengthA - lengthB;
            while(diff != 0){
                headA = headA.next;
                diff--;
            }
            while(headA != headB){
                headA = headA.next;
                headB = headB.next;
            }
            return headA;
        }else{
            int diff = lengthB - lengthA;
            while(diff != 0){
                headB = headB.next;
                diff--;
            }
            while(headA != headB){
                headA = headA.next;
                headB = headB.next;
            }
            return headA;
        }
    }
    
    private int getLength(ListNode head){
        int count = 0;
        while(head != null){
            count++;
            head = head.next;
        }
        return count;
    }
}
```

