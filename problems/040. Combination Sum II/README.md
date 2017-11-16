# 040. Combination Sum II

# Solution

这道题目属于排列组合中递归回溯枚举法的题型，之前已经总结好了整个的算法模板，但是，这道题目涉及到元素有重复的问题，这个时候我们就就需要对元素进行去重复;

假设输入的序列为`[10, 1, 1, 7, 6, 1, 5]`，对其进行排序之后，会得到`[1,1,1,5,6,7,10]`，然后我们进行递归回溯枚举，会得到如下的分支:

```
step1 step2 ...
  1		1
     \
  1		1
	 \	   \
  1		1
		   \
  5		5

  6		6

  7		7

  10	10
```

我们发现由于序列中有三个1，记为$1_1$, $1_2$, $1_3$这时候[$1_1$, 7]、[$1_2$,7]和[$1_3,7$]都是满足条件的，即它们的和都等于target=8，但是这三种答案是重复的。所以，我们需要做的是在同一列循环中，去除重复，因为我们已经将数组进行排序，所以，相同值的元素会相邻，我们根据条件`i>0 && candidates[i] == candidates[i-1]`来去除同一列循环中的重复元素。

但是这个条件作用于所有的列循环时，会出现问题，因为上面的条件使得，我们第二列也无法取到1，因为第二列循环，只能从第二个1开始遍历，肯定满足`i>0 && candidates[i] == candidates[i-1]`这个条件，所以无法取得1，所以，我们仍需要对上述条件加一个限制，使它对不同列起不到效果。这个地方可能不太好想，我这边举一个例子：

假设此时第一列循环取到$1_1$，那么第二列循环可以取$1_2$，但是不可以取$1_3$，这有一个条件，就是如果有重复元素，则第n列循环的重复元素只能取紧挨着第n-1列循环取到的重复元素之后的那个重复元素。就比如上述的第一列取到$1_1$，则第二列只能去$1_2$，所以，我们修改上述的条件，将其限制在当不同列重复元素想取的值不是紧挨着上一列的重复元素时。

最后的去重复条件变成了:

```java
if(i>0 && candidates[i] == candidates[i-1] && i>step) 	   continue;
```

```java
class Solution {
    private List<List<Integer>> result = new ArrayList<List<Integer>>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        if(candidates == null || candidates.length == 0) return new ArrayList<List<Integer>>();
        Arrays.sort(candidates);
        backtrack(candidates, target, 0, new ArrayList<Integer>());
        return result;
    }
    
    private void backtrack(int[] candidates, int target, int step, List<Integer> temp){
        if(target == 0){
            result.add(new ArrayList<Integer>(temp));
        }else if(target > 0){
            for(int i=step; i<candidates.length; i++){
                if(candidates[i] > target) break;
                if(i>0 && candidates[i] == candidates[i-1] && i>step) continue;
                temp.add(candidates[i]);
                backtrack(candidates, target-candidates[i], i+1, temp);
                temp.remove(temp.size()-1);
            }   
        }
    }
}
```