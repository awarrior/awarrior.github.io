---
layout: post
title: Reservoir Sampling
description: 
category: ISSUE
---

### Describe

Sample K elements in N data, and N is not sure.

Imaging one setting: there is one continuous infinite data flow coming one after another, and we can not save the whole data. This situation limits us that the number N of coming data is changeable and we have to keep the randomness in the sampling.

There are many applications existing this problem such as search engine and file search.

### Resolve

The probability of each element drawing is the same, K/N, N is changeable.

Method 1. Keep K minimum elements

Use one Hash function to generate one random number according to each orignal value. Besides, define an array with K size to save the K minima in the random numbers. If there already are K minima and the new coming number is smaller than the biggest in array, let it swap with the biggest one. 

However, this method's performance is associated with the design of Hash function. That is to say that the mimima may stay at the fixed region and this loses the generality of randomness.

Method 2. Keep K elements using probability

Pick up the first K elements and save them in the array with K size. The NO.K+1 data will be chosen with 1/i (i=K+1,K+2,...,N) probability to swap with one of elements in the array, which is seleted randomly.

Here is the proof:

---
Assume A[i] is the event that element A (saved in array) will leave in the Round i (i=K+1,K+2,...,N); AS is the event that element A will be substituted at this moment; B is the event that the coming new element will replace one of elements in the array; AC is the event that A becomes the element would like to be replaced.

The probability of A[i+1] is:

`P(A[i+1]) = P(A[i]) * (1 - P(AS))`  
`= P(A[i]) * (1 - P(B) * P(AC))`  
`= (k/i) * (1 - (k/(i+1)) * (1/k))`  
`= (k/(i+1))`

Q.E.D.

---


