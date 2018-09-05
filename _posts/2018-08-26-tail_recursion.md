---
layout: post
section-type: post
title: "[재귀 함수 사용할 때 주의할 것] Tail_Recursion_Optimize"
categories: Python
tags: [ 'python', 'tail_recursion', 'stack_overflow', 'call_stack' ]
comments: true
---

# tail_recursion_optimize 가 나온 배경

우리는 종종 재귀함수를 쓴다.
재귀 함수는 자기 자신을 호출하는 함수이다.
코드가 짧아져 가독성을 높일 수 있지만, 스택 오버 플로우를 일으킬 수 있는 엄청난 위험성이 내재되어 있다.

그 위험성을 해결할 수 있게 해주는 것이 tail_recursion_optimize이다.

## 재귀함수가 stack overflow를 일으키는 이유

함수를 호출 시 함수의 입력 값(매개변수), 리턴 값, 리턴 됐을 때 돌아갈 위치 값 등을 스택에 저장한다.
*재귀함수를 사용하면 함수가 끝나지 않은 채 연속적으로 함수를 호출함으로 stack에 메모리가 쌓이게 됩니다.*

즉 재귀함수를 사용하면 호출시 마다 스택에 해당 함수관련 정보가 memory를 계속 쌓이게 되고,
함수가 return값을 반환해야 stack이 비워지는데, 함수가 끝나지 않은 도중에 계속 함수가 호출됨으로
계속 메모리가 쌓이게 된다. 그래서 stack overflow가 일어난다.


일반 재귀함수
``` cpp
int fibonacci(n) {
  if (n < 2) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```
일반 재귀함수
```
호출 : fibonacci(3)

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
```
무려 함수 호출을... n이 3인데 5번이나 한다.
심지어 n이 6이면 25번한다 ^^
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
https://homoefficio.github.io/2015/07/27/%EC%9E%AC%EA%B7%80-%EB%B0%98%EB%B3%B5-Tail-Recursion/
http://bozeury.tistory.com/entry/%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80-%EC%B5%9C%EC%A0%81%ED%99%94Tail-Recursion

https://homoefficio.github.io/2015/07/27/%EC%9E%AC%EA%B7%80-%EB%B0%98%EB%B3%B5-Tail-Recursion/
https://groups.google.com/forum/#!topic/scala-korea/5PCCAS8wu8o
