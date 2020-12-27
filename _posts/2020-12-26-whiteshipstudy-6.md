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
    - 클래스 속의 값들을 내부에서만 관리 할 수 있게 하는 캡슐화

# 자바 상속의 특징
- 상속은 단일 상속
  - 아래와 같은 예제는 안된다.
```
class A extends B, C{}
```
- 자바의 계층 구조 최상위에는 java.lang.Object 클래스
- 부모의 메소드와 변수만 상속되며
- 상속의 계층은 무한대
```
class A {};
class B extends A{};
class C extends B{};
class D extends C{};
class E extends D{};
```


주의 : 상속을 해도 부모 클래스의 모든 필드와 메소드를 물려받는 것은 아니다. 부모 클래스에서 private 접근 제한을 갖는 필드와 메소드는 상속의 대상에서 제외되며 부모와 자식이 다른 패키지에서 존재한다면 default 접근 제한을 갖는 필드와 메소드도 상속 대상에서 제외된다.


# super 키워드
this() 와 마찬가지로 super()도 생성자
- 하위 클래스가 생성될 때 상위 클래스가 먼저 생성된다.
- 상위 클래스의 생성자가 호출되고 하위 클래스의 생성자가 호출된다.
- 하위 클래스의 생성자에서는 무조건 상위 클래스의 생성자가 호출되어야 함
- 하위 클래스에서 상위 클래스의 생성자를 호출하는 코드가 없는 경우 컴파일러는 상위 클래스 기본 생성자를 호출하기 위한 super()를 추가한다.
- super()로 호출되는 생성자는 상위 클래스의 기본 생성자이다.
- 만약 상위 클래스의 기본 생성자가 없는 경우( 매개변수가 있는 생성자만 존재하는 경우) 하위 클래스는 명시적으로 상위 클래스의 생성자를 호출해야 함


결론적으로 class의 상속을 하면 해당 클래스의 인스턴스를 만들 때, 부모 클래스의 인스턴스가 내재적으로 만들어진다.  
즉 언제든지 부모 클래스의 값들을 가져올 수 있는 연결고리가 생성된다.  
그 연결고리를 이어주는 것이 바로 super 키워드이다.  



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
​``` shell
"Parent is created"
"Child is created"
```

컴파일러에 의해 super()는 자동으로 각 클래스 생성자에 추가




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




# 메소드 오버라이딩
- 오버라이딩은 부모의 함수를 재정의하는 기능
- 함수명, 리턴값, 파라미터가 모두 동일해야한다.

``` java
class Parent {
  void method1() {}

  void method2() {}
}

class Child extends Parent {
  @Override
  void method2() {}

  void method3() {}
}
class Example {
  public static void main(String[] args) {
    Child child = new Child();

    child.method1();  // 상속 받은 부모 메소드 호출
    child.method2();  // 재정의한 자식 메소드 호출
    child.method3();  // 자식 메소드 호출
  }
}
```






# 메소드 디스패치
메소드 디스패치는 어떤 메소드를 호출할 지 결정하여 실제로 실행시키는 과정

## 정적 메소드 디스패치(Static Method Dispatch)

``` java
public class A{
     public void print(){
           System.out.println("A");
     }
}

public class B extends A {

     //메소드 오버라이딩 - A를 상속받았으나 함수를 재정의
     public void print(){
           System.out.println("B");
     }
}

public class Test{
      public static void main(String[] args){
             B b = new B();
             b.print();         //B를 출력
      }
}
```
위에서 작성했던 오버라이딩 소스이다. (오버로딩 예제 역시 정적 메소드 디스패치입니다.)

​

메인 함수에서 b.print()를 호출했을 때 우리는 클래스B의 오버라이딩 된 함수가 불릴 것이라는 것을 알고 있다. 우리가 이미 알고 있는 것과 같이 컴파일러 역시도 이 메소드를 호출하고 실행시켜야되는 것을 명확하게 알고 있는데 우리는 이를 정적 메소드 디스패치라 부른다.


## 동적 메소드 디스패치(Dynamic Method Dispatch)

동적 메소드 디스패치는 정적 디스패치와는 다르게 컴파일러가 어떤 메소드를 호출해야되는지 모르는 것을 말한다.
``` java
class A {
  private BB bb;

  A(BB bb) {
    this.bb = bb;
  }

  void print() {
    bb.print();
  }
}

class B implements BB {
  public void print() {
    System.out.println("B");
  }
}
class B1 implements BB {
  public void print() {
    System.out.println("B1");
  }
}

interface BB {
  void print();
}
B b=new B()
b.print()
B1 b1=B1()
b1.print()
```

<!-- new BB(); -->




# 추상 클래스
추상 클래스는 클래스를 만들기 위한 일종의 설계도로 인스턴스를 생성할 수 없는 클래스



# final 키워드

final 키워드는 엔티티를 한 번만 할당하겠다는 의미로 자바에서는 총 세가지 의미로 사용됩니다.


- final 변수
  - final 변수는 우리가 흔히 아는 상수를 의미합니다. 생성자나 대입연산자를 통해 한번만 초기화 가능한 변수입니다.

​

- final 메소드
  - final 메소드는 오버라이드하거나 숨길 수 없음을 의미합니다.

​

- final 클래스

  - 해당 클래스를 상속할 수 없음을 의미합니다. 상속을 할 수 없기 때문에 상속 계층에서 마지막 클래라는 의미입니다.
  - 오버라이딩도 불가능

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

public static class Army extends Object{
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








----------
다음주 과제설명
- static import
