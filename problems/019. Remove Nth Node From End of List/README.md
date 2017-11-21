# 019. Remove Nth Node From End of List

也是采用向前指针法，找到指定的位置后，将该元素删除即可。链表题目中有四大指针，控制好这四大指针，一般题目都能够很快的求解出来:

```java
ListNode dummy = new ListNode(-1);
ListNode pre = dummy;
ListNode cur = dummy.next;
ListNode next = cur.next;
```

主要要控制好`cur`和`pre`这两个指针。