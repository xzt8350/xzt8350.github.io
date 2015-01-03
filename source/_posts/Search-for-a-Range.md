title: Search for a Range
date: 2015-01-02 16:05:48
tags: Binary Search
categories: Leetcode
---

> Question :  Given a sorted array of integers, find the starting and ending position of a given target value. Your algorithm's runtime complexity must be in the order of O(log n). If the target is not found in the array, return [-1, -1].
For example,
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].


####Approach####
可以先用最基本的binary search algorithms 找到 target. 如果没有找到的话，直接return [-1, -1]. 如果找的话，就需要找到这个target的开始和结束。 这也是本题的难点。 我最开始想的方法是新建两个pointer, 指到刚刚找到的target index, 然后一个pointer一直往前找，直到遇到的element 不等于target. 第二个pointer往后找，逻辑同理。 但是这个算法找到target的开始和结尾用了O(n)的时间。为了保证算法始终是O(log n)，我们需要用binary search 去找到target的开始和结尾。 


####Solution####
{% codeblock lang:java %}
	public int[] searchRange(int[] A, int target) {
	    int index = binarySearch(A, 0, A.length-1, target);
	    int[] result = {-1, -1};
	    if (index != -1) {
	        int left  = index; 
	        int right = index;
	        result[0] = left;
	        result[1] = right;
	        //Find the starting and ending index for the target
	        while ((left  = binarySearch(A, 0, left-1, target)) != -1)           result[0] = left;
	        while ((right = binarySearch(A, right+1, A.length-1, target)) != -1) result[1] = right;
	    }
	    return result;
	}

	//Helper function : Binary Search
	private int binarySearch(int[] A, int lo, int hi, int target) {
	    while (lo <= hi) {
	        int mid = lo + (hi - lo) / 2;
	        if      (A[mid] < target) lo = mid + 1;
	        else if (A[mid] > target) hi = mid - 1;
	        else return mid;            
	    }
	    return -1;
	}
{% endcodeblock %}

<br>


#####Performance#####
	Time: O(log n)  Space: O(1)
