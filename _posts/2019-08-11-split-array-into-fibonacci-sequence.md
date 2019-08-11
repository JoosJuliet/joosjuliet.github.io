---
layout: post
section-type: post
title: "[leet_code] 842. Split Array into Fibonacci Sequence with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---


문제 : https://leetcode.com/problems/split-array-into-fibonacci-sequence/

# 목표:
- substring이 피보나치 수열이 맞게 해라.

# 조건:
- 숫자 앞에 0이 있는 경우는 없다.
  - 07 의 숫자는 아니다.
- 만약에 조건에 맞는 피보나치가 안되면 []이다.
- 숫자의 크기는 2**31 - 1 보다 작아야한다 'ㅡ'
# solution 설명 :
- O(N**3)
- brute force로 다해보는 것이다 ㅇ<-<


``` python

class Solution:
  def splitItoFibonacci(S):
      L, T, t = len(S), "", []
      for i in range(1,L-2):
          for j in range(1,L-i-1):
              a, b = int(S[:i]), int(S[i:i+j])
              T, t = S[:i+j], [a,b]
              while len(T) < L:
                  c = a + b
                  T += str(c)
                  t += [c]
                  a, b = b, c
              # 일단 맞든 틀리든 한다. 계속 한다.
              if len(T) == L and T == S and len(t) > 2 and t[-1] < 2**31 - 1:
                  # 맞으면 그 때 return이 되는거다. 그리고 0인 경우를 안해도 그냥 어차피 여기서 걸러진다.

                  # len(T) == L and T == S는 그냥 대놓고 맞춰보는거
                  # len(t) > 2 는 개수가 충분히 찾나 확인
                  # t[-1] < 2**31 - 1 숫자가 제한 넘지 않나 확인
                  return t
      return [] # 앞에서 return이 안됬으면 그냥 [] 주는 것이다.
  # 대신 n세제곱
```
