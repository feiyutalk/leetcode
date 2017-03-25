#Description

:star2::star2:

![](/images/Kth_Smallest_Element_In_a_Sorted_Matrix.png)

***
##Analysis
感觉这道题目难度非常大，虽然用了二分的框架，但是里面的边界很难把握，很容易出错。

##Solution 负相关的二分求解

```java
public class Solution {
    public boolean guess(int g, int[][]matrix, int k){
        int length = matrix[0].length;
        int sum = 0;
        for(int i=0; i<length; i++){
            int low = 0;
            int high = length-1;
            int ans = -1;
            while(low<=high){
                int mid = (low+high)/2;
                if(matrix[i][mid] < g){
                    ans = mid;
                    low = mid + 1;
                }else{
                    high = mid - 1;
                }
            }
            sum += (ans + 1);
        }
        return k > sum;
    }
    
    public int kthSmallest(int[][] matrix, int k) {
        int length = matrix[0].length;
        int low = matrix[0][0];
        int high = matrix[length-1][length-1];
        int ans = low;
        while(low <= high){
            int mid = (int)(((long)low + high)/2);
            if(guess(mid,matrix,k)){
                ans = mid;
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return ans;
    }
}
```
***
enjoy life, coding now! :D now! :D           if(guess(mid, nums, m)){
                ans = (int)mid;
                high = mid;
            }else{
                low = mid + 1;
            }
        }
        return ans;
    }
}
```
***
enjoy life, coding now! :D now! :D