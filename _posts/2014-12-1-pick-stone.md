---
layout: post
title: Pick Stone
description: 
category: ISSUE
---

### Describe

Two players would like to pick up some from one heap of stones. Assume the quantity of stones is 100 and these two men pick up some one by one. The winner is whom brings the last one.

Please figure out the solution that the prior picker wins the game.

### Rule

1. No one can pick up all the stones once if he is the prior picker;

2. The number of stones player can pick up must not exceed the double of previous one pick after the first pick.

### Resolve

There exits one assumption (*how to reach ?_?*):

* If the quantity of stones is a Fibonacci number (in Fibonacci sequence), the first picker will lose this game.

Give a proof using mathematical induction:

---
Let F(i) denotes the number of stones, x is the number the first player picks up and y is the number the second player does.

1. When i=2, it's easy to comprehend that assumption meets the 1st rules.  

2. Assume when i<=k, that assumption is true.  

When i=k+1, F(k+1)=F(k)+F(k-1).  

The terms F(k) and F(k-1) are Fibonacci numbers and both let the first picker lose.   

It's obvious to see that the first picker would lose when x>F(k+1)/3. Then if x<=F(k+1)/3, we will get x<F(k-1)<F(k). Because of this:

F(k-2)<F(k-1) => F(k-1)+F(k-2)<2\*F(k-1) => F(k-1)+F(k)<3\*F(k-1) => F(k+1)/3<F(k-1)<F(k)

So when x<F(k-1)<F(k), y can be F(k-1)-x and let the number of stones become a Fibonacci number F(k). This proves the first picker must lose again.

Above all, first picker is loser when stones number is a Fibonacci number.

---

Let's explore another situation, that is stones quantity is not a Fibonacci number (like the issue condition: 100).

Before we expand the discussion of this situation, let's see Zeckendorf representation.

* Each positive integer could be denoted as the cumulation of several discontinuous Fibonacci numbers (in Fibonacci sequence).

We can get that F(k)>2\*F(k-2) because of F(k-1)+F(k-2)>2\*F(k-2). This can be more general that F(k)>2\*F(k-i) with i>=2.

The first picker will win if he pick up the minimal Fibonacci number as a part of the stones number. After this, the second player will become the first picker of the second minimal Fibonacci number so that the first picker has an opportunity to become the last-one picker, according to the previous prove.

This progress will be more clear if we use the one number to explain. Here is the answer of the issue.

### Answer

According to Zeckendorf representation, 100 stones can be represented by 100=89+8+3.

Let x and y be the number of stones the first and second player picks up in one round.

Here is one example:

Round 1: x=3, y=6; left=91;  
Round 2: x=2,|y=4; left=85;  
Round 3: x=4, y=8; left=73;  
Round 4: x=13, y=26; left=34;  
Round 5: x=34. (win)  


