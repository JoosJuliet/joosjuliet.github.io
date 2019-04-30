---
layout: post
section-type: post
title: "(작성중) [javascript] js는 single thread?"
categories: Javascript
tags: [ 'Javascript', 'javascript' ]
comments: true
---

# 작성중입니다. 틀린내용이 있을 수 있습니다.


일단 웹서버로 보자면, web은 *브라우저 engine* 과 *서버 engine* 즉 두가지 엔진을 신경써야 합니다.

memory
# js는 memory allocation할 때 stack, heap을 둘 다 쓰나요?
- closure를 저장할 때 private heap을 씁니다. stack이 아니라요.

일단 js는 ecma를 따릅니다. 근데 memory를 어디에 저장해야 하는지는 안써있죠. (https://www.ecma-international.org/ecma-262/8.0/index.html)

그래서 interpreter에 따라서 어떤 곳에다 할 지를 정할 수 있습니다. 가장 많이 사용하는 V8 engine을 가지고 얘기해 보겠습니다.

일단 쉽게 생각하면 js는 grabage-collected language임으로 data가 scattered될 것이기 때문에 stack에 저장될 것이라고 생각할 수 있습니다. 그러나 그렇지 않습니다.

왜냐하면 stack은 data를 ordering 하기 때문입니다. 그럼으로 변수들은 heap에 저장됩니다.

NodeJS unofficial V8 reference의 코드를 보면
[https://github.com/v8/v8/blob/ddec1c4f57a94f5e0450e70c98c1b5d2d5f0d46e/include/v8.h#L2385]

내가 Boolean value를 사용하면 Boolean class가 객체화 됩니다. 그리고 그 v8 engine은 cpp로 만들어져 있습니다. cpp은 heap에다가 data를 저장하고, stack의 pointer로만 동작합니다. 따라서, v8에 새 변수를 할당해야 할 때마다 힙에 대한 추가 정보와 함께 데이터가 들어있는 구조가 할당된다.


만약 boolean data만 온다면 stack 구조를 사용하는 것이 더 좋지만, 매번 다른 크기의 data가 온다면 적합하지 않다.
변수는 heap에 stack에는 저장이 안된다 근데 함수를 쓸때는 콜스택을 사용하는 것이다

---
# single thread를 사용한 이유

js는 동시성이 있는 언어를 만들고 싶어서 만들었다.
동시성을 원하기 때문에 async 기능을 원하게 된 것이다.

js에서 엔진은 다양한 게 있는데 그 중 v8엔진을 얘기하겠다.
v8엔진에서 async 기능을 만들었을 때 왜 하필 멀티 스레드가 안되는 것을 원했나 생각을 가질 수 있다.(안나와 있다.)
근데 v8엔진에서 async 부분을 핵심적으로 담당한 애는 libuv library인데, 이 애 때문에 single thread를 사용하게 되었다.

*즉 js는 libuv library 때문에 single thread가 된 것 이다.*

그럼 왜 하필 멀티 스레드가 안되는데 이걸 선택한 걸까 라는 생각을 할 수 있다.
libuv 엔진과 같이 async 일을 하면서 multi-thread를 지원 하는 library도 있다.(ex. GLib library)

그런데도 불구하고 libuv가 많은 사람들(+Node)이 async를 원할 때 이걸 사용하는 것은 일단 사용자가 많고, 가볍고 멀티 플랫폼에서 성능과 안정성이 더 많이 검증되었기 때문이다. multi-thread를 지원하는 이유로 상당히 많은 것을 고려해야 하기 때문에 무거워 질 수 밖에 없고, (멀티 스레드를 지원하는 다른 Library의 단점) 가볍게 만드는 데 집중하자 라면, libuv를 선택해서 async를 만든 것 같다.

*즉 js는 동시성을 원하기 때문에 async 기능이 필요했고, 그렇기 때문에 async 기능을 만들기 위해서 libuv library를 사용했고, libuv library는 single thread만 사용하게 했기 때문에 js는 single thread만 사용하게 되었다.*


<!-- async programming을 하기 위해 concurrency를 확보해야 하는데(Non-blocking이 사용되어야 한다), 그걸 Event-loop를 사용해서 한다. -->



그런데 여기서부터는 뇌피셜이다. v8 engine과 ajax 모두 google에서 만든것이다.
(내용은 사실이다.)
Ajax call은 Ajax 호출은 실행을 멈추고 다른 코드는 호출이 반환 될 때까지 실행할 수 있습니다.

JavaScript is only asynchronous in the sense that it can make, for example, Ajax calls. The Ajax call will stop executing and other code will be able to execute until the call returns (successfully or otherwise), at which point the callback will run synchronously. No other code will be running at this point. It won't interrupt any other code that's currently running.


그리고 멀티스레드를 지양했던 이유는 I/O 대기 시간(polling time)이 항상 0이 되어 CPU 사용률이 100%을 시키기 위해서 인 것 같다.

---
# single thread 장점
싱글 쓰레드 : 문맥교환으로 인한 오버헤드X
비동기 IO : CPU time loss를 피함, io요청이 있으면 워커한테 던져놓고 쓰레드는 다른일을 계속 받는다.


non-blocking이기 때문에 non-blocking의 장점을 그대로 가져온다.

일단 js는 프론트를 염두하고 태어난 아이여서 프론트 엔드에 최적화 된 아이이다.

문제상황 1)
프론트 엔드에서는 다양한 서버에서 내용을 주고 받을 수 있다.
(참고로 most of the I/O works 부분은 multi-thread를 사용할 수 있다. main event loop는 single thread고)
The main event loop is single-threaded but most of the I/O works run on separate threads
그런데 동기라면 코드 앞쪽에 있던 부분에서 서버가 연결이 안되서 지연이 되고 있으면 뒷쪽에서 계속 기다리고 있어야 한다. 그런데 만약 사용자가 원하는 것은 뒷쪽에서 간단하게 버튼을 클릭하는  거였다면, 그 버튼이 늦게 나와서 그 나오는 순서를 계속 기다리는 불상사가 나타난다.

문제상황 2)
서버에 있을 때 만약 사람들이 들어왔는데 각자 다른 thread에 있다.있는데

##그렇다면 non-blocking를 하려면 왜 single thread를 선택해야 할까?

non-blocking을 하려면 asynchronous call을 해야하기 때문이다.
async call을 하기 위해서는 kernel에 모든 책임을 떠넘겨야 합니다.
왜냐하면 이벤트큐를 작업할 때 쓰는 Libuv 라이브러리가 그렇게 만들어졌기 때문입니다.
Libuv라이브러리를 써야 하는 이유는 싱글스레드를 사용하기 때문에 worker들이 task를 수행해야 하기 때문에 OS Kernel과 함게 이 워커들을 다루는데 도움을 주는 일을 하기 때문이다.
(참고) Libuv는?
Libuv는 강력한 커널을 사용하여 asynchronous 이벤트의 관리 및 대기열을 다루는 마법의 라이브러리입니다.


락을 걸어야만 하는 이유는 kernel에 모든 책임을 떠넘긴 상황인데 그건 async가 안되서이거
(참고) thread pool은 존재한다
It’s so because the kernel doesn’t support doing everything asynchronously. In those cases Node has to lock a thread for the duration of the operation so it can continue executing the event loop without blocking.

동기식 IO에서는 디스크에 파일쓰기요청이 들어오면, 디스크가 파일쓰는 동안에 cpu가 논다. 다쓰면 return이 돌아와서 그다음 코드가 진행된다.

비동기에서는 저런 요청이 들어오면 워커한테 일준다. 그러고선 계속 cpu가 쉬지않고 다른 요청들을 받는다. io처리가 끝나면 워커가 콜백함수와 함께 파일쓰기가 끝났다고 알려준다. cpu 효율입장에서 엄청난 차이인 거다. 또한 워커들의 일을 kernel마구 주고 있는데 multi thread 때문에 context switching하다보면 kernel의 작업 효율도가 떨어질 거라는 판단으로... kernel은 워커한테 일 주는데 집중을 하게 한다.

또한 프론트에서 복잡한 작업을 예전에는 별로 하지 않았기에 별 문제 없겠지.. 라는 안일한 생각을 했다는 풍문도 있다.
그치만 web gl이 똥싸놨따.

응용 프로그램에서 커널의 서비스를 사용하는 방법이 시스템 호출인데 커널은 프로세스 관리, 동시성, 메모리 관리등을 한다.


multithread를 하려면 Context Switching를 해야하는데, 그 때 많은 부하가 걸리기 때문에 오히려 퍼포먼스는 떨어지게 됩니다.



node는 single thread 임에도 불구하고 non-blocking을 사용하기 위해서 kernel로 가 system call을 사용한다.
간단한 작업들은 event loop에서 single thread로 하고 복잡하고 긴 작업들은 non-blocking worker(c++ threadpool)한테 시켜서 callback을 통해 main thread로 다시 보낸다.
<!--
Apache와 같은 웹서버는 웹 리소스가 요청될 때마다 요청을 처리하기 위해 매번 별도의 스레드를 생성하거나, 새 프로세스를 호출한다.
request가 많은 경우, 병목구간이 흔히 발생하는데, 까보면 로직보다는 IO에서 문제(서버에서 IO처리하다가 지연발생으로 다른 요청들이 처리되지 않음)가 많다. 동기 방식에서 이를 해결하기 위해 흔히 멀티쓰레드에 스케일아웃하고 로드밸런싱을 한다.하지만 Node와 같이 비동기로 처리하게 될 경우, 훨씬 가벼우면서도 빠른데, 요청 처리가 완료되기전에 제어권을 다음 요청으로 넘긴다. 논블로킹으로 요청들을 처리할 수 있는 것이다. Node.js는 싱글스레드 위에서 비동기로 돌아간다. URL_A가 들어오면 이벤트를 돌리고, 또 다음 URL_B를 받고 이벤트 돌리고, 그 와중에 A가 완료되면 콜백해주는 방식이다.

단일 쓰레드이기 때문에 오버헤드가 적어 어플리케이션 확장성을 쉽게 얻을 수 있다. 또한 리소스 사용량을 최소화하였기 때문에 멀티스레드로 굳이 만들 필요가 없다. -->


---
# libuv란

*비동기 이벤트 루프를 만들게 해준 핵심 library*

thread 간의 통신을 할 수있다. (uv_async_send()함수가 유일) 그러나 좀 더 통신을 정밀 히 하기 위해서는 thread 간 통신에 TCP / UDP / 파이프 등을 이용해도 되지만 오버헤드가 발생할 수밖에 없다.  (예를 들어 GLib 같은 경우 특정 스레드에서 어떤 함수를 호출하고 싶으면 해당 스레드에서 실행 중인 루프의 콘텍스트에 g_idle_add() / g_timeout_add() 종류의 함수를 이용해서 쉽게 추가할 수 있다.) 하지만 libuv에서는 아이에 활동 방식이 다르다. 메시지 큐 또는 채널 같은 자료구조를 구현해서 메시지를 전달하면 그 메시지를 해독해서 특정 함수를 실행하거나 작업을 진행하는 방식이다.


---
# single thread 단점


---
JS에서는 multithreaded가 안되지만 앞서 말했듯 JS안해줘도 brower engine에서 해줄 수 있다. HTML5에서 web worker라고 멀티스레드를 사용할 수 있게 해준다.(background에서 도는 걸로)
---


2-3. 싱글쓰레드로 여러 요청을 어떻게 받는가?
멀티플렉싱으로 해결한다.
---
javascript는 single thread로 움직인다. 블로킹 모델을 채용했다는 건 아니다. 전혀 다르다.
js는 다른식으로 비동기 프로그래밍을 한다.
multithread 언어에서는 어떤 작업을 해당코드와 병렬 실행을 시킬 수 있지만, js는 어떤 이벤트가 끝나자마자 실행할 함수를 큐에 넣는게 고작이다.
여기서 이벤트는 일정시간 경과, 다른 웹 사이트에서 데이터 조회, 마우스 클릭 등이다.
js 엔진은 event loop에서 한번에 하나씩 함수를 꺼내 실행한다.
설계 관점에서 보면 이런 방식이 오히려 멀티 스레드 환경보다 생각하기 편하다.
제어권을 가진 상태에서도 인터럽트를 당하거나 다른 객체가 변수에 마음대로 접근하는 식의 문제는 신경 쓰지 않으니까 말이다.
즉 프로세서를 독차지할 염려도 없다.


---
참고자료
[Concurrency model and Event Loop]
https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop

https://hashnode.com/post/does-javascript-use-stack-or-heap-for-memory-allocation-or-both-cj5jl90xl01nh1twuv8ug0bjk

[kernel 설명]
https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/

[single thread 사용 이유 설명]
https://codeburst.io/how-node-js-single-thread-mechanism-work-understanding-event-loop-in-nodejs-230f7440b0ea
http://sjh836.tistory.com/79 [빨간색코딩]

[libuv 설명]
https://lethean.github.io/2016/03/08/note-about-libuv/
