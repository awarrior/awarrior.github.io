---
layout: post
title: Maximal Difference
description: 
category: ISSUE
---

### Describe

Given one integer array, you have to find out two disjoint continuous sub-array A and B, which maximate the absolute value of SUM(A)-SUM(B).

For example, [2,-1,-2,1,-4,2,8], A=[-1,-2,1,-4], B=[2,8], the maximum is 16.

### Resolve

It's obvious see that to one array with N length, there is N-1 positions to seperate the original array. Then we get left sub-array and right sub-array.

We have to iterate the left and right part and find out the minimum and maximum respectively using dynamic programming method. It's important to figure out that, in front of one number position x, the minimum VAL will be `VAL[x] = MIN { VAL[x-1]+arr[x], arr[x] }` (similar to maximum). Then we could get several minimal (or maximal) sumary value (different end positions) if we notice to mark in all the minimal (or maximal) sumary in all positions.

This algorithm will get O(N) time complexity.

### Code

{% highlight c++ %}
#include <iostream>
using std::cout;
using std::endl;

const int arr[] = {2,-1,-2,1,-4,2,8};
const int sz = sizeof(arr)/sizeof(int);

struct sumType {
	int sum; // the sumary number
	int len; // the length of sumary
	int idx; // the best index in the history
};

// columns represent min & max
sumType left[sz][2];
sumType right[sz][2];

// a: cols in array; b: left or right part
void init(sumType sav[][2], int a, int b) {
	for (int i=b; i<sz-(1-b); ++i) {
		sumType &s = sav[i][a];
		if (i==0) {
			s = {arr[i], arr[i], 1};
		} else {
			s.sum = sav[i-1][a].sum+arr[i];
			s.len = sav[i-1][a].len+1;
			if ((a == 0 && arr[i] < s.sum) || \
				(a == 1 && arr[i] > s.sum)) {
				s.sum = arr[i];
				s.len = 1;
			}

			int idxs = sav[i-1][a].idx;
			if ((a == 0 && s.sum < sav[idxs][a].sum) || \
				(a == 1 && s.sum > sav[idxs][a].sum))
				s.idx = i;
			else
				s.idx = idxs;
		}
	}
}

int main() {
	// initialize
	init(left, 0, 0);
	init(left, 1, 0);
	init(right, 0, 1);
	init(right, 1, 1);

	// compare
	int max, li, ri;
	bool flag;
	for (int i=1; i<sz; ++i) {
		const int &li_min = left[i-1][0].idx;
		const int &li_max = left[i-1][1].idx;
		const int &ri_min = right[i][0].idx;
		const int &ri_max = right[i][1].idx;
		int tmp1 = left[li_max][1].sum-right[ri_min][0].sum;
		int tmp2 = right[ri_max][1].sum-left[li_min][0].sum;
		if (i==1 || tmp1 > max) {
			max = tmp1;
			li = li_max;
			ri = ri_min;
			flag = 1;
		}
		if (tmp2 > max) {
			max = tmp2;
			li = li_min;
			ri = ri_max;
			flag = 0;
		}
	}

	// print
	cout<<max<<endl;
	for (int i=left[li][flag].len-1; i>=0; --i)
		cout<<' '<<arr[li-i];
	cout<<endl;
	for (int i=right[ri][!flag].len-1; i>=0; --i)
		cout<<' '<<arr[ri-i];
	cout<<endl;

	return 0;
} 
{% endhighlight %}


