# 2. Add Two Numbers

## #1 合并链表[AC]
### 思路

这是链表相加的问题，两个链表相加本身是一个简单的问题，但是，这题进行了扩展，就是相加的过程要考虑进位的问题，但是相加最多进位1，所以问题也不是那么难，只要在相加的时候把进位值加上，然后记得算下一次相加的进位就可以了，当然，常见的细节，比如链表为空之类的点，还是要想清楚的，这个做多了就有感觉了，不是什么难点，相对来说，本题虽然是中级题目，但是我觉得算是中级里面比较简单的题目了。

### 算法

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

### 复杂度分析：

- 时间复杂度：$O(m)$
- 空间复杂度：$O(m)$，这个复杂度可以不需要，借用输入链表作为存储空间，但是程序写起来会稍微麻烦一点。