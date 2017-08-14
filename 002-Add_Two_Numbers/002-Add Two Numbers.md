# 2. Add Two Numbers

## Description

```
Difficulty: Medium
Total Accepted:326.8K
Total Submissions:1.2M
Contributor: LeetCode
```

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Expample:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```

***

## Solution1
  这是链表相加的问题，两个链表相加本身是一个简单的问题，但是，这题进行了扩展，就是相加的过程要考虑进位的问题，但是相加最多进位1，所以问题也不是那么难，只要在相加的时候把进位值加上，然后记得算下一次相加的进位就可以了，当然，常见的细节，比如链表为空之类的点，还是要想清楚的，这个做多了就有感觉了，不是什么难点，相对来说，本题虽然是中级题目，但是我觉得算是中级里面比较简单的题目了。还有，用Java写链表好不习惯，怀念考研那会用C指针写链表的情景......

```java
/**
  Definition for singly-linked list.
  public class ListNode {
      int val;
     ListNode next;
     ListNode(int x) { val = x; }
  }
*/
public class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int count = 0;
        int value;
        ListNode ori = new ListNode(-1);
        ListNode result = new ListNode(-1);
        ori = result;
        while(l1!=null||l2!=null){
            value = (count + (l1==null?0:l1.val) + (l2==null?0:l2.val)) % 10;
            count = (count + (l1==null?0:l1.val) + (l2==null?0:l2.val)) / 10;
            result.next = new ListNode(value);
            result = result.next;
            if(l1 != null)
                l1 = l1.next;
            if(l2 != null)
                l2 = l2.next;
        }
        if(count == 1){
            result.next = new ListNode(count);
            result = result.next;
        }
        return ori.next;
    }
}
```

最后看一下结果，不好不坏吧，想不到优化的空间了：

![](/002-Add_Two_Numbers/Add_Two_Numbers/result.png)

***

**enjoy life, coding now! :D**

