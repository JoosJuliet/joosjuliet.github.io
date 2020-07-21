---
layout: post
section-type: post
title: "Title"
category: Django
tags: [ 'django', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

coordinate => 좌표
equations => 방정식

# 2.
``` python
class Solution:
    def getLastMoment(self, n: int, left: List[int], right: List[int]) -> int:

  if right == []: return max(left)
  if left == []: return n-min(right)
  return max(n - min(right),  max(left))

# return max(max(left or [0]), n - min(right or [n]))
```

# 4. 버블소트 사용해서 O(N**2)

``` python
def minInteger(num: str, k: int) -> str:
    if k <= 0: return num
    n = len(num)
    if k >= n*(n-1)//2:
        return "".join(sorted(list(num)))

    for i in range(10):
        ind = num.find(str(i))
        if 0 <= ind <= k:
            return str(num[ind]) + minInteger(num[0:ind] + num[ind+1:], k-ind)


print(minInteger(num = "4321", k = 4))


```
