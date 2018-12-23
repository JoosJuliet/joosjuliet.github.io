---
layout: post
section-type: post
title: "(작성중) [재귀 함수 사용할 때 주의할 것] Tail_Recursion_Optimize"
categories: Python
tags: [ 'python', 'tail_recursion', 'stack_overflow', 'call_stack' ]
comments: true
---

# 재귀적 수행 시간 구하기


``` python
def f(n) :
  if n <= 1:
    return
  return f(n-1) + f(n-1)
```

함수 f가 두번 호출로 O(N**2)으로 오해를 받을 수도 있지만

<img alt="function_tree" src = "https://www.dropbox.com/s/ol8btyd557e9rs8/Screenshot%202018-12-18%2012.22.40.png?dl=0"/>

트리의 깊이가 N이고, 각 노드는 두개의 자식 노드를 갖고 있다.
따라서 깊이가 한 단계 깊어질 때마다 이전보다 두배 더 많이 호출하게 된다.
그럼으로 2의 제곱들의 합 인 2**(N+1) -1 이 시간복잡도 이다.

보통 재귀함수의 수행시간은 O(분기**깊이)로 표현된다.

# 다른 문제들

- n!을 구하는 코드의 big O는?
``` python
def factorial(n):
  if n < 0 :
    return -1
  else if n == 0 :
    return 1
  else:
    return n * factorial(n-1)
```
단순히 n부터 1까지 반복하는 재귀함수여서 O(N)이다.

- permutation을 구하는 코드의 big O는?
``` python
def permutation(str, prefix):
  if len(str) == 0 :
    print(prefix)
  else:
    for i in range(0, len(str)):
      permutation(str[0:i]+str[i+1:], prefix + str[i])
```
N!의 순열이 존재함으로 O(N!)이다.


https://joosjuliet.github.io/11724/
tail recursion 되는 것 해결책
파이썬 재귀 최대깊이 지정 sys.setrecursionlimit( limit )

# tail_recursion_optimize 가 나온 배경

우리는 종종 재귀함수를 쓴다.
재귀 함수는 자기 자신을 호출하는 함수이다.
코드가 짧아져 가독성을 높일 수 있지만, 스택 오버 플로우를 일으킬 수 있는 엄청난 위험성이 내재되어 있다.
그럼으로 1. 함수 과다 호출 2. stack overflow 라는 위험성이 있다.


그 위험성을 해결할 수 있게 해주는 것이 tail_recursion_optimize이다.

## 재귀함수가 stack overflow를 일으키는 이유

함수를 호출 시 함수의 입력 값(매개변수), 리턴 값, 리턴 됐을 때 돌아갈 위치 값 등을 스택에 저장한다.
*재귀함수를 사용하면 함수가 끝나지 않은 채 연속적으로 함수를 호출함으로 stack에 메모리가 끊임 없이 쌓이게 됩니다.*

즉 재귀함수를 사용하면 호출시 마다 스택에 해당 함수관련 정보가 memory를 계속 쌓이게 되고,
함수가 return값을 반환해야 stack이 비워지는데, 함수가 끝나지 않은 도중에 계속 함수가 호출됨으로 함수의 깊이는 계속 깊어만 진다.
즉 계속 메모리가 쌓이게 되고 그래서 stack overflow가 일어난다.


일반 재귀함수
``` cpp
int fibonacci(n) {
  if (n < 2) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```
일반 재귀함수
```
호출 : fibonacci(6)

call fibonacci(6)
  call fibonacci(5)
    call fibonacci(4)
      call fibonacci(3)
        call fibonacci(2)

          call fibonacci(1)
          return 1
          call fibonacci(0)
          return 0
        return 1
        call fibonacci(1)
        return 1
      return 2
      call fibonacci(2)
        call fibonacci(1)
        return 1
        call fibonacci(0)
        return 0
      return 1
    return 3
    call fibonacci(3)
      call fibonacci(2)
        call fibonacci(1)
        return 1
        call fibonacci(0)
        return 0
      return 1
      call fibonacci(1)
      return 1
    return 2
  return 5
  call fibonacci(4)
    call fibonacci(3)
      call fibonacci(2)
        call fibonacci(1)
        return 1
        call fibonacci(0)
        return 0
      return 1
      call fibonacci(1)
      return 1
    return 2
    call fibonacci(2)
      call fibonacci(1)
      return 1
      call fibonacci(0)
      return 0
    return 1
  return 3
return 8
```
앞에 fibonacci를 호출 했음에도 계속 다시 함수를 stack에 호출한다.

무려 함수 호출을... n이 3인데 5번이나 하고 심지어 n이 6이면 25번하며,
딱 봐도 정신이 혼란스럽다.
즉 n이 100만 되도 stack_overflow가 난다.

이런 단점을 보완하기 위해 나온 것은 *tail_recursion* 이라는 최적화 방법이다.

# tail_recursion
*[주의사항]컴파일러가 이런 최적화 기능을 지원하는지 먼저 확인해야 합니다. gcc는 제공합니다. python은... py언어단 부터 제공 안합니다.*

함수 호출이 반복되어 스택이 깊어지는 문제를 컴파일러가 스택 재사용을 할 수 있게 하는 것입니다.
(값이 변할 여지가 없으므로 스택을 덮어 쓸 수 있기 때문에)

## 일반 재귀함수와 꼬리 재귀함수를 비교


꼬리 재귀함수
``` cpp
function fibonacciTailRecursion(n, previousFibo, previousPreviousFibo) {
  if (n < 2) return n * previousFibo;
  return fibonacciTailRecursion(n - 1, previousFibo + previousPreviousFibo, previousFibo);
  }
```

연산이 어떻게 되는지 보면


꼬리 재귀함수
```
호출 : fibonacciTailRecursion(3, 3, 2)
call fibonacciTailRecursion(3, 3, 2)
  call fibonacciTailRecursion(2, 5, 3)
    call fibonacciTailRecursion(1, 8, 5)
    return 2
  return 2
return 2
```
acc변수에 계산 한 값을 저장 후 값을 한번에 반환함으로,
스택을 한번 호출하는 것으로 끝낸다.
반복 단계별 계산 결과를 반복이 끝날 때까지 어떤 변수에 계속 저장한 다음에
필요할 때 가져다 쓰는 것이다.



컴파일러가 해석하는 것으로 해석(?) 해보면
```
function sumLoop(n) {
    var accumulator = 0;
    while(n) {
        accumulator += n--;
    }
    return accumulator;
}

```
이렇게 됨으로 O(n)으로 된다.


# tail_recursion 지원하는 곳

## cpp
당연히 해준다'ㅅ'

## python
컴파일러에서 최적화 기능을 지원하지 않다는 이유로, 그냥 계속 overflow를 낼 수 없다.
그래서 다양한 pip들이 있다.

https://github.com/baruchel/tco

## js
es6부터 공식지원한다.



# 정리
재귀 호출은 탈출로직만 잘 다듬으면 전체적으로는 직관적이고 이해하기 쉬운 코드를 작성할 수 있게 해준다.
하지만 재귀 호출 깊이가 깊어지면 stack을 많이 사용하는 문제가 발생한다.
그렇지만 반복이나 꼬리 호출 단계별 계산 결과를 어딘가에 계속 저장하는 tail recursion 방식으로 구현하면 문제를 피할 수 있다.

그러나 tail recursion을 지원해 주지 않을 대는 유일한 해결책은 반복문이다.




---
# 참고자료
재귀적 수행 시간 구하기 부분
[코딩인터뷰 69쪽 11번째 줄부터 70쪽까지]

https://homoefficio.github.io/2015/07/27/%EC%9E%AC%EA%B7%80-%EB%B0%98%EB%B3%B5-Tail-Recursion/
http://bozeury.tistory.com/entry/%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80-%EC%B5%9C%EC%A0%81%ED%99%94Tail-Recursion

https://homoefficio.github.io/2015/07/27/%EC%9E%AC%EA%B7%80-%EB%B0%98%EB%B3%B5-Tail-Recursion/
https://groups.google.com/forum/#!topic/scala-korea/5PCCAS8wu8o
