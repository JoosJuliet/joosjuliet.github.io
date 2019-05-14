---
layout: post
section-type: post
title: "(작성중)[ WebFlux 1탄 ] 사전지식( Non-Blocking, Asynchronous, Concurrency )"
category: WebFlux
tags: [ 'WebFlux', 'java', 'Non-Blocking', 'Asynchronous', 'Concurrency' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

# Non-Blocking
두 가지 의미
- Non-blocking algorithm(Non-blocking synchronization)
- Non-blocking I/O(Asynchronous I/O 혹은 Non-sequential I/O)




## 1. Non-Blocking algorithm
- Non-blocking이란, <span style="background-color:yellow"><b> 어떤 쓰레드에서 오류가 발생하거나 멈추었을 때 다른 쓰레드에게 영향을 끼치지 않도록 만드는 방법 </b></span>
- 공유 자원(메모리, 파일 등)를 사용하는 멀티 쓰레드 프로그래밍을 할 때, 특정 공유 자원을 사용하는 부분에서 뮤텍스나 세마포어 등을 사용하여 여러 쓰레드에서 동시에 접근하지 못하도록 개발자가 보장하는 것이 전통적인 방법이었다.
- Non-blocking algorithm(Wait-freedom, Lock-freedom 등)을 사용하여 공유 자원을 안전하게 동시에 사용

*Wait-freedom, Lock-freedom*




## 2. Non-Blocking I/O
- Non-blocking I/O란, <span style="background-color:yellow"><b> 입출력 처리는 시작만 해둔 채 완료되지 않은 상태에서 다른 처리 작업을 계속 진행할 수 있도록 멈추지 않고 입출력 처리를 기다리는 방법 </b></span>
- I/O 처리를 하는 전통적인 방법은 I/O 작업을 시작하면 완료될 때까지 기다리는 방법
- 기존에는 synchronous I/O 혹은 blocking I/O를
, 이는 수많은 I/O 작업이 있는 경우 I/O 작업이 진행되는 동안 프로그램이 아무일도 하지 않고 시간을 소비
- 반면, Non-blocking I/O 방식을 사용하면 외부에 I/O 작업을 하도록 요청한 후 즉시 다음 작업을 처리함으로써 시스템 자원을 더 효율적으로 사용
- 그러나 I/O 작업이 완료된 이후에 처리해야하는 후속 작업이 있다면, I/O 작업이 완료될 때까지 기다려야 한다
- 따라서 이 후속 작업이 프로세스를 멈추지 않도록 만들기 위해, I/O 작업이 완료된 이후 후속 작업을 이어서 진행할 수 있도록 별도의 약속(Polling, Callback function 등)을 한다.


*Polling, Callback function*


# Asynchronous Programming(비동기 프로그래밍)
- 프로그램의 주 실행흐름을 멈추어서 기다리는 부분없이 즉시 다음 작업을 수행할 수 있도록 만드는 프로그래밍 방식
- <span style="background-color:yellow"><b> 이는 코드의 실행 결과 처리 및 활용을 별도의 채널에 맡겨둔 뒤 결과를 기다리지 않고 바로 다음 코드를 실행하는 방식으로 프로그램을 진행</b></span>
- 결과를 처리하는 방식은 여러가지가 있다 그중 대표적으로 세가지가 있다.
  - 언어에서 지원하는 방식(future, promise와 같은 객체 형태의 결과를 요청 즉시 돌려받는 방식
  - Python의 코루틴(Coroutine)과 같은 언어의 문법을 이용하는 방식 등)을 사용하는 방식
  - 함수 전달을 통해 처리하는 방식(함수를 값처럼 사용(First-class function)하는 것을 지원하는 언어에서 콜백 함수(Callback function)를 전달하여 결과를 처리하는 방식)


*promise*
*go routine*

# Asynchronous I/O
- 비동기 I/O 또는 비 블로킹 I/O는 전송이 완료되기 전에 다른 처리를 계속할 수 있도록하는 입출력 처리의 한 형태입니다.
- 이것이 의미하는 바는 프로세스가 동기 호출에서 read () 또는 write ()를 수행하려는 경우 하드웨어가 물리적 I/O를 완료 할 때까지 기다려야 프로세스가 성공/실패를 알 수 있고, I/O 작업이 실패했습니다.
- 비동기 모드에서 프로세스가 비동기 적으로 읽기/쓰기 I/O를 실행하면 I/O가 하드웨어에 전달되거나 OS/VM에 대기하면 즉시 시스템 호출이 반환됩니다.
- 따라서 시스템 호출의 결과를 기다릴 필요가 없기 때문에 프로세스의 실행이 차단되지 않습니다 (따라서 논 블로킹 I/O라고하는 이유). 나중에 결과를 수신합니다.

# Non-blocking과 Asynchronous 그리고 Concurrency
- Non-blocking과 Async를 비교해보자는 질문이 있다면, 질문 자체를 좀 더 명확히 할 필요성이 있다.
- 우선 Non-blocking은 앞서 짚어본 바와 같이 Non-blocking I/O를 의미할 수도 있고, Non-blocking 알고리즘을 의미할 수도 있다.
- 또한 Async라는 용어는 Asynchronous I/O를 의미할 수도 있고, Asynchronous Programming을 의미할 수도 있다.


- I/O 작업을 멈추지 않고 기다리는 방식을 구체적으로 분류하면 Synchronous Non-blocking I/O와 Asynchronous blocking I/O 등으로 구분할 수 있기 때문에 이를 비교해보는 것은 의미가 있다.
- 그러나 Non-blocking I/O와 Asynchronous Programming은 비교 대상이 되기 어렵다. 각 개념이 바라보는 관점이 다르기 때문이다.
- Asynchronous Programming을 위한 재료로써 Concurrency를 확보하거나 혹은 Non-blocking I/O를 활용할 수 있으나, 이것이 Asynchronous Programming의 필수조건은 아니다.
- 예를 들어 Event-loop를 사용하여 동시성을 확보했으나, I/O 작업의 성격에 따라 그 처리를 위해 blocking I/O 모델을 사용할 수 있다.
- Blocking I/O를 사용했어도 이 부분이 별도의 채널을 통한 작업으로 이루어짐으로써 이 프로그램의 주 실행흐름(event-loop)을 막지 않았다면, 이 프로그램은 Asynchronous Programming이라고 부를 수 있다.



---
참고 :
https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html
