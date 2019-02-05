---
layout: post
section-type: post
title: "[hacker_rank]Cut the sticks with python3, Java8"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python3', 'Java8' ]
comments: true
---

https://www.hackerrank.com/challenges/cut-the-sticks/problem



로직은 비슷하다
단지 java와 python의 차이일뿐

# JAVA8

N log N
PriorityQueue는 nlog n이다.

``` JAVA
import java.util.*;
public class Solution {

    // Complete the cutTheSticks function below.

    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        int numSticks = sc.nextInt();
        Queue<Integer> sticks = new PriorityQueue<>(numSticks);
        Queue<Integer> tmpSticks = new PriorityQueue<>();
        for (int i = 0; i < numSticks; i++) {
            int stick = sc.nextInt();
            sticks.add(stick);
        }
        while (sticks.peek() != null) {
            System.out.println(sticks.size());

            for(Integer stick : sticks) {
                int cut = stick - sticks.peek();
                if (cut > 0)
                    tmpSticks.add(cut);

            }

            sticks.clear();
            sticks.addAll(tmpSticks);
            tmpSticks.clear();
        }
    }
}

```

# PYTHON3
이건 두가지다.

## sol1
nlog n
``` python
from collections import defaultdict # 콜렉션에서 불러옵니다.

d = defaultdict(lambda: 0) # Default 값을 0으로 설정합니다.
input()
sticks = list(map(int, input().split()))
sticks_len = len(sticks)
for s in sticks:
    d[s] += 1
d_sort = sorted(d)

for i in d_sort:
    print(sticks_len)
    sticks_len -= d[i]


```

## sol2
n ** 2


스터디에서 무려 https://wkdtjsgur100.github.io 이분이 올린 코드인

``` python
n = int(input())
l = list(map(int, input().split()))

while l:
    print(len(l))
    l = list(filter(lambda a: a != min(l), l))
```

이렇게 짧게도 할 수 있다...
그동안 python 중랩이라 생각했는데 난 아직 쪼중랩이다. ^^

``` python
input()
sticks = list(map(int, input().split()))

while len(sticks) != 0:
    cnt = 0
    min_value =  min(sticks)
    for i in range(len(sticks)):
        if sticks[i] >= min_value:
            sticks[i] -= min_value
            cnt += 1
    print(cnt)
    sticks = list(filter(lambda x: x > 0, sticks))

```
