---
layout: post
section-type: post
title: "[leet_code] 134. Gas Station with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---

문제 : https://leetcode.com/problems/gas-station/submissions/

# 목표:
- 총 가스양이 음수가 되지 않은 채로 모든 station을 돌아야한다.
- 어느위치에서 시작하든 모든 station을 차례로 돈다.

# 조건:
- 경로는 하나이다.
- gas, cost 모두 양수만 있고 빈칸은 없으며 길이는 같다.

# solution 설명 :

이 문제를 해결하려면 다음 두 가지 사실을 이해하고 사용해야한다.
- 가스의 합이 비용의 합보다 크면 원을 완성 할 수 있다.
- A가 "A-> B-> C"의 순서로 C에 도달 할 수 없으면 B 역시 도달할 수 없다.
  - 근데 이거 왜 있는거지... 그니까 만약 중간부터가 시작인 건데
  - 그 앞쪽에 있는 애들이 조건에 만족하다는 것과 무슨상관이야?
## 2번증명
- gas[A] < cost[A]이면 A는 B에 도달 할 수 없다.
  - 따라서 A에서 C에 도달하려면 gas[A] >= cost[A] 만족해야 한다.(B를 거쳐야만 c를 가야하니까)
- A가 C에 도달 할 수 없다면 gas[A] + gas[B] <cost[A] + cost[B]이다.
  - 그런데 앞서 말한 b로 도달하기 위해  gas[A]> = cost[A]를 반드시 만족해야한다.
- 그러므로 gas[B] < cost[B]를 만족해야한다.
  - 결국 B는 C에 도달 할 수 없다.
- 결론: A가 C에 도달할 수 없다면, B 역시 도달할 수 없다.


``` python
def canCompleteCircuit(gas, cost) -> int:
    start = tank = chk = 0
    for i in range(len(gas)):
        difference = gas[i] - cost[i]
        # 각 gas와 cost의 차이를 tank에 더한다.

        tank += difference
        chk += difference
        if tank < 0:
            start = i + 1
            # 총 합이 음수가 되면 그곳의 위치에서 시작을 할 수 없기 때문에 다음 위치라고 생각하고 start의 위치를 옮긴다.
            tank = 0
    if chk < 0 :
        return -1
    return start
```

---
reference:
https://www.programcreek.com/2014/03/leetcode-gas-station-java/
