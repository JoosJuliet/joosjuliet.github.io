---
layout: post
section-type: post
title: "[hacker_rank] Java String Compare with java"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'java' ]
comments: true
---

문제:
https://www.hackerrank.com/challenges/java-string-compare/problem

``` Java
public static String getSmallestAndLargest(String s, int k) {
    String largest = s.substring(0, k);
    String smallest = s.substring(0, k);
    for (int i = 0; i <= s.length() - k; i++){
        String curr = s.substring(i, i + k);
        if (curr.compareTo(smallest) < 0)
            smallest = curr;
        if (curr.compareTo(largest) > 0)
            largest = curr;
    }         
    return smallest + "\n" + largest;

}
```
