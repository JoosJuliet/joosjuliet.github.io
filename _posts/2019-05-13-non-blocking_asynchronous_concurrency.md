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

*Wait-freedom*
wait-free : 어떤 알고리즘의 모든 연산이 완료될 때 까지 밟는 단계(명령어 수로 봐도)가 유한한(상수는 아님에 주의) 경우
- 기다림이 없으나 호출수 한정
- 모든 호출이 한정된 수의 단계로 끝나도록 보장되는 경우 메소드는 대기하지 않아도됩니다.
- wait-free 메소드는 결코 블로킹되지 않으며 교착상태가 발생하지 않으며
- 참여자는 제한된 수의 호출후에 진행할수 있으므로 궁핍(기아)현상이 발생하지 않습니다.

*Lock-freedom*
lock-free : 개별 스레드는 starvation을 겪을 수 있지만(즉 진행을 못함), 전체적으로는 항상 진행
- Lock이 없음
- Lock이 없기때문에 교착상태가 발생하지 않지만 호출이 결국 완료되는것을 보장하지 않기때문에 궁핍(기아)현상을 보장하기에는 충분하지 않습니다.

*Wait-freedom, Lock-freedom차이*
차이는 개별 스레드의 진행을 보장하냐 마느냐임. (어느 쪽이든 전체적으론 진행한다).
개별 스레드도 무조건 진행하게되는 wait-free는 당연히 lock-free인게 자동으로 보장된다.



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

# Non-blocking vs. Blocking
한 스레드의 지연이 다른 스레드를 무기한 지연 시킬수 있을때 블록킹되었다라고 표현함
예를 들면 상호배제(mutual exclusion)을 사용하여 하나의 스레드가 독점할시 자원을 공유하고있는
다른 스레드가 진행될수 없는경우 논블록킹은 이와 반대되는 개념으로, 어떠한 스레드도 다른것들을 무기한 연기할수 없다란것을 의미합니다.
블록킹 작업포함시 전반적인 작업진행이 쉽게 보장이 되지 않기때문에, 논블록킹 작업방식으로의 설계가 추천됩니다.

# Deadlock vs. Starvation vs. Live-lock
## DeadLock
DeadLock(교착상태)는 여러 Task가 어떠한 특정 상태를 기다린후 진행할수 있는 구조에서
어떠한 Task가 특정상태에 도달하지 못할때 하위의 모든 시스템이 멈추는 경우입니다.



## Starvation
Starvation(빈곤)은 계속 진행이되며 , 우선순위가 높은 Task가 어렵게 진행이되지만  
항상 높은 우선순위의 Task를 선택하는 순진한 스케쥴링 알고리즘때문에 낮은 순위의 Task가
끝나지 않거나 진입을 못하는 경우입니다.



## LiveLock
LiveLock은 Task중 누구도 진행되지 않는 경우이며, 교착상태와 유사합니다. 서로 진행되기를
기다리면서 Task의 상태가 지속적으로 변화는 상황으로 불행한 경우 획득하지 않고 항상 상대방에게
양보하는 경우가 발생하여 누구도 실행되지 않는 케이스입니다.

## Race Condition
우리가 정한 이벤트 세트의 순서에대한 가정이 , 외부의 결정적이지 않은 효과임에도 불구하고
위반되어 오동작인 상태가 되는것을 레이스(경쟁) 조건이라고 합니다.
발생하는 케이스는 스레드가 공유 가능상태를 가지고 경쟁상태가 자주발생하면서 스레드의 작업순서가
바뀌면서 예기치 않는 동작이 발생하는것입니다. 일반적으로 공유상태는 경쟁조건을 가질필요가 없으며
순서를 보정하지 않습니다. 패킷으로 예를 들면 P1,P2를 차례로 서버에 보냈지만 패킷이 다른 네트워크의
경로 를 통해 P2를 먼저받고 P1을 나중에 수신받을수 있으며 순서에대한 정보처리없이 서버가 이를 처리하려한다면
패킷의 의미에 따라 Race Condion(경쟁조건)이 발생할수가 있습니다. 이것은 멀티스레드에서도 발생할수 있는
문제이며 동시에 공유자원을 접근해서 발생하는 문제도 포함됩니다.

---
참고 :
https://tech.peoplefund.co.kr/2017/08/02/non-blocking-asynchronous-concurrency.html
https://rein.kr/blog/archives/1346
http://wiki.webnori.com/pages/viewpage.action?pageId=1507411
