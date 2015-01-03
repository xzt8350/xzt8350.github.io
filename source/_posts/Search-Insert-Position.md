title: Search Insert Position
date: 2015-01-02 14:23:14
tags: Binary Search
categories: Leetcode
---

> Question :  Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. You may assume no duplicates in the array.Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0


####Approach####
看到是sorted array 就知道此题一定会用到binary seach. 这题比较简单，用最经典[binary search algorithm](/2015/01/02/Binary-Search/)模版稍加修改就可得到。 


####Solution####
{% codeblock lang:java %}
 public int searchInsert(int[] A, int target) {
        int lo = 0;
        int hi = A.length - 1;
        while (lo <= hi) {
            int mid = (lo + hi)/ 2;
            if (target < A[mid]) hi = mid - 1;
            else if (target > A[mid]) lo = mid + 1;
            else return mid;
        }
        return lo;
 }
{% endcodeblock %}


####Note####
这题和经典模版唯一的不同是return lo 而不是 -1. 可能有些人会疑惑为什么不是 return hi, 设想一下，如果这个target 可以在这个array 里找到，那么function 直接return mid, 所以和lo 和 hi没有什么关系。
只有在target 在这个array 里找不到的情况下我们才可以分析为什么是return的是 lo 而不是 hi. 第一种情况是， 搜索到 lo 的 index 比 high 小一个， 比如 lo 的index  是 10， hi 的index 是 11， mid的index 是 （10 ＋ 11） ／2 ＝ 10；我们可以发现 mid 的值在这种情况下 是lo 的 值，所以 mid 和 target 相比较 就是等同于 lo 和 target 相比较。 如果 lo > target, return lo, 新加的target应该放在lo这个位置。 反之，如果 target > lo -> lo + 1, target 放在 lo + 1 这个位置上。 第二种情况是， lo 的 index 和 high 相等， 所以 mid 的 index 也一定 和 lo 还有 hi 相等。 在这种情况下，与第一种情况相似， return lo 或者 hi 肯定不会错。
通过上面的分析，我们可以发现，只有当return lo 的 时候才能涵盖所有的 case.


#####Performance#####
	Time: O(log n)  Space: O(1)
