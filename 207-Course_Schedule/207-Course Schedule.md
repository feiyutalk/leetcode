# 207. Course Schedule

## Description

```
Difficulty: Easy
Total Accepted:580.8K
Total Submissions:1.7M
Contributor: LeetCode
```

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a **pair**: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:

```
2, [[1,0]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

```
2, [[1,0],[0,1]]
```

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

***

## Solution1 三步走判断拓扑排序
  这是图论中比较经典的题目，判断图是否可以拓扑排序。虽然这是中等的题目，但是感觉还是相对来说比较简单，第一遍就已经AC了，解题的模式如下：

+ 定义节点的入度数组，遍历求解各节点的入度。
+ 定义零入度的队列，将节点初始状态下的零入度的节点入队，作为队列的启示状态。
+ 关键步骤，依次出队队列中的节点，找到其指向的节点，记为next，将next节点的入度减去1，此时判断next节点是否入度为0，如果是的话，入队。循环退出的条件就是队列为空。
+ 当循环退出时，我们判断我们的遍历次数是否与总节点一样，据此来判断是否可以拓扑排序。

```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        LinkedList<Integer> zeroIdg = new LinkedList<Integer>();
        int[] indegree = new int[numCourses];
        
        //count indegree
        for(int i=0; i<prerequisites.length; i++){
            indegree[prerequisites[i][0]]++;
        }
        
        //find zero indegree
        for(int i=0; i<indegree.length; i++){
            if(indegree[i] == 0)
                zeroIdg.offer(new Integer(i));
        }
        
        //loope
        while(!zeroIdg.isEmpty()){
            int course = zeroIdg.poll();
            numCourses--;
            for(int i=0; i<prerequisites.length; i++){
                if(prerequisites[i][1] == course){
                    int nextCourse = prerequisites[i][0];
                    indegree[prerequisites[i][0]]--;
                    if(indegree[prerequisites[i][0]] == 0)
                        zeroIdg.offer(prerequisites[i][0]);
                }
            }
        }
        
        //judge result according to numCourses
        if(numCourses>0){
            return false;
        }else{
            return true;
        }
    }
}
```

***

**enjoy life, coding now! :D**
