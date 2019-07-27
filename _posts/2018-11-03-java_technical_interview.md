---
layout: post
section-type: post
title: "[tech interview 2 편] JAVA"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'Java' ]
comments: true
---

이글은 tech interview를 볼 때 기본적으로 물어보는 것들을 정리하기 위해 쓴 글입니다.
깊이 보다는 compact 성을 강조합니다.
---
이 글은 시리즈 물입니다.

[tech interview 1 편] DB https://joosjuliet.github.io/db_technical_interview/  
[tech interview 2 편] JAVA https://joosjuliet.github.io/java_technical_interview/  
[tech interview 3 편] Network https://joosjuliet.github.io/network_technical_interview/  
[tech interview 4 편] Operating System
 https://joosjuliet.github.io/os_technical_interview/  
[tech interview 5 편] WEB https://joosjuliet.github.io/web_technical_interview/  
[tech interview 6 편] SPRING https://joosjuliet.github.io/spring_technical_interview/
---


아무래도 java를 쓰는 회사들이 많아서 신입면접에는 java에 대한 질문도 꽤 하는 것 같다.
1편과 마찬가지로 얕게만 쓴다

근데 사실 몇개의 질문은 java에만 국한 되게 아니라 모든 언어에 해당 되는 문제인 것도 있다.

# 1. Overloading vs Overriding
- Overloading(오버로딩)
  - 같은 이름의 메소드를 여러개 정의하는 것
  - 매개변수의 타입이 다르거나 개수가 달라야 한다.

- Overriding(오버라이딩)
  - 상속에서 나온 개념
  - 상위 클래스(부모 클래스)의 메소드를 하위 클래스(자식 클래스)에서 재정의


# 2. Interface, Abstract

- interface랑 abstract 사용하는 이유
  - 객체는 상태와 행동을 의미한다.
  - 동물 객체는 특별한 무언가를 지칭해서 한것이 아니다.
  - 특정 생명체(?)들을 가지고 이런 경우에는 동물이라고 하자! 한 것들이 동물이다.
  - 즉 불완전한 것들이다.
  - 그런것들을 interface와 abstract로 만든느 것이다.

- Interface
  - 특정 method 강제시키는 게 목적이다.
  - 일종의 추상 클래스
  - 오직 추상메서드와 상수만을 멤버로 갖는다.
  - 구현 객체와 같은 동작 보장
  - 상속의 관계가 없는 클래스간 서로 공통되는 로직을 구현하여 쓸 수 있도록한다.
  - Implement 키워드
  - 인터페이스는 생성자를 선언할 수 없다.

- Abstract
  - 대상이 두가지가 있다.
    - class
    - method

  - abstract class
    - 클래스 내에 추상메서드가 선언되어 있음을 의마한다.
  - abstract method
    - 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드

  - 추상 클래스를 상속받은 클래스는 추상 클래스가 갖고 있는 추상 메소드를 반드시 구현해야 한다.
    - @Override 사용
    - 추상 클래스를 상속받고, 추상 클래스가 갖고 있는 추상 메소드를 구현하지 않으면 해당 클래스도 추상 클래스가 된다.

  - 상속 받아서 기능 확장
  - extends 키워드
  - 객체를 생성할 수 없다.
  - 생성자를 선언할 수 있다.(그렇지만 생성자를 직접 호출하여 객체를 생성할 수는 없다. super() 메소드를 이용),


그런데 JPA에서는 직접 entity attribute에 intntity attribute에 interface불가능

directly mapping interfaces as an entity attribute is not supported by JPA.

You can only map top level classes directly annotated with @Entity. This top level class may implement an interface though.

This feature has been requested and discussed for a long time.

Also take a look at this and this.

Depending on what you're trying to accomplish, @Inheritance annotation with table-per-class strategy could be an option.


출처: https://stackoverflow.com/questions/12627607/jpa-entity-with-a-interface-attribute-is-it-possible



# 3. Call by Reference, Call by Value
- Call by Reference
  - 매개 변수의 원래 주소에 값을 저장하는 방식. 클래스 객체를 인수로 전달한 경우
- Call by Value
  - 인수로 기본 데이터형을 사용. 주어진 값을 복사하여 처리하는 방식. 메서드 내의 처리 결과는 메서드 밖의 변수에 영향을 미치지 않는다.


# 4. Static의 의미
- 클래스가 로딩될 때, 메모리 공간을 할당하는데 처음 설정된 메모리 공간이 변하지 않음을 의미
- 객체를 아무리 많이 만들어도 해당 변수는 하나만 존재(객체와 무관한 키워드)


## 4-1. static 변수(정적 변수)
- 선언된 함수 내에서만 사용 가능
- 프로그램이 시작될 때 생성 및 초기화
- 프로그램 종료 시 까지 메모리 공간 존재


# 5. Garbage Collection(가비지 컬렉션)
시스템에서 더이상 사용하지 않는 동적 할당된 메모리 블럭을 찾아 자동으로 다시 사용 가능한 자원으로 회수하는 것으로
시스템에서 가비지컬렉션을 수행하는 부분을 가비지 컬렉터라 부른다.


# 6. Primitive type vs Reference type
- JAVA Primitive, Reference Type은 메모리 저장 방식이 다릅니다.
- JAVA에 call-by-reference는 없습니다. pass-by-value reference 정보를 가진 객체가 복사됩니다.

- Primitive type
  - <b>변수에 값 자체를 저장</b>
  - Primitive Type 마다 사용하는 메모리 사이즈가 fix 되어있습니다.
  - 종류
    - 정수형 byte, short, int, long
    - 실수형 float, double
    - 문자형 char
    - 논리형 boolean
  - primitive type은 javaVM에서 지원하는 비객체형 타입.
  - 비객체형 타입은 객체형 타입은 아니지만 예외적으로 지원을 해야하는 기본형 타입.
  - 자바에서 사용하는 메소드를 통해서 사용이 불가능하다.
  - 자바에서 기본형으로 사용가능하지만 객체로는 가공할 수 없다.
  - primitive type은 stack영역에서 생성,종료

*Primitive type은 Wrapper Class를 통해 객체로 변형할 수 있다.
예) int→Integer, char→Character(int와 char를 제외한 Primitive type의 다른 자료형들은 맨 앞 알파벳을 대문자로 바꿔주면 된다. float→Float)*

- Reference type
  - <b>메모리상에 객체가 있는 위치를 저장</b>
  - 기본 1Byte + @ (class variable size의 합)의 메모리를 사용합니다.
  - 종류
    - Class, Interface, Array 등
  - reference type은 java에서 최상인 Object클래스를 상속하는 모든 클래스이다.
  - 물론 new로 인하여 생성하는 것들은 메모리영역인 heap영역에 생성을 하게 되고, garbage collector라는 곳에 등록하게 되서 버려진다.


*String*  
- String은 좀 독특한 존재이다.
- String은 reference Type 입니다.
- String은 제임스 고슬링이 char의 array라 했다.
- String은 String constant pool을 이용한 메모리 관리 합니다. 리터럴 방식으로 생성하면 컴파일러가 효율적으로 사용할수 있게 해줍니다.

참고자료 : https://againsee.com/2018/06/15/java-datatype/


# 7. string과 char 차이
char 는 단일 문자
String 은 문자 배열
char 는 java의 기본 유형이고 String 은 chars 배열을 캡슐화하는 클래스


# 8. Wrapper Class
Primitive type으로 표현할 수 있는 간단한 데이터를 객체로 만들어야 할 경우가 있는데 그러한 기능을 지원하는 클래스


# 9. 접근제한자(public > protected > default > private)
public - 접근 제한이 없다.(같은 프로젝트 내에 어디서든 사용가능)
protected - 같은 패키지 내, 다른 패키지에서 상속받아 자손클래스에서 접근 가능
default - 같은 패키지 내에서만 접근 가능
private - 같은 클래스 내에서만 접근 가능


# 10. Java에서 OOP컨셉 및 원리는 무엇이 있는가?
- 4가지가 있습니다.
  - Abstraction(추상화)
  - Encapsulation(캡슐화)
  - Inheritance(상속)
  - Polymorphism(다형성)  


## 10-1. Polymorphism(다형성)란?
- 다형성이란 상위클래스 타입의 변수에 여러개의 하위클래스의 객체를 참조할 수 있도록 하는것
- 즉 같은 타입이지만 오른쪽에 실제 런타임중에 new되는 객체(하위클래스)의 메소드가 실행되어 동일한 메소드가 다양한 형태를 표출한다는 것 이다.

### 10-1-1. 다형성의 장점?
- 여러 타입의 객체를 하나의 타입으로 관리하니 유지보수가 좋다.
- 메속드의 매개변수(인자)로 상위 클래스, 추상 클래스, 인터페이스등이 온다면 그 하위클래스, 인터페이스를 구현한 클래스등이 인자로 들어 갈 수 있어 좀 더 유연한 프로그래밍을 할 수 있다.
- 확장성이 좋은 코드를 작성할 수 있고, 결합도가 강하지 않은 프로그래밍을 할 수 있다.


## 10-2. Abstraction(추상화)란?
- 일상생활 예제


# 12. 객체와 클래스의 차이점에 대해 설명해 보시오.
- 클래스(Class)
  - 현실 세계의 객체의 속성과 동작을 추려내 필드와 메서드로 정의한 것으로 "아직 메모리가 할당되지 않은 상태"
- 객체(Object)
  - Class라는 설계도를 기반으로 실제 메모리가 잡힌 것을 의미하며 이런 객체를 조합해 전체 프로그램을 완성해 나가는 방식을 OOP(객체지향 프로그래밍)이라고 한다.


# 13. 캡슐화, 은닉화란?
외부 객체에서 구현방식은 알 수 없도록 숨기고 별도로 접근할 수 있는 getter/setter 메서드를 통해 접근하도록 하는 방식


# 14. 상속이란?
부모 Class를 자식이 접근할 수 있도록 하는 것


# 15. 자바의 메모리 영역
- 메서드 영역
  - static 변수, 전역변수, 코드에서 사용되는 Class 정보 등이 올라간다.
  - 코드에서 사용되는 class들을 로더로 읽어 클래스별로 런타임 필드데이터, 메서드 데이터 등을 분류해 저장한다.
- 스택(Stack)
  - 지역변수, 함수(메서드) 등이 할당되는 LIFO(Last In First Out) 방식의 메모리
- 힙(Heap)
  - new 연산자를 통한 동작할당된 객체들이 저장되며, 가비지 컬렉션에 의해 메모리가 관리되어 진다.


# 16. 인터페이스(Interface)란? 또 왜 사용하나?
모든 메서드가 구현부가 없는 추상메서드로 이루어진 클래스로, abstract 키워드를 붙이지 않아도 자동으로 모든 메서드는 추상메서드로 정의


# 17. 왜 인터페이스를 사용하는가?
:팀작업시 개발코드 부분과 객체가 서로 통신하는 접점 역할을 지원하게 되는데, 이는 개발코드에선 객체의 내부 구조를 모르더라도 인터페이스의 메서드 명만 알고 있으면 되기 때문이다.
이를 통해 얻을 수 있는 장점은 해당 메서드를 통해 나오는 결과물을 알고 있기 때문에 다른 팀의 작업을 기다리고 있지 않아도 되며, 또한 해당 객체가 수정될 경우 개발 코드 부분은 수정을 하지 않아도 된다.
또한, 부가적으로 객체를 파일에 쓰기 위해 Serializable 인터페이스를 구현하거나, Collections.sort()를 하기 위해서 Comparable 인터페이스를 상속하는 것, Cloneable 을 구현하는 것처럼 특정 작업을 하겠다라는 "Mark"역할을 해주기도 한다.


# 18. Wrapper Class의 사용이유를 아나요?
기본 data 타입은 객체가 아니어서 Object로 받는 다형성을 지원할 수가 없다. 하지만, 메서드에서 실재로 기본데이터 타입을 다형성으로 넘겨주어야 하는 경우가 빈번히 발생하는데 이때, 기본 데이터 타입을 객체로 변환시켜 전달하기 위해 사용되며 최근에는 AUTO Boxing, AUTO UnBoxing이 지원된다.


# 19. 자바의 제네릭이란??
클래스 내부에서 사용할 데이터 타입을 인스턴스(객체) 생성시에 결정짓는 방식

# 20. 함수 vs method?
함수: 특정 작업을 수행하는 코드조각으로 독립된 기능을 수행하는 단위 *함수가 method를 포함한다*
method: 클래스, 구조체, 열거형에 포함되어 있는 *함수*


# 21. 구조체?
> [java에 없는 것이지만 따로 빼는게 애매해서 넣었다.]

구조체란 하나 이상의 연관성 있는 변수를 묶어 새로운 자료형을 정의 하는 것.

``` c
struct point    // point라는 이름의 구조체 선언
{                 // 구조체 정의
    int x;       // 구조체 멤버 int x
    int y;      // 구조체 멤버 int y
}
```

# 22. 인스턴스란?
> 클래스로부터 객체를 만드는 과정을 클래스의 인스턴스화

클래스로부터 만들어진 객체를 그 클래스의 인스턴스라고 합니다.

인스턴스 생성법
``` java
Car a = new Car();
```


# 23. JAVA SE (Java Platform Standard Edition) vs JAVA EE (Java Platform EnterPrise Edition)

- JAVA SE  
  - 표준 자바 플랫폼.
  - JAVA의 프로그래밍을 할 때 주로 사용하는 거의 모든 기술들의 core들이 있다고 생각하면 된다.(ex. networking, security, database access, gui etc...)  
  - 또 SE platform의 코어 API에는 virtual machine, development tools,  deployment technologies, 그리고 other class libraries 그리고 Java technology applications에서 기본으로 사용하는 toolkits 들이 구성을 이루고 있다.  


- JAVA EE  
  - JAVA SE에 서버측을 위한 기능을 부가하였기 때문에 SE기능을 모두 포함한다.  
  - The Java EE platform provides an API and runtime environment for developing and running large-scale, multi-tiered, scalable, reliable, and secure network applications.


# 24. long 과 Long의 차이
Java 에서 long 은 primitive type, 즉, 원시형 데이터로 클래스가 아니다.
long 은 64bit 정수값을 표현하는 데이터 타입으로 8byte 의 메모리 공간을 사용한다.
Long 은 long 과 마찬가지로 64bit 정수 값을 표현하지만 이것은 클래스다.


# 25. 자바의 특징에 대해 말해보시오.

- OOP(객체 지향 언어)
- "가비지 컬렉션"에 의한 메모리 자동 관리
- "멀티 쓰레드"를 지원한다.
- JVM 위에서 동작하기 때문에 특정 OS에 종속적이지 않고 이식성이 좋으며, 보안성이 좋다.
- 다양한 Open 라이브러리들이 존재한다.


# 26. 자바의 JVM의 역할에 대해서 설명해 보시오.


# 27.
<!--

5. Framework
- 특정 형태의 소프트웨어 문제를 해결하기 위해 상호 협력하는 클래스프레임과 인터페이스 프레임의 집합
- 특정한 틀을 만들어놓고 거기에 살을 붙여 놓음으로써 프로그램을 만들어 작업시간을 줄여주는 것이다.
- 프레임워크는 특정 개념들의 추상화를 제공하는 여러 클래스나 컴포넌트로 구성된다.
- 프레임워크는 이렇게 추상적인 개념들이 문제를 해결하기 위해 같이 작업하는 방법을 정의한다.
- 프레임워크 컴포넌트 들은 재사용이 가능하다.
- 프레임워크는 좀 더 높은 수준에서 패턴을 조작한다.
* 프레임워크가 중요한 이유는 객체지향 개발을 하게 되면서 개발자의 취향에 따라 다양한 프로그램이 나오게 되었다.
 프로그램 개발에 투입되는 개발자도 점점 늘어남에 따라 전체 시스템의 통합성, 일관성이 부족하게 되었기 때문이다.
 그래서 개발자의 자유를 제한하기 위해 프레임워크를 도입했다.

프레임워크가 가져야할 특징
a. 개발자들이 따라야할 가이드라인을 가진다.
b. 개발할 수 있는 범위가 정해져 있다.
c. 개발자를 위한 다양한 도구들이 지원된다.

프레임워크의 장/단점
장점 - 개발 시간을 줄일 수 있고 오류로부터 자유로울 수 있다.
단점 - 프레임워크에 너무 의존하면 개발 능력이 떨어져서 프레임워크 없이 개발하는 것이 불가능해지는 점이다.







자바의 메모리 영역(간단하게 설명)



1. 메서드 영역 : static 변수, 전역변수, 코드에서 사용되는 Class 정보 등이 올라간다.코드에서 사용되는 class들을 로더로 읽어 클래스별로 런타임 필드데이터, 메서드 데이터 등을 분류해 저장한다.

2. 스택(Stack) : 지역변수, 함수(메서드) 등이 할당되는 LIFO(Last In First Out) 방식의 메모리

3. 힙(Heap) : new 연산자를 통한 동작할당된 객체들이 저장되며, 가비지 컬렉션에 의해 메모리가 관리되어 진다.



인터페이스(Interface)란? 또 왜 사용하나?

인터페이스는 모든 메서드가 구현부가 없는 추상메서드로 이루어진 클래스로, abstract 키워드를 붙이지 않아도 자동으로 모든 메서드는 추상메서드로

정의가 된다. 또한 변수도 자동으로 final static 키워드가 붙게 된다.



– 메모리 상수풀 영역 이란

힙영역(프로그래머가 관리하는 메모리 영역)에 생성되어 자바 프로세스 종료까지 계속 유지되는 메모리영역입니다. 기본적으로 JVM에서 관리하며 프로그래머가 작성한 상수에 대해 최우선적으로 찾아보고 없으면 상수풀에 추가한 이후 그 주소값을 리턴합니다. 그로 인해 메모리 절약 효가가 있습니다.




직렬화란 무엇인가



자바에서 입출력에 사용되는 것은 스트림이라는 데이터 통로를 통해 이동했습니다. 하지만 객체는 바이트형이 아니라서 스트림을 통해 파일에 저장하거나 네트워크로 전송할 수 없습니다. 따라서 객체를 스트림을 통해 입출력하려면 바이트 배열로 변환하는 것이 필요한데, 이를 '직렬화' 라고 합니다. 반대로 스트림을 통해 받은 직렬화된 객체를 원래 모양으로 만드는 과정을 역직렬화라고 합니다.



리플렉션이란 무엇인가요






출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]


자바의 클래스 멤버 변수 초기화 순서에 대해서 설명하라.



1. static 변수 선언부 : 클래스가 로드 될 때 (메모리 모델상 Methd area 에 올라감) 변수가 제일 먼저 초기화 됨



2. 필드 변수 선언부 : 객체 생성 될 때 (메모리 모델상 Heap area에 올라감) 생성자 block 보다 앞서 초기화 함



3. 생성자 block : 객체 생성 될 때 (메모리 모델상 Heap area에 올라감)

JVM이 내부적으로 locking (thread safe 영역임)

필드 변수 중 final 변수의 가시화는 (다른 스레드에 공개하는 시점은) 생성자 block이 끝난 다음.

필드 변수 선언부에서 이미 초기화 되었다면 그 값들은 덮어 씀



초기화 시점

    * 클래스변수의 초기화시점 : 클래스가 처음 로딩될 때 단 한번 초기화 된다.

    * 인스턴스변수의 초기화시점 : 인스턴스가 생성될 때마다 각 인스턴스별로 초기화가 이루어진다.



초기화 순서

    * 클래스변수의 초기화순서 : 기본값 -> 명시적초기화 -> 클래스 초기화 블럭

    * 인스턴스변수의 초기화순서 : 기본값 -> 명시적초기화 -> 인스턴스 초기화 블럭 -> 생성자



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]

제너릭



클래스를 선언할 때 타입을 결정하지 않고 객체를 생성할 때 유동적인 타입으로 재사용하기 위한 것

형변환을 할 필요없고, 타입 에러가 발생할 확률이 없어진다.



타입추론은 메서드를 호출하는 코드에서 타입인자가 정의한대로 제대로 쓰였는지 살펴보는 컴파일러의 능력이다.



컬렉션(collection) 클래스에서 제네릭을 사용하는 이유를 설명하시오.



컬렉션 클래스에서 제네릭을 사용하면 컴파일러는 특정 타입만 포함 될 수 있도록 컬렉션을 제한합니다.

컬렉션 클래스에 저장하는 인스턴스 타입을 제한하여 런타임에 발생할 수 있는 잠재적인 모든 예외를 컴파일타임에 잡아낼 수 있도록 도와줍니다.



pojo란 무엇인가



Plain Old Java Object. 간단히 포조 라는 말 그대로 해석하며 ㄴ오래된 방식의 자바 오브젝트로서 J2EE등의 중량 프레임워크들을 사용하면서 해당 프레임워크에 종석된 무거운 객체를 만들게 된 것에 반발하여 특정 자바 모델이나 기능, 프레임워크 등을 따르지 않는 자바 오브젝트를 지칭하는 말로 사용되었다.



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]

상속과 합성(컴포지션)의 차이에 대해서 설명해 주세요.  

상속은 is a 관계

컴포지션은 개체들 간에 has a 관계이다.



상속은 클래스를 확장하여 부모 클래스에서 속성 및 동작을 상속하는 기능입니다.

자동차는 자동차다.

class Engine{}

abstract class Automobile{}



class car extends Automobile{

	private Engine engine;

}



합성은 클래스가 구성원 데이터로 다른 클래스의 객체를 포함 할 수있는 능력입니다.

자동차는 엔진이 포함되어 있다.



JVM 의 역할은 무엇인지 설명해 보세요.



JVM(Java virtual machine)은 자바를 실행하기 위한 가상 기계라고 할 수 있습니다. 여기서 가상 기계란 말이 어색하다면 프로그램을 실행하기 위해 물리적 머신과 유사한 머신을 소프트웨어로 구현한 것이라고 해석할 수 있습니다.

JVM은 Java Byte Code를 OS에 맞게 해석해주는 역활을 합니다. Java Compiler가 *.java 파일을 컴피알을 하면 .class라는 java byte code로 변환시켜 주며, Byte Code는 기계어가 아니기 때문에 OS에서 바로 실행이 되지 않습니다. 이 때 JVM이 OS가 이해할 수 있도록 해석해줍니다



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]


스프링 mvc
MVC 구성요소

Model - 소프트웨어 응용과 그와 관련된 고급 클래스 내의 논리적 데이터 기반 구조를 표현. 이 목적 모형은 사용자 인터페이스에 관한 어떠한 정보도 가지고 있지 않다.

View - 사용자 인터페이스 내의 구성요소들을 표현(사용자에게 보여지는 화면)

Controller - Model과 View를 연결하고 있는 클래스를 대표, Model과 View 내의 클래스들 간 정보 교환하는데 사용.

Spring Framework(스프링 프레임워크)



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]


Spring의 AOP란?


AOP는 Aspect Oriented Programming 관점 지향 프로그래밍의 약자로, 기존의 OOP(객체 지향 프로그래밍)에서 기능별로 class를 분리했음에도 불구하고, 여전히 로그, 트랜잭션, 자원해제, 성능테스트 메서드 처럼 공통적으로 반복되는 중복코드가 여전히 발생하는 단점을 해결하고자 나온 방식으로 이러한 공통 코드를 "횡단 관심사"라 표현하며 개발코드에서는 비지니스 로직에 집중하고 실행시에 비지니스 로직 앞, 뒤 등 원하는 지점에 해당 공통 관심사를 수행할 수 있게 함으로서 중복 코드를 줄일 수 있는 방식입니다.


Spring에서 DI란 무엇인지 아시나요?


DI는 Dependency Injection(의존성 주입)의 약자로, 객체들 간의 의존성을 줄이기 위해 사용되는 Spring의 IOC 컨테이너의 구체적인 구현 방식입니다.

DI는 기존처럼 개발코드 부분에서 객체를 생성하는 것이 아니라, 팩토리 패턴처럼 객체의 생성과, 데이터를 주입만 담당하는 Factory에 해당 하는 별도의 공간에서 객체를 생성하고 데이터간의 의존성을 주입해 개발코드에서는 이를 가져다 씀으로서 의존성을 줄이는 방식입니다. 이때,

Factory 패턴의 Factory Class의 역할을 스프링의 환경설정 파일이 담당합니다.



설정 파일을 통해 객체간의 의존관계를 설정함으로써 외부 Assembler가 객체간의 의존 관계를 정의하게 되며, 객체는 직접 의존하고 있는 객체를 생성하거나 검색할 필요가 없어지므로 코드의 관리가 쉬워진다.



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]

IOC란 무엇인가



인스턴스 생성의 제어를 개발자 본인이 아닌 다른 누군가에게 반환해 준다는 개념으로 여기서 말하는 다른 누군가는 Servlet과 같은 bean을 관리해주는 컨테이너이다.

즉 IOC란 인스턴스의 생성부터 소멸까지 개발자가 아닌 컨테이너가 대신 관리해준 다는 것이다.



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]

DAO

Data Access Object의 약자로 간단히 Database의 data에 접근을 위한 객체입니다. Database에 접근을 하기위한 로직과 비즈니스 로직을 분리하기 위해서 사용을 합니다

DAO(Data Access Object)는 DB를 사용해 데이터를 조화하거나 조작하는 기능을 전담하도록 만든 오브젝트를 말한다.



DTO

DTO(Data Transfer Object)는 VO(Value Object)로 바꿔 말할 수 있는데 계층간 데이터 교환을 위한 자바빈즈를 말합니다.여기서 말하는 계층간의 Controller, View, Business Layer, Persistent Layer를 말하며 각 계층간 데이터 교환을 위한 객체를 DTO 또는 VO라고 부릅니다. 그런데 VO는 DTO와 동일한 개념이지만 read only 속성을 가짐



출처: https://ktko.tistory.com/entry/개발자-면접-질문자바-스프링 [KTKO 개발 블로그와 여행 일기]


23) Wrapper Class의 사용이유를 아나요?

: 기본 data 타입은 객체가 아니어서 Object로 받는 다형성을 지원할 수가 없다. 하지만, 메서드에서 실재로 기본데이터 타입을 다형성으로

 넘겨주어야 하는 경우가 빈번히 발생하는데 이때, 기본 데이터 타입을 객체로 변환시켜 전달하기 위해 사용되며

 최근에는 AUTO Boxing, AUTO UnBoxing이 지원된다.



출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]
21) 오버로딩과 오버라이딩의 차이?

- 오버로딩 : 메서드 명은 동일하지만, 매개 변수 타입과 개수를 다르게 해 선언하는 방식

- 오버라이딩 : 상속한 자식에서 부모의 메서드를 재정의하는 방식



출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]
18) 디자인 패턴 아는 것?

1) 싱글톤(SingleTone Pattern) : 대표적으로 Calendar 객체나 dataSource 객체처럼 객체가 하나만 생성되어야 하는 경우

 전체 코드에서 하나의 객체만 존재할 수 있도록 이미 생성된 객체가 있으면 그 객체를 사용하도록 하는 방식입니다.

2) 팩토리 패턴(Factory pattern) : 객체간 의존성을 줄이기 위해 객체의 생성과 데이터 주입만 담당하는 Factory Class를 정의하고 개발 코드 부분에서는

   생성된 객체를 가져다 사용함으로서 의존성을 줄이는 방식입니다.

3) 옵저버 패턴(Observer Pattern) : 기후 정보처럼 RSS 수신시 하나의 객체가 변하면 다른 객체에 객체가 변했다는 사항을 알려주어야 할 경우에 주로

    사용됩니다.



출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]

12) 캐시(Cache)와 세션(Session)의 공통점과 차이점은?

- 공통점 : 둘 다 사용자의 데이터를 저장한다.

- 차이점

- 캐시 : 캐시는 Client 컴퓨터에 저장했다 서버 요청시 네트워크를 타고 서버로 전달되기 때문에 보안에 취약하다.

- 세션 : 세션은 서버에 저장되고 브라우저 단위로 관리된다. 캐시에 비해 보안성이 좋다.



출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]


11) 컬렉션프레임워크(CollectionFramework)에 대해 아는만큼 말해 보시오.



- Collection 인터페이스

- List 인터페이스 : 배열과 유사하되, 추가할때마다 자동으로 Boundary를 늘려주는 구조로, 중복된 데이터를 허용하며, 순서가 존재한다.

ex) - ArrayList : 배열로 구현됬으며, 인접해 있기 때문에 데이터 조회에 매우 빠르다 하지만, 빈번한 삽입, 삭제시 새로 배열을 만들고 데이터를

옮겨야 하기 때문에 LinkedList에 비하여 속도가 느리다.

    - LinkedList : 링크 구조로 되어 있기 때문에 조회는 ArrayList에 비해 느리지만, 삽입 삭제시 링크를 끊고 새로 추가되는 데이터에 링크만

연결하면 되기 때문에 삽입, 삭제에 유리하다.

    - Vector : 구현 방식은 ArrayList와 유사하지만 Vector를 개선한 것이 ArrayList이다. 또한 Vector의 경우에는 ArrayList와 달리

Synchronized(동기화)가 걸려 있어 여러 쓰레드에서 동시에 접근할 수 없다.

- Set 인터페이스 : 집합처럼 중복된 데이터를 허용하지 않으며, 순서가 없다. 또한, 객체 내부의 중복된 데이터를 배제하고 싶은 경우

  Object 클래스의 equals 메서드와 hashCode 메서드의 재정의가 반드시 필요하다.

ex) - HashSet

    - TreeSet : 순서가 있는 HashSet으로 이진 트리 구조로 만들어 졌다. 순서에 맞게 정렬되어 저장되기 위해서 Comparable을 구현해야한다.





- Map 인터페이스 : key와 value 쌍으로 데이터를 저장하며, key는 중복될 수 없고, value는 중복 저장이 가능하다.

ex) - HashMap

     - TreeMap

     - Properties : key value 쌍으로 저장되지만 value의 타입이 String만 가능하다.

     - Hashtable : HashMap과 구조는 같으며, 단지 Synchronized(동기화) 되어져 있다는 점이 다른점이다.



출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]


3) 변수란?

: "하나의 값을 저장할 수 있는 메모리 공간"

직렬화(Serialize)
자바 시스템 내부에서 사용되는 Object 또는 Data를 외부의 자바 시스템에서도 사용할 수 있도록 byte 형태로 데이터를 변환하는 기술.
JVM(Java Virtual Machine 이하 JVM)의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 바이트 형태로 변환하는 기술
역직렬화(Deserialize)
byte로 변환된 Data를 원래대로 Object나 Data로 변환하는 기술을 역직렬화(Deserialize)라고 부릅니다.
직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태.


출처: https://js2prince.tistory.com/entry/java-경력-기술-면접-질문-리스트 [개발은 전투다]
-->


---
참고링크:
http://rongscodinghistory.tistory.com/m/44  
http://hahahoho5915.tistory.com/16 [넌 잘하고 있어]  
https://yolojeb.tistory.com/20 [개발 일기]  

6번 참고:
https://inetizenseo.tistory.com/12

21번 구조체에 대한 설명  
http://knkky.tistory.com/53 [남깐느]  
(23번 참고)  
https://www.ibm.com/support/knowledgecenter/ko/SSQP76_8.9.1/com.ibm.odm.dserver.rules.res.managing/topics/con_javase_javaee_applis.html   
https://docs.oracle.com/javaee/6/firstcup/doc/gkhoy.html  
24번 출처: https://yjacket.tistory.com/63
