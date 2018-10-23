---
layout: post
section-type: post
title: "[hacker_rank] Climbing the Leaderboard with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제:
https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem


``` python
import sys
read = lambda : sys.stdin.readline().strip()

int(read())
scores = [int(s) for s in read().split()]
int(read())
alice = [int(a) for a in read().split()]

unique_scores = list(sorted(set(scores), reverse = True))
i = len(alice)-1
j = 0
ans = []

while i >= 0:
    if j >= len(unique_scores) or unique_scores[j] <= alice[i]:
        ans.append(j+1)
        i -= 1
    else:
        j += 1
for i in sorted(ans, reverse = True):
    print(i)
```

# solution 2
이분트리로 풀기

``` python
import sys
import bisect
read = lambda : sys.stdin.readline().strip()

int(read())
scores = [int(s) for s in read().split()]
m = int(read())
alice = [int(a) for a in read().split()]

def get_rank(element, array):
    return len(array) + 1 - bisect.bisect(array, element)

for i in range(m):
    print(get_rank(alice[i], sorted(set(scores))))

```


# solution 3
이분탐색으로 풀기

``` python
int(input().strip())
scores = [int(s) for s in input().strip().split(' ')]
int(input().strip())
alice = [int(a) for a in input().strip().split(' ')]

def find(x, lst, a, b):
    if b == a:
        return b
    pivot = (b+a)//2
    if x == lst[pivot]:
        return pivot
    elif x > lst[pivot]:
        return find(x, lst, a, pivot)
    else:
        return find(x, lst, pivot+1, b)

scores = sorted(set(scores), reverse = True)

last = len(scores)
for x in alice:
    last = find(x, scores, 0, last)
    print(last+1)
```
