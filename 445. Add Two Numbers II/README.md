# 445. Add Two Numbers II

# Solution

这道题目本质上还是做链表合并的问题，链表做的题目也不少了，常见的问题就是链表的拆分，链表的合并，链表的排序等等。涉及的操作无非就是头插法，尾插法，遍历链表。

在做此类题目的时候，可以考虑先画出示意图，特别是对pre、cur、next三种指针的操作。

这道题目是链表合并的问题， 它加了算数运算这种背景，也就是我们在合并的时候需要用算数相加的角度去做合并，需要考虑进位。这道题目又绕了点弯子，将表达式逆序了，所以在求解时先转化为已经做过的题目，就是将输入逆序，最后再将结果逆序，就可以了。

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        //boundary condition
        if(l1 == null)
            return l2;
        if(l2 == null)
            return l1;
        //normal condition
        l1 = reverse(l1);
        l2 = reverse(l2);
        
        ListNode result = new ListNode(0);
        ListNode tail = result;
        int carry = 0;
        while(l1!=null || l2!=null){
            int val = ((l1==null?0:l1.val) + (l2==null?0:l2.val) + carry)%10;
            carry = ((l1==null?0:l1.val) + (l2==null?0:l2.val) + carry)/10;
            
            ListNode cur = new ListNode(val);
            tail.next = cur;
            tail = tail.next;
            //go to next
            if(l1 != null)
                l1 = l1.next;
            if(l2 != null)
                l2 = l2.next;
        }
        
        if(carry != 0){
            ListNode last = new ListNode(carry);
            tail.next = last;
            tail = tail.next;
        }
        
        return reverse(result.next);
    }
    
    private ListNode reverse(ListNode l){
        ListNode dump = new ListNode(0);
        dump.next = null;
        ListNode next = l.next;
        while(l!=null){
            l.next = dump.next;
            dump.next = l;
            //go to next 
            l = next;
            if(next != null)
                next = next.next;
        }
        return dump.next;
    }
}
```

