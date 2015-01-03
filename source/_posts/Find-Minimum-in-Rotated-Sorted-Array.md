title: Find Minimum in Rotated Sorted Array
date: 2015-01-02 16:32:27
tags: Binary Search
categories: Leetcode
---

> Question :  Suppose a sorted array is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
Find the minimum element.
You may assume no duplicate exists in the array.


####Approach####
经典题改编 把sorted array 变形了一下 找到最小值
废话不说 先上图， 左边的图表示的是如果array没有rotated，右边的自然是rotated过后的样子。可以沿用之前最基本的algo,稍加修改就可以完成这个算法。
最基本的算法可以参考 [Binary Search](/2015/01/02/Binary-Search/) 
观察右边的图可以发现：
如果 M 在 左边的那条线上， M 一定大于 R, 因此 L ＝ M ＋ 1
如果 M 在 右边的那条线上， M 一定是小于 R或者是等于R, 因此 R ＝ M. 等于R的情况是 M 正好落在了右边那条线的第一个点上，也正是如此，我们不能用 R = M - 1;
首先，需要注意的是，while loop 的condition 发生了改变, 第一是加了个额外条件 A[L] > A[R]， 这样做的原因是为了确保这个array是rotated. 一旦，A［L］ < A[R], 说明L从左边边那条线移到了右边，所以直接return A[L] 既得到结果。
第二注意， L <  R 而不是 L <= R, 如果出现了 L ＝ R 的情况， 那就是 L和R 正好都在最小值的index那里， 所以直接return A[L]即可，不需要再次进入while loop. 如果进入的话， 因为 R ＝ M， 所以while loop 会进入无限循环之中。   

![](http://i58.tinypic.com/2a98mz4.png)


####Solution####
{% codeblock lang:java %}
 public int findMin(int[] A) {    
       int L = 0;
       int R = A.length -1;
       while(L < R && A[L] > A[R]){
           int M = (L+R)/2;
           if(A[M] > A[R]) L = M + 1;
           else R = M;
       }
       
       return A[L];
    }
{% endcodeblock %}

<br>


#####Performance#####
	Time: O(log n)  Space: O(1)
