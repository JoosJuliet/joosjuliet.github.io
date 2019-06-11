---
layout: post
section-type: post
title: "(작성중)stack(스택), queue(큐), deque(덱)란?"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
# 큐(Queue)
1. 선형 리스트의 한쪽에서는 삽입 작업이 이루어지고 다른 한쪽에서는 삭제 작업이 이루어지도록 구성한 자료 구조이다.
2. 가장 먼저 삽입된 자료가 가장 먼저 삭제되는 선입선출(FIFO)방식으로 처리한다.
3. 시작과 끝을 표시하는 두 개의 포인터가 있다.

<img alt="success" src = "/images/2019-05-24-stack-queue-deque/queue.png"/>


## 프런트(F) 포인터
1. 가장 먼저 삽이된 자료의 기억공간을 가리키는 포인터이다.
2. 삭제 작업을 할때 사용한다.


## 리어(R) 포인터
1. 가장 마지막에 삽입된 자료가 위치한 기억장소를 가리키는 포인터이다.
2. 삽입 작업을 할 때 사용한다.



# 덱(Deque)
1. 삽입과 삭제가 리스트의 양쪽 끝에서 모두 발생할 수 있는 자료 구조이다.
2. Double Ended Queue의 약자이다.
3. Stack과 Queue의 장점만 따서 구성한 것이다.


<img alt="success" src = "/images/2019-05-24-stack-queue-deque/deque.png"/>입력이 한쪽에서만 발생하고 출력은 양쪽에서 일어날 수 있는 입력제한과 입력은 양쪽에서 일어나고 출력은 한쪽에서만 이루어지는 출력 제한이 있다.

``` python


```


---
출처:
https://coding-factory.tistory.com/230
