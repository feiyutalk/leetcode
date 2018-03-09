# 221. Maximal Square
## #1 动态规划[AC]
  这道题目需要采用动态规划的方法来求解，动态规划最难的在于如何建立状态转化函数！这里需要注意的是，状态转换函数的**状态**怎么表示，用什么表示！

  这里往往需要一定的技巧，抓住一个点来表示我们问题的解！在这道题目中，就需要建立一个结果数组（是会随着状态转化函数的变化而变得更加的健全）。数组中的每个值，保存的是以该cell作为最右下角的元素构建正方形所能构建的最大的正方形的边长。有了这个对状态的定义，我们就能够很好的建立我们的状态转移函数了~

```java

public class Solution {
    public int maximalSquare(char[][] matrix) {
	if(matrix == null || matrix.length == 0)
	    return 0;

	int result = 0;
	int[][] count = new int[matrix.length][matrix[0].length];

	//initialize the status
	for(int i=0; i<matrix.length; i++){
	    count[i][0] = (matrix[i][0] == '0'?0:1);
	    result = Math.max(result, count[i][0]);
	}
	for(int i=0; i<matrix[0].length; i++){
	    count[0][i] = (matrix[0][i] == '0'?0:1);
	    result = Math.max(result, count[0][i]);
	}

	//start transform status
	for(int i=1; i<matrix.length; i++){
	    for(int j=1; j<matrix[0].length; j++){
		if(matrix[i][j] == '0'){
		    count[i][j] = 0;
		    continue;
		}
		count[i][j] = Math.min(Math.min(count[i-1][j-1], count[i-1][j]), count[i][j-1]) + 1;

		result = Math.max(count[i][j],result);
	    }
	}

	return result * result;
    }
} 
```


