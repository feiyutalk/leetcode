# 142. Linked List Cycle II

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

我们也可以利用快慢指针的技巧来进行求解，快慢指针是说，我们用两个指针，一个是慢指针，每次走一步，一个是快指针，每次走两步，如果有环的话， 那么这两个指针最后会相遇，在第一次相遇之后，我们来分析，如何到达环的首个节点。

![](http://4.bp.blogspot.com/-syoC7y2yUq4/VpaQQ6OzRKI/AAAAAAAABQQ/RVqu1SDiDSI/s1600/3.png)

对这个图说明如下:

- 我们假设`p 和 q `$6$相遇，我们假设此时慢指针`q`走了$x$步，则快指针走了$2x$步。而，此时它们差了一环，所以可以得出，环的步数等于$x$。
- 上面的推导得到环的步数，等于慢指针`q`走的步数$x$，通过第二张图，我们假设$k = x-c$，设$c$是环起始点到相遇点的距离。我们发现q从原点走到起始点的距离等于$k$，p从相遇点走到起始点的距离也为$k$。利用这个性质，我们可以很快的写出该算法。

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
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            
            if(slow == fast){
                slow = head;
                while(slow != fast){
                    slow = slow.next;
                    fast = fast.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```

