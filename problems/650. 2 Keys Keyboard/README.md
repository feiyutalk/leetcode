# 650. 2 Keys Keyboard
## Description

```
Difficulty: Medium
```

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

1. Copy All: You can copy all the characters present on the notepad (partial copy is not allowed).
2. Paste: You can paste the characters which are copied last time.

Given a number n. You have to get exactly n 'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get n 'A'.

**Example 1:**

```

Input: 3
Output: 3
Explanation:
Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.

```
## Solution 1 BFS
  题目要求的操作步数要最少，那么我们怎么样的一个操作序列才能保证步数最少？需要考虑的情况非常多，这时候我们需要对我们的问题进行建模或者说是抽象，抽象的角度应该是往前人总结好的一些非常常见的数据结构或者算法模型上进行。其实上，这道题可以抽象成一个图的模型。题目涉及到的问题可以看成是状态节点之间的转化问题，我们从初始状态开始进行转化，每一步的转化呢，我们有两种路径，所对应的可能会连接到两个不同的状态节点上，以此类推，就可以构成我们整个图。状态节点可以由当前的字符长度curLen和粘贴板上的字符长度构成clipLen。

  抽象成图模型之后，原问题就会转化成，从初始节点到某个指定节点的最小路径。那这个问题实际上我们在图模型的学习中已经非常熟悉了，我们可以采用广度优先遍历的方式去求解。
	
![graphModel](./images/status_graph_model.png)

```java

// neuclil
class Solution {
    class Status{
        int curLen;
        int clipLen;
        public Status(int a, int b){
            this.curLen = a;
            this.clipLen = b;
        }
    }
    
    public int minSteps(int n) {
        if(n == 1)
            return 0;
        //1. initialize
        Queue<Status> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();
        int step = 1;
        queue.offer(new Status(1,1));
        visited.add("1,1");
        
        //2. while
        while(!queue.isEmpty()){
            // 2.1 level++
            step++;
            // 2.2 visit node in same level
            int size = queue.size();
            for(int i=0; i<size; i++){
                Status s = queue.poll();
                //copy all
                if(!visited.contains(s.curLen+","+s.curLen)){
                    queue.add(new Status(s.curLen, s.curLen));
                    visited.add(s.curLen+","+s.curLen);
                }
                
                //paste
                if(s.curLen + s.clipLen == n)
                    return step;
                if(!visited.contains((s.curLen+s.clipLen)+","+s.clipLen) && s.curLen + s.clipLen < n){
                    queue.add(new Status(s.curLen+s.clipLen, s.clipLen));
                    visited.add((s.curLen+s.clipLen)+","+s.clipLen);
                }
            }
        }
        return -1;
    }
}

```

***

**enjoy life, coding now! :D**
