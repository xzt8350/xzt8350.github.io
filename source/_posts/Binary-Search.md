title: Binary Search
date: 2015-01-02 18:14:21
tags: Binary Search
categories: Algorithm
---

###Introduction###
相信接触过算法的朋友对这个Binary Search都应该很熟悉 简单的来讲就是用 **O(log n)** 的时间去搜索一个sorted array. 注意，这里面有个key word -> sorted array. 正是因为是sorted, 所以我们可以每次找到array的中间值，然后比较这个中间值的大小与given target的大小，以此来决定我们是从中间element的右边还是左边开始下一次的搜索。

####Classical Binary Search Question####
> Given an sorted integer array - a, and an integer - target. Find the first position of target in a, return -1 if target doesn’t exist.

{% codeblock lang:java %}
 public int binarySearch(int[] a, int target) {
      int lo = 0;
      int hi = a.length - 1;
      while (lo <= hi) {
         int mid = (lo + hi)/2;
         if (a[mid] == target) return mid;
         else if (a[mid] < target) lo = mid + 1;
         else hi = mid - 1;
      }
      return -1;
   }
{% endcodeblock %}

这个alorithm 应该很好理解，唯一需要注意的是while loop的condition是 lo<= hi 而不是lo < hi, 这样做的原因是如果不巧，正好我们algorithm 搜索到最后一次的时候是target值，而此时正好lo == hi,如果while loop 的 condition 是 lo < hi 的话，则进入不了while loop, function return -1，得到了错误的答案。 lo <= hi 这个condition 就可以解决这个edge case.  


