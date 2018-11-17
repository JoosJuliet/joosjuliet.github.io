---
layout: post
section-type: post
title: "[hacker_rank]Sherlock and the Valid String with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/sherlock-and-valid-string/problem

``` python
from collections import Counter, defaultdict
import operator

def isValid(S):
    count_d = defaultdict(lambda: 0)
    char_map = Counter(S)
    for i in char_map.values():
        count_d[i] +=1
    if len(count_d) == 1:
        return True
    if len(count_d) == 2:
        count_d = sorted(count_d.items() , key=operator.itemgetter(1), reverse=True)
        if count_d[1] == (1, 1):
            return True
        if count_d[1][1] == 1:
            if count_d[1][0] - count_d[0][0] == 1:
                return True
    return False

if isValid(input()):
    print ("YES")
else:
    print ("NO")
```

---
참고 코드:
https://www.hackerrank.com/challenges/sherlock-and-valid-string/submissions/code/90790756
