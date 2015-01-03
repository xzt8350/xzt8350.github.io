title: Search in Rotated Sorted Array
date: 2015-01-02 16:28:39
tags: Binary Search
categories: Leetcode
---

> Question :  Suppose a sorted array is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
You are given a target value to search. If found in the array return its index, otherwise return -1.
You may assume no duplicate exists in the array.


####Approach####
先用[Find Minimum in Rotated Sorted Array](/2015/01/02/Find-Minimum-in-Rotated-Sorted-Array/)的算法得到这个array里最小的值。然后在用target 和 array里最右边的element做比较确定搜索范围。最后用经典binary search algo 既可以得到答案


####Solution####
{% codeblock lang:java %}
public int search(int[] A, int target) {        
   int L = 0;
   int R = A.length-1;
   /* Find minimum element in the array */
   while(L < R && A[L] > A[R]){
   	  int M = (L+R)/2;
   	  if(A[M] > A[R]) L = M + 1;
   	  else R = M;
   }	
   /* Get the range of the target */            
   if(target <= A[A.length - 1]){
      R = A.length -1;
   }
   else{
      R = L -1;
      L = 0;
   }
   /* Classical Binary Search Alogo */
   while(L <= R){
      int M = (L + R)/2;
      if(A[M] > target) R = M - 1;
      else if(A[M] < target) L = M + 1;
      else return M;
   }	            
   return -1;        
}
{% endcodeblock %}

<br>

####Note####




#####Performance#####
	Time: O(log n)  Space: O(1)
