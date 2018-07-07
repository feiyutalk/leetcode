# 582. Kill Process

## #1 深度优先遍历[TLE]

### 思路

递归的删除所有的子进程，深度优先遍历。

### 算法

```java
class Solution {
    public List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
        List<Integer> res = new ArrayList<>();
        if(kill == 0)
            return res;
        res.add(kill);
        for(int i=0; i<ppid.size(); i++){
            if(ppid.get(i) == kill){
                res.addAll(killProcess(pid, ppid, pid.get(i)));
            }
        }
        return res;
    }
}
```

### 复杂性分析

## #2 队列[TLE]

### 思路

通过队列来保存每次要删除的进程号，我们知道，每次要删除一个进程时，需要递归的删除其子进程。

### 算法

```java
class Solution {
    public List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
        if(pid == null || pid.size() == 0 || ppid == null || ppid.size() == 0)
            return new ArrayList<Integer>();
        List<Integer> res = new ArrayList<>();
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(kill);
        while(!queue.isEmpty()){
            int curKill = queue.poll();
            res.add(curKill);
            // 找到它的孩子节点，添加进去
            for(int i=0; i<ppid.size(); i++){
                if(ppid.get(i) == curKill){
                    queue.offer(pid.get(i));
                }
            }
        }
        return res;
    }
}
```

### 复杂度分析

- 时间复杂度
- 空间复杂度

## #3 提前构建数据结构，优化遍历

### 思路

在上一种做法中，我们用队列的方式来依次的、层级的删除每个进程，在该算法中，对于每个父进程，我们都需要遍历一遍来寻找到其所有的子进程，我们可以提前构建这种数据结构，来优化这部分时间开销。

### 算法

```java
class Solution {
    public List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
        if(pid == null || pid.size() == 0 || ppid == null || ppid.size() == 0)
            return new ArrayList<Integer>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        for(int i=0; i<ppid.size(); i++){
            if(ppid.get(i) == 0)
                continue;
            if(!map.containsKey(ppid.get(i))){
                List<Integer> temp = new ArrayList<>();
                temp.add(pid.get(i));
                map.put(ppid.get(i), temp);
            }else{
                map.get(ppid.get(i)).add(pid.get(i));
            }
        }
        List<Integer> res = new ArrayList<>();
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(kill);
        while(!queue.isEmpty()){
            int curKill = queue.poll();
            res.add(curKill);
            // 找到它的孩子节点，添加进去
            if(!map.containsKey(curKill))
                continue;
            for(int child : map.get(curKill))
                queue.offer(child);
        }
        return res;
    }
}
```

### 复杂性分析

- 时间复杂度
- 空间复杂度

### 