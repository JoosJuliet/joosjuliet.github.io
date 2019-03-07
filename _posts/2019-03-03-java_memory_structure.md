---
layout: post
section-type: post
title: "인스턴스의 생성과 사용"
category: OOP
tags: [ 'java', 'oop' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

# 인스턴스의 생성과 사용

```

클래스명 변수명;      // 클래스의 객체를 참조하기 위한 참조변수를 선언한다.
변수명 = new 클래스명(); // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장한다.

Tv t;                   // Tv클래스 타입의 참조변수 t를 선언
t = new Tv();       // Tv인스턴스를 생성한 후, 생성된 Tv인스턴스의 주소를 t에 저장한다.

```

[예제6-1] TvTest.java

``` java

class TvTest {
    public static void main(String args[]) {
          Tv t;                         // Tv인스턴스를 참조하기 위한 변수 t를 선언       
          t = new Tv();             // Tv인스턴스를 생성한다.
          t.channel = 7;             // Tv인스턴스의 멤버변수 channel의 값을 7로 한다.
          t.channelDown();             // Tv인스턴스의 메서드 channelDown()을 호출한다.
          System.out.println("현재 채널은 " + t.channel + " 입니다.");
    }
}

```

```

[실행결과]
현재 채널은 6 입니다.

```
한줄씩 설명해 보겠습니다.


## 1. Tv t;
Tv 클래스 타입의 참조변수 t 선언,
메모리에 참조변수 t를 위한 공간 마련된다.
(in stack)
![1](/images/2019-03-03-java_memory_structure/1.gif)

## 2. t = new Tv();
![jvm구조](/images/2019-03-03-java_memory_structure/jvm.png)
*참고로 Heap에 저장된 데이터가 더 이상 사용이 불필요하다면 메모리 관리를 위해 JVM(자바 가상머신)에 의해 알아서 해제된다. 이러한 기능을 가비지컬렉션(GC, 쓰레기 수집)이라고 한다.*

연산자 new에 의해 Tv 클래스의 인스턴스가 메모리의 빈 공간에 생성된다.(in heap)
주소가 0x100인 곳에 생성되었다(가정)
맴버변수는 각 자료형에 해당하는 기본값으로 초기화
- color는 참조형이므로 null, power는 boolean이므로 false로, 그리고 channel은 int이므로 0으로 초기화
![2](/images/2019-03-03-java_memory_structure/2.gif)

그 다음에는 대입연산자(=)에 의해서 생성된 객체의 주소값이 참조변수 t에 저장된다. 이제는 참조변수 t를 통해 Tv인스턴스에 접근할 수 있다. 인스턴스를 다루기 위해서는 참조변수가 반드시 필요하다.

![3](/images/2019-03-03-java_memory_structure/3.gif)


[참고]위 그림에서의 화살표는 참조변수 t가 Tv인스턴스를 참조하고 있다는 것을 알기 쉽게 하기 위해 추가한 상징적인 것이다. 이 때, 참조변수 t가 Tv인스턴스를 '가리키고 있다' 또는 '참조하고 있다'라고 한다.

## 3. t.channel = 7 ;
참조변수 t에 저장된 주소에 있는 인스턴스의 멤버변수 channel에 7을 저장한다.
여기서 알 수 있는 것처럼, 인스턴스의 멤버변수(속성)를 사용하려면 '참조변수.멤버변수'와 같이 하면 된다.
![4](/images/2019-03-03-java_memory_structure/4.gif)


## 4. t.channelDown();
참조변수 t가 참조하고 있는 Tv인스턴스의 channelDown메서드를 호출한다. channelDown메서드는 멤버변수 channel에 저장되어 있는 값을 1감소시킨다.
``` java

void channelDown() {       --channel;             }

```
channelDown()에 의해서 channel의 값은 7에서 6이 된다.
![5](/images/2019-03-03-java_memory_structure/5.gif)


# 결론
인스턴스와 참조변수의 관계는 마치 우리가 일상생활에서 사용하는 TV와 TV리모콘의 관계와 같다. TV리모콘(참조변수)을 사용하여 TV(인스턴스)를 다루기 때문이다. 다른 점이라면, 인스턴스는 오직 참조변수를 통해서만 다룰 수 있다는 것이다.


---
참고문헌 :
JAVA의 정석
https://m.blog.naver.com/PostView.nhn?blogId=endlessshow&logNo=47440638&proxyReferer=https%3A%2F%2Fwww.google.com%2F
https://m.blog.naver.com/PostView.nhn?blogId=heartflow89&logNo=220954420688&proxyReferer=https%3A%2F%2Fwww.google.com%2F
