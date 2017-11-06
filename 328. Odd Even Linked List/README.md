# 328. Odd Even Linked List

# Description

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example:**
Given `1->2->3->4->5->NULL`,
return `1->3->5->2->4->NULL`.

**Note:**
The relative order inside both the even and odd groups should remain as it was in the input. 
The first node is considered odd, the second node even and so on ...

**Credits:**
Special thanks to [@DjangoUnchained](https://leetcode.com/discuss/user/DjangoUnchained) for adding this problem and creating all test cases.

# Solution

关于这道题目，是链表中经典的链表节点归类的问题，通常的做法就是设置类标头节点，然后遍历原始链表，并将不同的节点归类到不同的类标链表中。

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
    public ListNode oddEvenList(ListNode head) {
        //boundary condition
        if(head == null || head.next == null){
            return head;
        }
        //normal condition
        ListNode odds = new ListNode(-1);
        ListNode oddLast = odds;
        ListNode evens = new ListNode(0);
        ListNode evenLast = evens;
        
        ListNode cur = head;
        boolean isOddNum = true;
        while(cur!=null){
            ListNode next = cur.next;
            if(isOddNum){
                oddLast.next = cur;
                cur.next = null;
                oddLast = cur;
            }else{
                evenLast.next = cur;
                cur.next = null;
                evenLast = cur;
            }
            isOddNum = !isOddNum;
            cur = next;
        }
        //merge
        oddLast.next = evens.next;
        return odds.next;
    }
}
```

