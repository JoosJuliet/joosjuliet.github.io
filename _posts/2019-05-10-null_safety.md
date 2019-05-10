---
layout: post
section-type: post
title: "[Null Safety] NPE란? 극복법은? Optional 과 @NotEmpty, @NotBlank, @NotNull 차이"
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




# NullPointerException(NPE)이란?
- 자바 데이터 타입은 기본 타입(primitive type)과 참조 타입(reference type)이 있다.
- 참조 타입은 객체의 생성 이전에는 할당된 메모리 주소가 없는 null을 참조하는 변수이다.
- 이를 가지고 아래 작업을 수행하면 NPE가 발생하게 된다.




## NPE가 발생하는 경우
- null 객체의 instance 함수(static이 아닌 method)를 호출하는 경우
- null 객체의 instance 변수에 접근하는 경우
- null 배열 객체의 length를 구하려는 경우
- null 배열 객체의 값을 인덱스로 접근하는 경우
- 애플리케이션 단에서 NPE를 던지는 경우




# optional로 하는 법
``` java
//자바8에서 Optional의 ofNullabledm을 사용하여 null 처리
String strVal = null;
int value = Optional.ofNullable(strVal).map(Integer::valueOf).orElse(-1);
//String 값이 null이면, NPE를 내지 않고 대신에 -1을 리턴

System.out.println("return: " + value); //return: -1

```


*Optional이란?*
값이 있거나 또는 없는 경우를 표현하기 위한 클래스
Optional는 “존재할 수도 있지만 안 할 수도 있는 객체”
즉, “null이 될 수도 있는 객체”을 감싸고 있는 일종의 래퍼 클래스입니다.
직접 다루기에 위험하고 까다로운 null을 담을 수 있는 특수한 그릇


*Optional 클래스 쓰는 법*
1. null이 아닌 객체를 담고 있는 Optional 객체
2. null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성


## 1. null이 아닌 객체를 담고 있는 Optional 객체
``` Java
Optional<Member> maybeMember = Optional.empty();
Optional.of(value)
```
- null이 아닌 객체를 담고 있는 Optional 객체를 생성합니다.
- null이 넘어올 경우, NPE를 던지기 때문에 주의해서 사용해야 합니다.


## 2. null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성
``` JAVA
Optional<Member> maybeMember = Optional.of(aMember);
Optional.ofNullable(value)
```
- null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성합니다.
- Optional.empty()와 Optional.ofNullable(value)를 합쳐놓은 메소드라고 생각하시면 됩니다.
- null이 넘어올 경우, NPE를 던지지 않고 Optional.empty()와 동일하게 비어 있는 Optional 객체를 얻어옵니다.
- 해당 객체가 null인지 아닌지 자신이 없는 상황에서는 이 메소드를 사용하셔야 합니다.

*가장 큰 오류*
“Optional 적용 후 어떻게 null 체크를 해야하나요?”
“null 체크를 하실 필요가 없으시니 하시면 안 됩니다.”


우리가 Optional을 사용하려는 이유는 고통스러운 null 처리를 직접하지 않고 Optional 클래스에 위임하기 위함입니다.

# annotation으로 하는 법


## 코드
``` java
@NotNull //return 값이 NotNull
public void makeDinner(@NotNull String tomato , @Nullable String noodle) { /*매개변수가 NotNull*/

  return tomato + noodle
}
```




## @NotEmpty, @NotBlank, @NotNull 차이
- @NotEmpty
  - null이나 size가 0 검증(String, Collection)
- @NotBlank
  - null이나 whitespace 검증(String)
- @NotNull
  - nullvalues 검증




## 설정법
- preferenes/configure annotations 에 스프링에 관련된 annotation이 없다. 추가 해야한다.
- Nullabale, NonNull등을 .
- 재 시작해야한다.



---
참조 :
참고자료: https://www.baeldung.com/java-bean-validation-not-null-empty-blank  
http://blog.naver.com/PostView.nhn?blogId=tmondev&logNo=220791552394
