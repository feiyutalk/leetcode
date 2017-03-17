# Description
:star2:

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.

Hint:

If there are 5 stones in the heap, could you figure out a way to remove the stones such that you will always be the winner?

## Analysis
这道题我是正难则反的思想，逆向的推导，也就是如果要拿到最后一个石头，第n-1,n-2,n-3个石头都不能拿，你会发现n √, n-1 ×, n-2 ×, n-3 ×, 打钩就是代表能赢，打叉代表不能赢，继续往前推，你会发现n-4必须拿到，如果n-4你没拿到，那么你就会拿到n-1, n-2, n-3其中一个，那如果你要拿到n-4那么你就不能拿n-5,n-6,n-7,也就是n-4√, n-5 ×, n-6 ×, n-7 ×。我们发现了模式出来了，√×××√×××...的模式一直往前面推进，现在的问题转化为，我第一个拿石头，那么我处在这个模式的什么位置呢？？？这就取决与n了，如果n%(4) == 0 也就是 n%(3+1) ==0 为什么是3+1，因为最多能拿3个石头，这个模式正好是3+1循环，如果抽象化一点，就是数学的周期函数，10001000....交替出现。回到对n的分析上，我们发现，如果n%(3+1) ==0 那么我们第一个拿必死无疑，如果n%(3+1)!=0,那么可能就是这种情况√×××√××,那么因为每次我们都会选择最佳策略，那么我们肯定会走到√的位置啦:yum:

## Solution
```java
public class Solution {
    public boolean canWinNim(int n) {
        if(n%(3+1) == 0)
            return false;
        else
            return true;
    }
}
```

***
enjoy life, coding now!:D.