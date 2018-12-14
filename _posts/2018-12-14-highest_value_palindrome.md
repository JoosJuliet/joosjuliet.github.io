---
layout: post
section-type: post
title: "[hacker_rank]Highest Value Palindrome with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/richie-rich/problem

``` python
n, k = map(int, input().split())
nl = list(input())

ans = 0
change_set = set([])

for i in range(n//2+1):
    if nl[i] == nl[n-i-1]: continue
    else:
        k -= 1
        if k < 0 :
            ans = -1
            break
        if nl[i] < nl[n-i-1]:
            change_set.add(i)
            nl[i] = nl[n-i-1]
        else:
            change_set.add(n-i-1)
            nl[n-i-1] = nl[i]

for j in range(n//2+1):
    if k == 0: break
    if nl[j] != '9':
        if (j in change_set) or ( n-j-1 in change_set):
        # 만약 그 상대편 혹은 그 부분이 이미 바꾼 것
            k -= 1 # 하나만 줄인다.
            nl[j] = nl[n-j-1] = '9'
        else:
        # 한번도 안바꾼거 -> 그것도 된다. 그냥 바꿔서 크기만 하면 되니까
            if k >= 2:
                k -= 2
                nl[j] = nl[n-j-1] = '9'
            if k >= 1 and j == n-j-1: # 젤 가운데 있는 것 바꾸기
                nl[j] = '9'

if ans != -1:
    print(''.join(nl))
else:
    print(-1)

```
