---
layout: post
title: Maximum Continuous Subset
description: 
category: ISSUE
---

### Describe

There is one integer array and you must find out one subset that contains the maximum continuous numbers with time complexity O(n). 

E.g. imput-> `15, 7, 12, 6, 14, 13, 9, 11`

output-> `5: [11, 12, 13, 14, 15]`

### Resolve

1. One intuitive way is to use *Disjoint Set* which is a structure for unioning or searching element in set. The time complexity is O(n).

2. The second way is to maintain the information of continuous numbers set using a starting number and an offset. See code logic for more details.

3. The simplest way is to use bitset to count the numbers and then find out the longest set. Bitset is good at saving memory although it may be hard to define the length sometimes in this question.

### Code

the 1st algorithm

	#include <iostream>
	#include <unordered_map>
	using std::cout;
	using std::endl;
	using std::unordered_map;

	int data[] = {15, 7, 12, 6, 14, 13, 9, 11};
	unordered_map<int,int> parent;
	unordered_map<int,int> rank;
	unordered_map<int,int> cnt;
	int max, val;

	int findParent(int x) {
		if (x != parent[x])
			parent[x] = findParent(parent[x]);
		return parent[x];
	}

	void unionSet(int x, int y) {
		int a = findParent(x);
		int b = findParent(y);
		if (a != b) {
			if (rank[a] < rank[b]) {
				parent[a] = b;
				cnt[b]+=cnt[b];
				max = max<cnt[b]?cnt[b]:max;
				val = b;
			} else {
				parent[b] = a;
				cnt[a]+=cnt[b];
				max = max<cnt[a]?cnt[a]:max;
				val = a;
				if (rank[a] == rank[b])
					++rank[a];
			}
		}
	}

	int main() {
		for (auto d : data) {
			if (parent.find(d)!=parent.cend())
				continue;
			parent[d] = d;
			rank[d] = 0;
			cnt[d] = 1;
			if (parent.find(d-1)!=parent.cend())
				unionSet(d-1, d);
			if (parent.find(d+1)!=parent.cend())
				unionSet(d+1, d);
		}
		cout<<max<<":";
		for (auto c : cnt)
			if (findParent(c.first) == val)
				cout<<' '<<c.first;
		cout<<endl;
		return 0;
	}

the 2nd algorithm

	#include <iostream>
	#include <unordered_map>
	using std::cout;
	using std::endl;
	using std::unordered_map;

	int data[] = {15, 7, 12, 6, 14, 13, 9, 11};
	unordered_map<int,int> um;
	int max;
	int val;

	int main() {
		for (auto d : data) {
			if (um.find(d)!=um.cend())
				continue;
			um[d] = 1;
			if (um.find(d-1)!=um.cend()) {
				um[d] += um[d-1];
				um[d-um[d-1]] = um[d];
				
				if (max < um[d]) {
					max = um[d];
					val = d-um[d-1];
				}
			}
			if (um.find(d+1)!=um.cend()) {
				int idx = d;
				if (um.find(d-1)!=um.cend())
					idx = d-um[d]+1;

				um[d] += um[d+1];
				um[d+um[d+1]] = um[d];
				um[idx] = um[d];

				if (max < um[d]) {
					max = um[d];
					val = idx;
				}
			}
		}

		cout<<max<<":";
		for (int i=0; i<max; ++i)
			cout<<" "<<val+i;
		cout<<endl;
		return 0;
	}

the 3th algorithm

	#include <iostream>
	#include <bitset>
	#define N 20
	using std::cout;
	using std::endl;
	using std::bitset;

	int data[] = {15, 7, 12, 6, 14, 13, 9, 11};
	bitset<N> bs;
	int max;
	int val;

	int main() {
		for (auto d : data) {
			if (bs.test(d))
				continue;
			bs.set(d);
		}
		int cnt = 0;
		int beg = -1;
		for (int i=0; i<bs.size(); ++i) {
			if (bs.test(i)) {
				if (beg == -1) {
					beg = i;
				}
				++cnt;
			} else if (beg != -1) {
				if (max < cnt) {
					max = cnt;
					val = beg;
				}
				cnt = 0;
				beg = -1;
			}
		}

		cout<<max<<":";
		for (int i=0; i<max; ++i)
			cout<<" "<<val+i;
		cout<<endl;
		return 0;
	}


