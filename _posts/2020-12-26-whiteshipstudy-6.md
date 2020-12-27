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


참고:
https://leemoono.tistory.com/20
https://blog.naver.com/swoh1227/222181505425
https://github.com/mongzza/java-study/blob/main/study/6%EC%A3%BC%EC%B0%A8.md
https://www.notion.so/e5c33507880b4d098f83a2c4f8f02c04-> 그림도 잘그림, 설명도 잘함
-> 더블 디스패치의 과정까지 설명이 있어야 한다.


https://github.com/ByungJun25/study/tree/main/java/whiteship-study/6week
->더블 디스패치의 잼는 예제, 디지털패치도 있어야 한다.
토비의 영상에서 볼 수 있다.
------------------------
@Override 에노테이션 쓰면 확인할 수 있다.
부모는 아들 것 쓸 수 없지만
아들은 부모랑 자신 것 다 쓸 수 있따.

@Override는 단순 마커는 아니고 컴파일 타임에 check도 해준다.
붙이는게 best practice
안붙여도 intelij가 보여주기는 하다.
--------
https://www.notion.so/6-b9a34c0d1a03442091f927e91ee9858f
object class 설명도 좋다
좋은 질문(의문점)

다이나믹 디스패치인데 왜 바이트 코드 같으냐?
invokespecial과 invokevirtual
-> virtual table에 메소드가 담기고 호출 시 그 테이블에서 호출할 메서드를 가져와서 다 invokevirtual이 된다
바이트 코드는 티가 안난다, jvm virtual table에서 볼 수 잇다.
그래서 주소 접근을 통해 함수가 호출되므로 런타임 시 주소값이 어떻게 테이블에 담기느냐에 따라 호출되는 함수가 다릅니다.
---------
https://leemoono.tistory.com/20
이거 디지털 패치 설명 굿
https://blog.naver.com/swoh1227/222181505425
이건 또 꼭 보래
-----------
가장 디지털 패치의 많이 쓰는 것은
domparser과 ...

members.xml
``` xml
<members>
  <member id="1">
    <username>게릴라 </username>
    <license>라이센스 없쥬?스터디 참여안했으니 없어</license>
  </member>
  <member id="2">
    <username>whiteship </username>
    <license>1234-567-112334</license>
  </member>
</members>
```
DomParser.java

``` java
package xml;
public class DomParser{
  public static void main(String... args){
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder()
    Documnet documnet = builder.parse(new ClassPathResource("members.xml").getInputStream());
    // 돔방식으로
    NodeList members = documnet.getElementsByTagName("member");
    for (int i=0; i<members.getLength(); i++) {
      Node node = members.item(i);
      if (node.getNodeType() == Node.ELEMENT_NODE){
        Element element =(Element) node;
        String id = element.getAttribute("id");
        System.out.println(id);
      }

    }
  }
}
```
이건 다 읽어서 메모리 적재하는 거지 비지터 패턴 아님

근데 삭스라는 게 있다.
이게 어려우니 라이브러리 있따.(SAX)

SaxParser.java
``` java
public class SaxParser{
  public static void main(String[] args) throws ParserConfigurationException, SAXException {
    SaxParserFactory factory = SaxParserFactory.newInstance();
    SaxParserFactory saxParser = factory.newSAXParser();
    SaxParser.parse(new ClassPathResource("members.xml").getInputStream
    (), new MemberHandler())
  }

  static class MemberHandler extends DefaultHandler {
    @Override
    public void startDocument() throws SAXException {
      SOUT("start parsing xml");
    }
    @Override
    public void endDocument() throws SAXException{
      SOUT("end parsing xml");
    }
    @Override
    public void startElement(String uri, String localName, String qName, ){
      SOUT("element"+ qName);
    }
  }
}

```
이건 그나마 메모리 들쓴다.
돔파서는 메모리 o(n) 이건 o(1)
이건 비지터 패턴을 쓰는 xml파서이기 때문에 o(1)

xml의 member블럭이 각 element다

-----------

돔은 계속 메모리에 다 넣어놓는데, sax는 그냥 지나가면서 쭉 보는거여서 o(1)

--------

first class citizen
함수자체를 매개변수로 넘기거나 변수에 할당하거나 리턴하거나 해야한다.
자바도 이제 가능한데 정확히는 함수는 아니지만 함수 비슷한 것을
그 전에는 오브젝트를 가지고 했다.
즉 모든 것들을 오브젝트로 해야했다. 그래서 최상위를 오브젝트로 했다

-------
https://whereishq.blogspot.com/2020/12/6.html
invokespecial 설명해준다.


일단 이번 과제의 주제인 상속에 대해서 먼저 정리를 해봐야겠다.
- 상속
  - 기존의 클래스를 다양한 형태로 확장 할 수 있게 도와주는 개념
  - 서브 클래스와 슈퍼 클래스라는 계층 구조를 생성
  - 상속을 잘 사용할 수 있게 도와주는 개념들
    - 서브 클래스가 부모 클래스를 대신하여 작업하는 것을 가능하게 해주는 다형성
    - 클래스 속의 값들을 내부에서만 관리 할 수 있게 하는 캡술화

주의 : 상속을 해도 부모 클래스의 모든 필드와 메소드를 물려받는 것은 아니다. 부모 클래스에서 private 접근 제한을 갖는 필드와 메소드는 상속의 대상에서 제외되며 부모와 자식이 다른 패키지에서 존재한다면 default 접근 제한을 갖는 필드와 메소드도 상속 대상에서 제외된다.


하위 클래스가 생성될 때 상위 클래스가 먼저 생성된다.

상위 클래스의 생성자가 호출되고 하위 클래스의 생성자가 호출된다.

하위 클래스의 생성자에서는 무조건 상위 클래스의 생성자가 호출되어야 함

하위 클래스에서 상위 클래스의 생성자를 호출하는 코드가 없는 경우 컴파일러는 상위 클래스 기본 생성자를 호출하기 위한 super()를 추가한다.

super()로 호출되는 생성자는 상위 클래스의 기본 생성자이다.

만약 상위 클래스의 기본 생성자가 없는 경우( 매개변수가 있는 생성자만 존재하는 경우) 하위 클래스는 명시적으로 상위 클래스의 생성자를 호출해야 함


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
​``` shell
"Parent is created"
"Child is created"
```

컴파일러에 의해 super()는 자동으로 각 클래스 생성자에 추가




# 메소드 오버라이딩
- 오버라이딩은 부모의 함수를 재정의하는 기능
- 함수명, 리턴값, 파라미터가 모두 동일해야한다.

``` java
public class Parent {
     public void print(){
           System.out.println("Parent");
     }
}

public class Child extends Parent {
     public void print(){
           System.out.println("Child");
     }
}

public class Main{
      public static void main(String[] args){
             Child child = new Child();
             child.print();         // Parent를 출력
      }
}
```



## 메소드 오버로딩(Overloading)
- 이름도 비슷하고 둘 다 다형성을 만드는데 사용하기 때문에 은근 말이 헷갈린다.
``` java
public class Parent {
     public void print(){
           System.out.println("Parent");
     }

     public void print(int a){
           System.out.println("A" + "_" + a);
     }

     public void print(int a, int b){
           System.out.println("A" + "_" + a + "_" + b);
     }
}
```
위 예제가 오버로딩을 구현한 것이다. 오버로딩은 메소드와 리턴값은 같지만 매개변수가 다른 것을 의미한다. 만약 매개변수의 타입이 달라져도 오버로딩이 성립



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
```
위의 예제에서 BB라는 추상클래스는 B, B1으로 각각 구현되고 있다. 또한  A라는 클래스는 이런 BB라는 추상클래스(설계도)를 받아 bb.print()라는 함수를 사용하고 있다.

​

그렇다면 여기서 A클래스의 print()함수를 사용하면 어떤 함수가 호출될까? 아마도 해당 함수의 객체를 선언할 때에 할당 된 Obejct를 보고 어떤 함수를 실행할 지 결정하게 될 것이다. 우리는 이렇게 유추가 가능하지만 컴파일러는 이에 대해 알 수 있는 방법이 없다. 즉 컴파일러는 어떤 함수가 실행될 지 전혀 모르는 것이다. (B클래스의 print()를 가져와야 할 지 , B1클래스의  print()를 가져와야 할 지 아는 시점은 런타임 시점일 것이다.)

​

이처럼  컴파일러가 어떤 메소드를 호출해야되는지 모르는 것을 우리는 동적 메소드 디스패치라고 부른다.

## 더블 디스패치(Double Dispatch)

더블 디스패치는 Dynamic Dispatch를 두 번 하는 것을 의미한다.

``` java
interface Post {
    void postOn(SNS sns);
}

class Text implements Post {
    public void postOn(SNS sns) {
        sns.post(this);
    }
}

class Picture implements Post {
    public void postOn(SNS sns) {
        sns.post(this);
    }
}
interface SNS {
    void post(Text text);
    void post(Picture picture);
}

class Facebook implements SNS {
    public void post(Text text) {
        // text -> facebook
    }
    public void post(Picture picture) {
        // picture -> facebook
    }
}

class Twitter implements SNS {
    public void post(Text text) {
        // text -> twitter
    }
    public void post(Picture picture) {
        // picture -> twitter
    }
}
public static void main(String[] args) {
     List<Post> posts = Arrays.asList(new Text(), new Picture());
     List<SNS> sns = Arrays.asList(new Facebook(), new Twitter());

     posts.forEach(p -> sns.forEach(s -> p.postOn(s)));
}
```
더블 디스패치에 대한 예제이다. 해당에서는 총 두 번의 다이나믹 디스패치가 이루어진다.

​

1) Post 에서 어떤 구현체의 postOn을 사용할 지

2) postOn에서 SNS의 어떤 구현체의 post 함수를 사용할지

​

이렇게 두번의 다이나믹 디스패치를 거치게 되면 구현체를 생성하는 것에 자유로워지게 된다.
``` java
//코드 추가시
class Instagram implements SNS {
    public void post(Text text) {
        // text -> instagram
    }
    public void post(Picture picture) {
        // picture -> instagram
    }
}

```



# 추상 클래스
추상 클래스는 클래스를 만들기 위한 일종의 설계도로 인스턴스를 생성할 수 없는 클래스



# final 키워드

final 키워드는 엔티티를 한 번만 할당하겠다는 의미로 자바에서는 총 세가지 의미로 사용됩니다.

​

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








----------
다음주 과제설명
- static import
