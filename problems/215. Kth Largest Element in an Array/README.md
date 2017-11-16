# 215. Kth Largest Element in an Array

# Description

Find the **k**th largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
Given `[3,2,1,5,6,4]` and k = 2, return 5.

# Solution

关于选择第kth个大小元素的题目其实已经挺常见的了，一种做法就是通过构建堆，堆这种数据结构能够保证每次得到最大值(最小值)，然后依次弹出最大值(最小值)直到第k个，就可以得到第kth个大小的元素的值。

另外一种思路是采用 Quick Select算法，这种算法是将快排的思路用在第kth元素上，因为只是对快排的原理掌握了，并没有总结快速排序的算法模板，今天就借着这道题，把快速排序的算法模板总结一下。而且，只需要记住找第kth小的模板就可以了，因为第kth大的情况，可以转换为第nums.length - kth小的情况来处理。

```java
public int quickselect(int[] nums, int start, int end, int k) {// quick select: kth smallest
	if (start > end) return Integer.MAX_VALUE;
	
	int pivot = nums[end];// Take A[end] as the pivot, 
	int left = start;
	for (int i = start; i < end; i++) {
		if (nums[i] <= pivot) // Put numbers < pivot to pivot's left
			swap(nums, left++, i);			
	}
	swap(nums, left, end);// Finally, swap A[end] with A[left]
	
	if (left == k)// Found kth smallest number
		return nums[left];
	else if (left < k)// Check right part
		return findKthLargest(nums, left + 1, end, k);
	else // Check left part
		return findKthLargest(nums, start, left - 1, k);
} 

void swap(int[] A, int i, int j) {
	int tmp = A[i];
	A[i] = A[j];
	A[j] = tmp;				
}
```

