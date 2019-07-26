---
layout: post
section-type: post
title: "[hacker_rank] Bigger is Greater in a Grid with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

문제 : https://www.hackerrank.com/challenges/bigger-is-greater/problem

# 목표:
- 현제 주어진 글자보다 사전순으로 높은 글자를 보여주거나 없으면 NO ANSWER주기

# 조건:
- w가 길이 100까지 될 수 있기 때문에 brute force는 안된다.

# solution 설명 :
- http://www.nayuki.io/page/next-lexicographical-permutation-algorithm
- 총 길이 구한다.
- 이미 다 정렬이 된 것의 index(i)찾는다.
- 이미 정렬된 것을 벗어났기에 충분히 지금의 수보다 더 큰 수를 만들 수 있는 s[i-1]
- 그 s[i]보다 큰 수를 정렬된 부분에서 찾아 index(j)를 저장한다.
- s[i-1]과 s[j]를 바꾼다.
- 그 바꾼 것을 reversed만 해도 된다. 이미 정렬이 되어잇기 때문에


``` python

def next_permutation( s):
    i = len(s)-1
    # 총 길이 구한다.

    while i > 0 and s[i-1] >= s[i]:
        # 1. 이미 다 정렬이 된 것의 index(i)찾는다.
        i -= 1
    # 2. 이미 정렬된 것을 벗어났기에 충분히 지금의 수보다 더 큰 수를 만들 수 있는 s[i-1]


    if i <= 0:
        return "no answer"

    j = len(s)-1
    while i-1 < j:
        if s[i-1] < s[j]:
            # 3. 그 s[i]보다 큰 수를 정렬된 부분에서 찾아 index(j)를 저장한다.
            break
        j -= 1

    sl = list(s)
    sl[i-1], sl[j] = sl[j], sl[i-1]
    # s[i-1]과 s[j]를 바꾼다.
    return ''.join(sl[:i] + list(reversed(sl[i:])))
    # 그 바꾼 것을 reversed만 해도 된다. 이미 정렬이 되어잇기 때문에
for t in range(int(input())):
    print(next_permutation(input()))

```
