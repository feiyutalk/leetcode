# 042 Trapping Rain Water

采用双指针的做法，设置一个头指针，一个尾指针。先找到上升的第一个位置，然后计算后面的能装的水。

```java
class Solution {
    public int trap(int[] height) {
        if(height == null || height.length == 0)
            return 0;
        int res = 0;
        int l = 0;
        int r = height.length-1;
        while(l<r && height[l] < height[l+1])
            l++;
        while(l<r && height[r] < height[r-1])
            r--;
        while(l<r){
            int left = height[l];
            int right = height[r];
            if(left < right){
                while(l<r && height[l] <= left){
                    res += left - height[l];
                    l += 1;
                }
            }else{
                while(l<r && height[r] <= right){
                    res += right - height[r];
                    r -= 1;
                }
            }
        }
        return res;
    }
}
```

