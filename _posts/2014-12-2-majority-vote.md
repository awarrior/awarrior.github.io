---
layout: post
title: Majority Vote
description: 
category: ISSUE
---

### Describe

Give you a log of searching that contains N words, how to find out one key word which appears over N/2 times (definitely exists), just using O(n) time complexity?

### Analyze

There is a very important pre-condition in this issue: *the target word which we want to find definitely exists*.

Let's see several examples first:

`(A B) C A A B`  
`(A B) C A A B A`  
It doesn't matter if we leave A&B out, A is still the result.

`(C B) A A A B A`  
It doesn't matter if we leave C&B out, A is still the result.

`(A A) C B A B A`  
We have to record the apperance times of A for further judgement.

Here we consider two word each time. A majority word is still a major one if we minus two words which are different from each other. Otherwise, if the two words are the same, we also need to save the information of this word.

Actually, we can consider this words sequence as conbination of several word pairs (two words). 

### Resolve

We can set two variables to use, one for saving current word (p) and another for counting (c). Initialize c=0 and p points to the front of the first word.

Make a rule while we iterate the words sequence like this:

1. If c=0, p saves no word;

2. Else if the next word equals the current one, c+=1; else c-=1.

You can see the whole process in this website for details:

[http://www.cs.utexas.edu/~moore/best-ideas/mjrty/index.html](http://www.cs.utexas.edu/~moore/best-ideas/mjrty/index.html)

PAPER TITLE: *MJRTY - A Fast Majority Vote Algorithm*

### Code

{% highlight c++ %}
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
{% endhighlight %}


