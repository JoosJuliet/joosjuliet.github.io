---
layout: post
section-type: post
title: "Singleton Pattern(싱글톤 패턴)이란?(feat. Java)"
category: Spring
tags: [ 'Java', 'SKEncarLunchStudy', 'SingletonPattern', '글또2기', 'DesignPattern' ]
comments: true
---
# singleton패턴
<span style="background-color:yellow"><b>인스턴스가 사용될 때에 똑같은 인스턴스를 만들어 내는 것이 아니라, 동일 인스턴스를 사용하게끔 하는 것이 기본 전략</b></span>


## singleton이 나온 배경과 설명
singleton은 전역변수를 쓰고 싶어서 나온 개념이다.
근데 자바에는 전역변수라는 개념이 없다. 모든 것은 객체로 쌓여있어야한다.
그런데 쓰고 싶을 수 있다. 그럴 때 싱글톤을 쓴다.

근데 좀 위험할수 있다.
왜냐면 객체는 여러개가 생성될 수 있으니까 말이다.
하나만 쓰려 했는데, 여러개 생성되면 의미가 없어진다.


## singleton으로 만드는 핵심 방법
<span style="background-color:yellow"><b>그래서 전역 변수로 instance를 만드는데 private static을 이용한다.</b></span>
- static이 붙은 클래스변수는 인스턴스화에 상관없이 사용이 가능하게 된다.
- 하지만 앞의 private 접근제어자로 인해 Singleton.instance로의 접근은 불가능하다.

결국 외부 클래스가 EagerInitialization 클래스의 인스턴스를 가질 수 있는 방법은 getInstance() method를 사용하는 수 밖에 없다.


## singleton 구현방법
### singleton 구현방법 1
그래서 처음것은 실행하기 직전에 다 할당을 한다.
왜냐하면 static 객체이기 때문이다.
static 객체 특징
- 객체가 생기기 전에 이미 생성된다.
- 객체가 생기기 전에도 사용이 가능하다. (즉, 객체를 생성하지 않고도 사용할 수 있다.)
참고 : https://gmlwjd9405.github.io/2018/08/04/java-static.html

``` java

public class Singleton{
    private static Singleton instance = new Singleton(); // static 변수는 변수공간을 항상 유지해야 할때 사용
    private Singleton(){
    }

    public String getName(){
        return "IU";
    }
    public static Singleton getInstance(){
        return instance;
    }
}

public class Solution{
    public static void main(String[] args) throws IOException {
        Singleton.getInstance().getName();
    }
}

```

이 방법의 단점
- 프로그램의 크기가 커져서 수 많은 클래스에서 위와 같은 singleton pattern을 사용한다고 가정해보자.
- new Singleton()으로 인해 클래스가 load 되는 시점에 인스턴스를 생성시키는데 이마저도 부담스러운 경우도 있따.
- <b>또한 Singleton 클래스가 인스턴스화 되는 시점에 <b>어떠한 에러처리도 할 수가 없다.</b>


### singleton 구현방법 2 (static block initialization)

두번째것은 동적으로 할당을 하는 것이다.

``` java

public class Singleton{
    private static Singleton instance;
    static {
      try{
           instance = new Singleton();
      } catch (Exception e) {
      throw new RuntimeException("Exception creating Singleton instance.");
    }

    private Singleton () {}
    public String getName(){
        return "IU";
    }
    public static Singleton getInstance(){
      return instance;
		}
}

public class Solution{
    public static void main(String[] args) throws IOException {
        Singleton.getInstance().getName();
    }
}

```

static 초기화블럭을 이용하면 클래스가 로딩 될 때 최초 한번 실행하게 된다.
* 인스턴스 초기화 블럭 : 인스턴스 변수의 복잡한 초기화에 사용된다. 인스턴스가 생성될때 마다 수행된다. (생성자보다 먼저 수행된다.) *
참고 : https://hashcode.co.kr/questions/654/%EC%9E%90%EB%B0%94%EC%97%90%EC%84%9C-static-%EB%B8%94%EB%A1%9D%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%84-%EC%9D%98%EB%AF%B8%ED%95%98%EB%82%98%EC%9A%94  
특히나 초기화블럭을 이용하면 logic을 담을 수 있기 때문에 복잡한 초기변수 셋팅이나 위와 같이 에러처리를 위한 구문을 담을 수 있다.
첫 번째 패턴보다 좋아보이지만 인스턴스가 사용되는 시점에 생성되는 것은 아니다.

---
이건 간단한 설명이다
참고링크를 통해서 더 깊게 공부 하는 것이 굿
참고 : https://blog.seotory.com/post/2016/03/java-singleton-pattern
