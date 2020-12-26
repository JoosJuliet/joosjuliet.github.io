---
layout: post
section-type: post
title: "6주차 과제: 상속"
category: Java
tags: [ 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

일단 이번 과제의 주제인 상속에 대해서 먼저 정리를 해봐야겠다.
- 상속
  - 기존의 클래스를 다양한 형태로 확장 할 수 있게 도와주는 개념
  - 서브 클래스와 슈퍼 클래스라는 계층 구조를 생성
  - 상속을 잘 사용할 수 있게 도와주는 개념들
    - 서브 클래스가 부모 클래스를 대신하여 작업하는 것을 가능하게 해주는 다형성
    - 클래스 속의 값들을 내부에서만 관리 할 수 있게 하는 캡술화


# 자바 상속의 특징
- 상속은 단일 상속
  - 아래와 같은 예제는 안된다.
```
class A extends B, C{}
```
- 자바의 계층 구조 최상위에는 java.lang.Object 클래스
- 부모의 메소드와 변수만 상속되며, 생성자는 상속 x
- 상속의 계층은 무한대
```
class A{};
class B extends A{};
class C extends B{};
class D extends C{};
class E extends D{};
```





# super 키워드
class의 상속을 하면 해당 클래스의 인스턴스를 만들 때, 부모 클래스의 인스턴스가 내재적으로 만들어진다.  
즉 언제든지 부모 클래스의 값들을 가져올 수 있는 연결고리가 생성된다.  
그 연결고리를 이어주는 것이 바로 super 키워드이다.  

- super 참조변수 및 메소드 호출
  - 자식클래스가 부모클래스로부터 상속받을 메소드나 필드를 명시적으로 참조를 위해 사용
``` java
class Parent{
   int tall = 190;
   void sing(){System.out.println("hi i'm tall too");}
}

class Child extends Parent{
    int tall = 180;
    void message(){
      System.out.println("hi i'm tall");
    }
    void display(){
      message(); // 현재 클래스 메세지() 메소드가 호출 됨
      super.message(); // 부모 클래스 메세지 () 메소드가 호출 됨

    }

    void childMethod(){
           System.out.println(tall);         // 180
           System.out.println(this.tall);     // 180
           System.out.println(super.tall);   // 190
           display()
           //"hi i'm tall too" "hi i'm tall"
    }
}
```
- super method
  - ```super()```는 부모 클래스 생성자를 즉시 호출 할 때 사용
  - 자식 클래스가 자신을 생성할 때 부모 클래스의 생성자를 불러 초기화 할때 사용된다.
``` java
class Parent{
  Parent(){System.out.println("Parent is created");}
}

class Child extends Parent{

  Child(){
    super(); // 부모 클래스 생성자가 호출
    System.out.println("Child is created");
  }

  public static void main(String args[]){
    Child c = new Child();
  }
}   
```
output :
``` shell
"Parent is created"
"Child is created"
```

컴파일러에 의해 super ()는 자동으로 각 클래스 생성자에 추가



# 메소드 오버라이딩
오버라이딩은 부모의 함수를 재정의하는 기능이고, 함수명, 리턴값, 파라미터가 모두 동일해야한다.



## 메소드 오버로딩(Overloading)
이름도 비슷하고 둘 다 다형성을 만드는데 사용하기 때문에 은근 말이 헷갈리기도 하다 ㅋㅋ
public class A {
     public void print(){
           System.out.println("A");
     }

     public void print(int a){
           System.out.println("A" + "_" + a);
     }

     public void print(int a, int b){
           System.out.println("A" + "_" + a + "_" + b);
     }
}
- 위 예제가 오버로딩을 구현한 것
- 오버로딩은 메소드와 리턴값은 같지만 매개변수가 다른 것을 의미한다. 만약 매개변수의 타입이 달라져도 오버로딩이 성립






# 추상 클래스
추상 클래스는 클래스를 만들기 위한 일종의 설계도로 인스턴스를 생성할 수 없는 클래스



# final 키워드

- final 변수
  - final 변수는 우리가 흔히 아는 상수를 의미합니다. 생성자나 대입연산자를 통해 한번만 초기화 가능한 변수
- final 메소드
  - final 메소드는 오버라이드 x
- final 클래스
  - 해당 클래스를 상속할 수 없게 하고 싶을 때 사용
​



# Object 클래스

Class Object는 클래스 계층 구조의 루트이다.  
마치 기본적으로 `class 클래스명 extends Object` 이렇게 기본적으로 되어있다고 보면 된다.  


## Object의 기본 method들
모든 클래스에는 Object가 수퍼 클래스로 있기에, 모든 객체는 이 클래스의 메서드를 상속해서 구현한다.  
  - boolean equals(Object obj)
  - String toString()
  - protected Object clone()
  - protected void finalize()
  - Class getClass()
  - int hashCode()
  - void notify()
  - void notifyAll()
  - void wait()
  - void wait(long timeout)
  - void wait(long timeout, int nanos)

### 예제
``` java

public static void main(String[] args) {
    Army korean = new Army(27);
    Army american = new Army(27);
    System.out.println(korean.equals(american));
}

public static class Army {
    private int age;

    public Army(int age) {
        this.age = age;
    }
}
```

print 되는 것

``` shell
false
```

원래라면 User 클래스 속 equals method가 없어서 컴파일 에러가 나야한다고 생각할 수 있다.  
그러나 Object 클래스를 상속받기에 나지 않는다.  
