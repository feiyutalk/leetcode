659. Split Array into Consecutive Subsequences
==============================================

Description
-----------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Difficulty: Medium
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You are given an integer array sorted in ascending order (may contain
duplicates), you need to split them into several subsequences, where each
subsequences consist of at least 3 consecutive integers. Return whether you can
make such a split.

**Example 1:**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input: [1,2,3,3,4,5]
Output: True
Explanation:
You can split them into two consecutive subsequences : 
1, 2, 3
3, 4, 5
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Example 2:**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input: [1,2,3,3,4,4,5,5]
Output: True
Explanation:
You can split them into two consecutive subsequences : 
1, 2, 3, 4, 5
3, 4, 5
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Example 3:**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input: [1,2,3,4,4,5]
Output: False
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 

Solution1
---------

题目本身比较好懂，但是想把这道题目求解出来很是很有难度。

数据结构：我们需要两个HashMap，第一个HashMap我们记为freq，用来记录Input数组中元素出现的频度；第二个HashMap我们称为append，用来记录期望被拼接的元素及其个数（单纯这样来描述的话是比较难懂，必须结合例子和算法来演示，大家就清楚的了)
。

算法的主要思想：
首先，我们用到的遍历，我们需要两次遍历，第一次遍历，我们去求解Input数组中元素的频度；第二次遍历是算法的核心操作，对于遍历到的每个元素，我们做以下判断：

1.  （如果该元素频度不大于0，就直接返回）素是否是被期望拼接的元素（如果我们已经有了子串
    1 2
    3，如果遍历到的元素是4，那么该元素是被期望拼接的元素，我们通过append来记录被期望拼接的元素及其个数，当我们构建完1
    2 3之后，我们会进行append.put(4,1)）

2.  如果该元素不是期望被拼接的，那么意味着什么呢？这就意味该元素不能和前面的元素进行拼接，这个时候我们就需要去将该元素作为新的子串的起点，去构建新的子串。因为题目要求连续子串长度最少是3，所以我们会去判断i+1
    、i+2的频度是否是大于0，如果不是的话，就代表构建失败，返回false；否则的话，就构建子串，并进行append记录操作。第二次遍历结束，都需要把元素的频度减少1。

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ java
我们用Input[1,2,3,3,4,4,5,5]作为例子，演示代码的执行步骤
首先，第一次遍历，构造出两个HashMap: freq 和 append
    freq:{(1,1),(2,1),(3,2),(4,2),(5,2)}
    append:{}

其次，我们进行第二次遍历，核心部分 
1) 元素1
  判断出1不是期望被拼接的元素，所以我们希望构建新的子串[1,2,3]，又因为2,3的频度大于0，所以能够构建成功，那么我们需要修改freq，以及进行append操作。此时的数据结构的状态如下：
 freq{(1,0),(2,0),(3,1),(4,2),(5,2)}
 append{(4,1)}
 子串[1,2,3]
2) 元素2
  频度不大于0，直接continue
3) 元素3
  判断出3不是期望被拼接的元素，所以我们希望构建新的子串[3,4,5]，又因为4,5的频度大于0，所以能够构建成功，那么我们需要修改freq，以及进行append操作。此时的数据结构的状态如下：
 freq{(1,0),(2,0),(3,0),(4,1),(5,1)}
 append{(4,1),(6,1)}
 子串[1,2,3]、[3,4,5]
4) 元素4
  判断出4是期望被拼接的元素，所以我们进行拼接操作，那么我们需要修改freq，以及进行append操作。此时的数据结构的状态如下：
 freq{(1,0),(2,0),(3,0),(4,0),(5,1)}
 append{(4,0),(6,1),(5,1)}
 子串[1,2,3,4]、[3,4,5]
5) 元素5 
  判断出5是期望被拼接的元素，所以我们进行拼接操作，那么我们需要修改freq，以及进行append操作。此时的数据结构的状态如下： 
 freq{(1,0),(2,0),(3,0),(4,0),(5,0)}
 append{(4,0),(6,2),(5,0)}
 子串[1,2,3,4,5]、[3,4,5]

第二次循环顺利进行，意味着我们的整个算法是成功的，所以返回true。
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class Solution {
    public boolean isPossible(int[] nums) {
        HashMap<Integer, Integer> freq = new HashMap<>();
        HashMap<Integer, Integer> append = new HashMap<>();
        // first loop
        for(int num : nums)
            freq.put(num, freq.getOrDefault(num,0)+1);
        for(int num : nums){
            if(freq.get(num) == 0)
                continue;
            if(append.getOrDefault(num,0) > 0){
                // append ...
                append.put(num, append.get(num)-1);
                append.put(num+1, append.getOrDefault(num+1,0)+1);
            }else if(freq.getOrDefault(num+1,0)>0 && freq.getOrDefault(num+2,0)>0){ // create new subsequences with 3 integers.
                // create new subsequences ...
                freq.put(num+1, freq.get(num+1)-1);
                freq.put(num+2, freq.get(num+2)-1);
                append.put(num+3, append.getOrDefault(num+3,0)+1);
            }else{
                return false;
            }
            freq.put(num, freq.get(num)-1);
        }
        return true;
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**enjoy life, coding now! :D**
