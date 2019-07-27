---
layout: post
section-type: post
title: "[Null Safety 1편] NPE(NullPointerException)란? 극복법은? @NotEmpty, @NotBlank, @NotNull 차이란? @Column(nullable = false)이란? @Nullable이란? "
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
이 글은 시리즈 물입니다.
[Null Safety 1편] NPE(NullPointerException)란? 극복법은? @NotEmpty, @NotBlank, @NotNull 차이란? @Column(nullable = false)이란? @Nullable이란? https://joosjuliet.github.io/orm_jpa_hibernate/  
[Null Safety 2편] Optional이란? https://joosjuliet.github.io/optional/  
---

# 시작하는글
NullPointerException을 줄여서 NPE라고도 하는데 이 Null을 처음 도입한 <b>찰스 앤터니 리처드 호어</b>가 다음과 같이 말했다고 합니다.
"The Billion Dollar Mistake."
https://en.wikipedia.org/wiki/Tony_Hoare#Apologies_and_retractions




# NullPointerException(NPE)이란?

- 자바 데이터 타입은 기본 타입(primitive type)과 참조 타입(reference type)이 있다.
- Java는 기본적으로 초기화되지 않은 객체 참조 변수에 null을 할당합니다.
- 즉, 참조 변수를 선언하고 초기화하지 않으면 java에서 null로 지정된 특수 값을 지정합니다.
- 이를 가지고 아래 작업을 수행하면 NPE가 발생하게 된다.


``` java
public class TestClass {
    String string1;
    String string2 = null;

    public static void main(String[] a){
        TestClass testClass = new TestClass();

        System.out.println(testClass.string1);    // Output: null
        System.out.println(testClass.string2);    // Output: null
    }
}
```


## NPE가 발생하는 경우
- null 객체의 instance 함수(static이 아닌 method)를 호출하는 경우
- null 객체의 instance 변수에 접근하는 경우
- null 배열 객체의 length를 구하려는 경우
- null 배열 객체의 값을 인덱스로 접근하는 경우
- 애플리케이션 단에서 NPE를 던지는 경우



# 해결하는 법
- optional로 하는 법
- annotation으로 하는 법


## optional로 하는 법
``` java
//자바8에서 Optional의 ofNullabledm을 사용하여 null 처리
String strVal = null;
int value = Optional.ofNullable(strVal).map(Integer::valueOf).orElse(-1);
//String 값이 null이면, NPE를 내지 않고 대신에 -1을 리턴

System.out.println("return: " + value); //return: -1

```

> Optional의 자세한 내용은
[Null Safety 2편] Optional이란? https://joosjuliet.github.io/optional/  
을 참고해주세요




## annotation으로 하는 법
### 코드
``` java
@NotNull //return 값이 NotNull
public void makeSpaghetti(@NotNull String tomato , @Nullable String noodle) { /*매개변수가 NotNull*/
  return tomato + noodle
}
```


### @NotEmpty, @NotBlank, @NotNull 차이
- @NotEmpty
  - null이나 size가 0 검증(String, Collection)
- @NotBlank
  - null이나 whitespace 검증(String)
- @NotNull
  - nullvalues 검증





### @NotNull vs @Column(nullable = false)
*(in Hibernate)Column의 default는 nullable이다.*
- @NotNull 은 JSR 303 Bean Validation annotation
- @NotNull 은 db constraints를 신경쓰지 않는다.
- @Column(nullable = false)은 열을 null이 아니게 선언하는 JPA 방식입니다.
- @NotNull 는 유효성 검증을위한 것이고 @Column(nullable = false)는 데이터베이스 스키마 세부 사항을 나타 내기위한 것
- 즉 validation annotation에 대한 Hibernate의 도움을 받고있다.



### @Nullable 이란?
- 메서드가 null 값을 받아들이는지, 그리고 메서드를 재정의하는 경우 null 값을 받아 들여야한다는 것을 분명히합니다.
또한 FindBugs 같은 코드 분석기에 대한 힌트 역할을합니다. 예를 들어, 먼저 해당 메소드가 null을 확인하지 않고 인수를 역 참조하면 FindBugs가 경고를 내 보냅니다.

### 설정법
- preferenes/configure annotations 에 스프링에 관련된 annotation이 없다.
- 즉 추가 Nullabale, NonNull등을 해야한다.
- 그리고 재 시작!




## @Nullable 과 @NonNullByDefault
- @Nullable
  - 널 값이 허용되며 예상되어야 함
- @NonNullByDefault
  - 널 어노테이션이 없는 메소드 서명의 유형은 널이 아닌 항목으로 간주됩니다.

어노테이션 @NonNull 및 @Nullable은 다음 위치에서 지원됩니다.

메소드 매개변수
메소드 리턴(구문상 여기에서는 메소드 어노테이션이 사용됨)
로컬 변수
필드
Java 8에서는 추가 위치에 널 유형 어노테이션으로 어노테이션을 작성할 수 있습니다.
@NonNullByDefault는 다음에 제공됨

메소드 - 이 메소드의 서명에서 모든 유형에 영향을 줌
유형(클래스, 인터페이스, 열거) - 유형 본문의 모든 메소드에 영향을 줌
패키지(package-info.java 파일을 통해) - 패키지에서 모든 유형에 영향을 줌


# 널 어노테이션으로 표현할 수 있는 세 가지 레벨이 있습니다.

- 리더(사용자 및 컴파일러)에 대한 산발적인 힌트
- 규약에 의한 디자인: 일부 또는 모든 메소드에 대한 API 스펙
- 확장 유형 시스템을 사용하는 전체 스펙


nullable-annotation-usage
This annotation is commonly used to eliminate NullPointerExceptions. @Nullable is often says that this parameter might be null. Good example of such behaviour can be found in Google Guice. In this lightweight dependency injection framework you tell that this dependency might be null. If you would try to pass null and without annotation the framework would refuse to do it's job.

What is more @Nullable might be used with @NotNull annotation. Here you can find some tips how to use them properly. Code inspection in IntelliJ checks the annotations and helps to debug the code.

https://stackoverflow.com/questions/14076296/nullable-annotation-usage/14076320




*비슷한 팁*
- 빈 list를 줄 때는 Collections.emptyList()로 쓰는 게 더 좋다.

---
참조 :
https://www.amitph.com/avoid-nullpointerexception-using-java-8-optional/  dm
참고자료: https://www.baeldung.com/java-bean-validation-not-null-empty-blank  
http://blog.naver.com/PostView.nhn?blogId=tmondev&logNo=220791552394  

https://stackoverflow.com/questions/7439504/confusion-notnull-vs-columnnullable-false  

https://codeday.me/ko/qa/20190306/6221.html  
https://www.ibm.com/support/knowledgecenter/ko/SSRTLW_9.6.0/org.eclipse.jdt.doc.user/tasks/task-using_null_annotations.htm  
http://wonwoo.ml/index.php/post/1987  
