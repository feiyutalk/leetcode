# 078. Subsets

# Description

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

For example,
If **nums** = `[1,2,3]`, a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# Solution

这个问题是求解所有子集的问题，在数学的集合问题里面经常出现需要求解幂集、排列数、组合数这一类的问题，这类问题有什么特点？很大的一个特点就是对给定的各位数进行枚举，而且每个数只能用一次。有些情况下需要考虑顺序性，如排列，有些情况不需要考虑顺序性，如组合，求幂集，这里在Leetcode讨论区看到了此类问题的通用解法，在这里总结一下。

## SubSets

这里Leetcode分别给出了求幂集的两种情况，第一种情况是没有重复元素的，第二种情况是有重复元素的，我们可以通过一个框架算法来处理这两个问题，先看一眼这两种解法:

Subsets : https://leetcode.com/problems/subsets/

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list , List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```

Subsets II (contains duplicates) : https://leetcode.com/problems/subsets-ii/

```java
public List<List<Integer>> subsetsWithDup(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        if(i > start && nums[i] == nums[i-1]) continue; // skip duplicates
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
} 
```

整个算法的思想是什么，我们来分析一下：

算法应该是模拟人出处理问题的一个过程，这个过程可以通过严格的步骤进行，这个步骤转化为程序就成了算法，当然在大量的算法中，我们可以总结，归纳出一定的算法思想或者模式，我们对此模式进行总结以便于下次遇到同样的算法时候能够快速的应该该模式进行求解。算法思想一般有分而治之，递归回溯，贪心，动态规划等。这里我们要用的是递归回溯，递归和回溯分别是什么，其实上递归讲的就是函数调用自身，但是很多时候我们过多的强调的递归，却忽视了回溯，回溯指的是递归调用返回。做递归回溯的题目的时候，指需要做好两件事就可以：

1. 递归调用的时候需要做什么，需要传递什么参数，需要把当前步骤的什么状态带给下一个递归过程，以及递归的出口是什么。
2. 当递归调用返回的时候需要做什么。

我们以这道题目为例做说明，首先，在算幂集的时候我们可以采用如下的方式来枚举：

假设 nums = [1, 2, 3]

- 从左往右，先考虑第一位，再考虑第二位，然后是最后一位。
- 当第一位取 1 的时候，第二位只能取 2 或 3 ，当第二位取 2 的时候，第三位只能取3。当第二位取3的时候，第三为只能取2。

在上述的步骤中，我们可以看到递归的过程，是什么？

我们在取完第一位的时候，递归的调用backtack()这个函数，状态变成了什么？首先temp里面包含了第一位的取值，其次，start的值加1。

所以backtrack()里面的for()循环是每一位对不同取值的枚举。在for()循环里面我们进行的递归，就是在当前位取值后递归的调用backtrack()对下一位进行取值，我们可以看到此时tempList和start这两个状态都发生了改变。那么递归的结束是什么呢？递归的结束就是循环结束了。

另外，来看一下回溯的处理。我们在上面的讨论中发现，当第一位取1，第二位是可以取2或者3的，由递归的过程可以知道，当第二位取2的时候，会递归的去取第三位。那么当递归的取第三位返回的时候，我们需要做什么？当第三位返回的时候意味着(1, 2, 3)序列已经取了，这时候我们就需要第二位不取2，而取3，然后再做递归调用第三位的取值。所以我们需要把之前取的2删掉，然后再进行下一轮循环，也就是取下一个值。

对于有重复元素的集合，我们一开始做的排序操作就很重要了，因为它可以让我们很方便的判断重复元素，然后跳过它。重复元素主要在相同位出现的时候不允许，所以是在for循环的时候判断重复然后跳过就可以了。

## Permutations

排列数的求解，排列数的求解和之前求幂集有什么不同呢？

在求解幂集中:

(1,2,3) 和(1,3,2)是一样的，我们通过start这个状态的控制。这个状态信息保证了不会出现上述的情况。

在求解排列数的时候，就不能需要start这个状态了，但是，我们需要判断之前的元素时候出现过，如果出现了，我们就不能往里添加了。所以现在我们只需要temList这个状态信息就可以了。

```java
public List<List<Integer>> permute(int[] nums) {
   List<List<Integer>> list = new ArrayList<>();
   // Arrays.sort(nums); // not necessary
   backtrack(list, new ArrayList<>(), nums);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums){
   if(tempList.size() == nums.length){
      list.add(new ArrayList<>(tempList));
   } else{
      for(int i = 0; i < nums.length; i++){ 
         if(tempList.contains(nums[i])) continue; // element already exists, skip
         tempList.add(nums[i]);
         backtrack(list, tempList, nums);
         tempList.remove(tempList.size() - 1);
      }
   }
} 
```

可以看出来，这个算法框架运用递归和回溯的方式来求幂集、排列、组合这种枚举问题还是非常好用的，现在我们来考虑一下如果数组中有重复元素该如何处理。这时候对于重复元素我们分类讨论：

- 重复元素在不同位置，这个时候，我们只要判断用的不是同一位置的数值就可以了，就比如数组是1 1 2，当第一位用第一个1的时候，第二位就不可以用第一个1，而可以用第二个1。
- 重复元素在同一位置，这个时候如果上一次已经用该重复元素枚举过了，我们就应该跳过这种情况。

下面看一下具体的代码实现:

```java
public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, new boolean[nums.length]);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, boolean [] used){
    if(tempList.size() == nums.length){
        list.add(new ArrayList<>(tempList));
    } else{
        for(int i = 0; i < nums.length; i++){
            if(used[i] || i > 0 && nums[i] == nums[i-1] && !used[i - 1]) continue;
            used[i] = true; 
            tempList.add(nums[i]);
            backtrack(list, tempList, nums, used);
            used[i] = false; 
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

注意在for()循环里面的if()判断条件，它把两种可能的情况都给加上了，第一种情况就是在不同的位置，判断重复元素是否已经使用过了；第二种情况就是在相同位置，判断重复元素时候已经使用过了。

