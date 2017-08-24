# 374. Guess Number Higher or Lower
## Description

```
Difficulty: Easy
```
We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.

You call a pre-defined API guess(int num) which returns 3 possible results (-1, 1, or 0):

	-1 : My number is lower
	 1 : My number is higher
	 0 : Congrats! You got it!

**Example:**

	n = 10, I pick 6.
	
	Return 6.
## Solution 1 二分查找
 
 ```java
 
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    private int result = 1;
    public int guessNumber(int n) {
	binarySearch(1,n);
	return result;
    }

    public void binarySearch(int low, int high){
	int mid = low + (high - low)/2;
	if(guess(mid) == 0){
	    result = mid;
	}else if(guess(mid) == 1){
	    low = mid + 1;
	    binarySearch(low, high);
	}else{
	    high = mid;
	    binarySearch(low, high);
	}
    }
}
```

***

**enjoy life, coding now! :D**
