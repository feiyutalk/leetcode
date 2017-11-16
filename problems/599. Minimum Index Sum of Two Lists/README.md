# 599. Minimum Index Sum of Two Lists

# Description

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their **common interest** with the **least list index sum**. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

**Example 1:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```

**Example 2:**

```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```

# Solution

题目做多了，就会知道，其实简单的题目的思路都是非常直接的解法， 什么叫直接，就是暴力求解，暴力求解在算法中的形式是什么，其实就是多重遍历，这道题一看用二重循环就可以直接求解。

```java
class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        //boudary condition
        if(list1 == null || list2 == null || list1.length == 0 || list2.length == 0) 
            return new String[0];
        //normal condition
        int min = Integer.MAX_VALUE;
        List<String> result = new ArrayList<>();
        for(int i=0; i<list1.length; i++){
            for(int j=0; j<list2.length; j++){
                if(list1[i].equals(list2[j])){
                    if(i + j < min){
                        min = i+j;
                        result.clear();
                        result.add(list1[i]);
                    }else if(i + j == min){
                        result.add(list1[i]);
                    }
                }
            }
        }
        return result.toArray(new String[result.size()]);
    }
}
```

