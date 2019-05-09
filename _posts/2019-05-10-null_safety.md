---
layout: post
section-type: post
title: "[Null Safety] @NOTNULL"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# 시작하는글
NullPointerException을 줄여서 NPE라고도 하는데 이 Null을 처음 도입한 <b>찰스 앤터니 리처드 호어</b>가 다음과 같이 말했다고 합니다.
"The Billion Dollar Mistake."
https://en.wikipedia.org/wiki/Tony_Hoare#Apologies_and_retractions


# 대체 왜?

reference type을 다룰 때는 항상 null 값에 대비하여 프로그래밍을 해야 한다. 이 과정에서 때로는 불필요한 null 확인 코드가 포함되며, nested object 참조 과정에서 반복적인 null 확인으로 코드의 가독성을 떨어트리곤 한다.

기본적으로 default값을 심는것이 중요하다.




NullPointerException(NPE)이란?
자바 데이터 타입은 기본 타입(primitive type)과 참조 타입(reference type)이 있다. 참조 타입은 객체의 생성 이전에는 할당된 메모리 주소가 없는 null을 참조하는 변수이며 이를 가지고 아래 작업을 수행하면 NPE가 발생하게 된다.

NPE가 발생하는 경우
 * null 객체의 instance 함수(static이 아닌 method)를 호출하는 경우
 * null 객체의 instance 변수에 접근하는 경우
 * null 배열 객체의 length를 구하려는 경우
 * null 배열 객체의 값을 인덱스로 접근하는 경우
 * 애플리케이션 단에서 NPE를 던지는 경우






# 쓰는 법
``` java
@NotNull //return 값이 NotNull
public void makeDinner(@NotNull String tomato , @Nullable String noodle) { /*매개변수가 NotNull*/

  return tomato + noodle
}
```

# 설정법
- preferenes/configure annotations 에 스프링에 관련된 annotation이 없다. 추가 해야한다.
- Nullabale, NonNull등을 .
- 재 시작해야한다.

---
참조 :
http://blog.naver.com/PostView.nhn?blogId=tmondev&logNo=220791552394
