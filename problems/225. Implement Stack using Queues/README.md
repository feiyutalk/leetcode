# 225. Implement Stack using Queues

# Solution

这道题属于设计数据结构的题目，此类题目目前见过就只有一种模式，组合多种数据结构完成特殊的操作。这里要通过队列来实现栈操作，我们可以怎么做呢？

直接看代码吧，两个队列来回折腾，哈哈。

```java
class MyStack {
    private Queue<Integer> q1;
    private Queue<Integer> q2;
    /** Initialize your data structure here. */
    public MyStack() {
        q1 = new LinkedList<Integer>();
        q2 = new LinkedList<Integer>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        if(q1.isEmpty()){
            q1.add(x);
            for(int i=0; i<q2.size(); i++){
                q1.add(q2.poll());
            }
        }else{
            q2.add(x);
            for(int i=0; i<q1.size(); i++){
                q2.add(q1.poll());
            }
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        if(!q1.isEmpty()){
            return q1.poll();
        }else{
            return q2.poll();
        }
    }
    
    /** Get the top element. */
    public int top() {
        if(!q1.isEmpty()){
            return q1.peek();
        }else{
            return q2.peek();
        }
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty() && q2.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

