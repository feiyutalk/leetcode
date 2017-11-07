# 142. Linked List Cycle II

# Solution

抓住问题的主要矛盾往往是求解问题的最关键的点，如果抓住了问题的本质，那么即便不能很快想出来，但是思考的角度和方向至少是对的。那么这道题目的主要矛盾点在哪呢？问题要求解圈的起始节点，这个节点有什么特别的呢？特别之处在链表中，圈的起始点也是圈的终点，这意味着对链表进行遍历的时候，它会被遍历两次，所以，而满足唯一性条件的数据结构是集合！所以可以通过集合来保存遍历过的节点。

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
    public ListNode detectCycle(ListNode head) {
        //boundary condition
        if(head == null || head.next == null)
            return null;
        //normal condition
        Set<ListNode> set = new HashSet<>();
        ListNode cur = head;
        while(cur != null){
            if(set.contains(cur))
                return cur;
            else{
                set.add(cur);
                cur = cur.next;
            }
        }
        return null;
    }
}
```

