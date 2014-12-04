---
layout: post
title: Majority Vote
description: 
category: ISSUE
---

### Describe

Give you a log of searching that contains N words, how to find out one key word which appears over N/2 times, just using O(n) time complexity?

### Analyze

A majority word is still a major one if we minus two words which are different from each other. Otherwise, if the two words are the same, we can save the information of this word.

### Resolve

We can set two variables to use, one for saving current word (p) and another for counting (c). Initialize c=0 and p points to the front of the first word.

Make a rule while we iterate the words sequence like this:

1. If c=0, p saves no word;

2. Else if the next word equals the current one, c+=1; else c-=1.

You can see the whole process in this website for details:

[http://www.cs.utexas.edu/~moore/best-ideas/mjrty/index.html](http://www.cs.utexas.edu/~moore/best-ideas/mjrty/index.html)

PAPER TITLE: *MJRTY - A Fast Majority Vote Algorithm*

### Code

	// use number expression for example
	int n[10] = { 2, 1, 2, 3, 4, 2, 2, 1, 2, 2 };
	int c = 0, p;
	for (int i : n) {
		if (c == 0) {
			p = i;
			++c;
		} else {
			if (i == p)
				++c;
			else
				--c;
		}
	}
	std::cout << c << std::endl << p << std::endl;


