---
id: mZ4d7lYDaMGWwd84azIZG
title: Inplace Operations
desc: ''
updated: 1628747092778
created: 1628745034586
---

## Two pointer technique

Implementing this requires the use of the two-pointer technique. This is where we iterate over the Array in two different places at the same time.

- Read all the elements like we did before, to identify the duplicates. We call this our readPointer.
- Keep track of the next position in the front to write the next unique element we've found. We call this our writePointer.

Example: In the below example _idx is the second pointer_

1. [Remove Element](https://leetcode.com/explore/learn/card/fun-with-arrays/526/deleting-items-from-an-array/3247/)

All two pointer [questions](https://leetcode.com/tag/two-pointers/)