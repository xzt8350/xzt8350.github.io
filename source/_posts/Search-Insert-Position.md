title: Search Insert Position
date: 2015-01-02 14:23:14
tags: Binary Search
categories: Leetcode
---


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