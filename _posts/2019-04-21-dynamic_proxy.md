---
layout: post
section-type: post
title: "[proxy 2편] Dynamic Proxy란?(feat. Spring)"
category: OOP
tags: [ 'Java', 'ProxyPattern', 'DesignPattern', 'DynamicProxy', 'SundayStudy', '글또 2기' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

중요참고! 이 글의 기본 base는 toby의 스프링3.1입니다.


이 컨텐츠는 시리즈물입니다.  
[proxy 1편] Proxy Pattern(프록시 패턴)이란?(feat. Java): https://joosjuliet.github.io/proxy_pattern/   
[proxy 2편] Dynamic Proxy란?(feat. Spring):  
https://joosjuliet.github.io/dynamic_proxy/
[proxy 3편] Dynamic Proxy와 트랜잭션?(feat. Spring): https://joosjuliet.github.io/transaction/  

---

# 스프링 AOP에서 사용하는 "다이나믹 프록시"
클라이언트가 사용하려고 하는 실제 대상인 것처럼 위장해서 클라이언트의 요청을 받아주는 것을 대리인과 같은 역할을 하는 것

- 프록시 패턴의 프록시는 <span style="background-color:yellow"><b>타깃의 기능을 확장하거나 추가하지 않는다.</b></span> 대신 클라이언트가 타깃에 접근하는 방식을 변경해준다.
- 타깃 오브젝트를  <span style="background-color:yellow"><b>필요한 시점까지 생성하지 않고</b></span> 타깃 오브젝트에 대한 레퍼런스가 필요하면 프록시 패턴을 적용하면 된다.(feat. 지연 생성)
- 클라이언트에게 타깃에 대한 레퍼런스를 넘겨야 하는데 실제 타깃 오브젝트 대신 프록시를 넘긴다.
- 그리고 해당 타깃을 사용하려 할 때 프록시가 타깃 오브젝트를 생성하고 요청을 위임
- 또는 특별한 상황에서 타깃에 대한 접근권한을 제어하기 위해 사용
- 프록시를 만들어 읽기전용으로 강제하고 add, update 등의 메소드를 사용하면 예외를 발생
- 구조적으로 보면 프록시와 데코레이터 패턴은 유사하지만 프록시는 코드에서 자신이 접근할 타깃 클래스 정보를 직접적으로 알야야 한다.

## 프록시
프록시를 만드는 것은 상당히 번거롭다.
하지만 자바에는 java.lang.reflect 패키지 안에 프록시를 손쉽게 만들게 지원해주는 클래스들이 있다.
마치 목프레임워크와 비슷하다. 프록시는 다음의 두 가지 기능으로 구성된다.

- 타깃과 같은 메소드를 구현하고 있다가 메소드가 호출되면 타깃 오브젝트로 위임한다.
- 지정된 요청에 대해서는 부가기능을 수행한다.
``` java

public class UserServiceTx implements UserService {
    UserService userService; //타깃 오브젝트
    ...

    @Override
    public void add(User user) {
        this.userService.add(user); //메소드 구현과 위임
    }

    @Override
    public void upgradeLevels() { //메소드 구현
    	//부가기능 수행
        TransactionStatus status = this.transactionManager.getTransaction(new DefaultTransactionDefinition());
        try {
            userService.upgradeLevels(); //위임
            this.transactionManager.commit(status);
        } catch (RuntimeException e) {
            this.transactionManager.rollback(status);
            throw e;
        }
    }
}
```
위의 코드에서 UserServiceTx 코드는 UserService 인터페이스를 구현하고 타깃으로 요청을 위임하는 트랜잭션 부가기능을 수행하는 코드로 구분할 수 있다. 이렇게 프록시의 역할은 위임, 부가작업이라는 두 가지 기능으로 구분할 수 있다.

*프록시가 번거로운 이유는 다음과 같다.*

- 첫째는 타깃의 인터페이스를 구현하고 위임하는 코드를 작성하기가 번거롭다.
일일이 코드를 만들어 주고 타깃 인터페이스의 메소드가 추가되거나 변경될 때마다 함께 수정해야 한다.

- 둘째는 부가기능 코드가 중복될 가능성이 많다.


### 리플랙션
이러한 문제들을 해결하기 위해 유용한 것이 다이내믹 프록시이다.
다이내믹 프록시는 리플랙션 기능을 이용해서 프록시를 만들어준다.

리플랙션(java.lang.reflect): 자바의 코드 자체를 추상화해서 접근하도록 만든 것

String name = "Spring";

위의 코드에서 길이를 알고 싶으면 name.length()를 호출하면 된다.

자바의 모든 클래스는 그 클래스 자체의 구성정보를 담은 class 타입의 오브젝트를 하나씩 갖고 있다.
'클래스이름.class', getClass() 메소드를 호출하면 클래스 정보를 담은 Class 타입의 오브젝트를 가져올 수 있다.
클래스 오브젝트를 이용하면 클래스 코드에 대한 메타정보를 가져오거나 오브젝트를 조작할 수 있다.

클래스의 이름이 무엇이고, 어떤 클래스를 상속하고, 어떤 인터페이스를 구현했는지, 어떤 필드를 갖고 있는지, 각각의 타입이 무엇인지, 메소드가 어떤게 있는지 등
더 나아가 오브젝트 필드의 값을 읽고 수정할 수도 있고, 원하는 파라미터 값을 이용해 메소드를 호출할 수도 있다.

``` java
Method langthMethod = String.class.getMethod("length"); //length 메소드를 가져와 invoke로 실행시키기
int length = lengthMethod.invoke(name) //int length = name.length();
```

### 다이나믹 프록시 클래스 예제

``` java
interface Hello {
    String sayHello(String name);
}
//구현한 타깃 클래스
public class HelloTarget implements Hello {
    @Override
    public String sayHello(String name) {
        return "Hello " + name;
    }
}
//인터페이스를 구현한 프록시
public class HelloUppercase implements Hello {
    Hello hello; //위임할 타깃 오브젝트(다른 프록시 접근을 위해 인터페이스로 접근)

    public HelloUppercase(Hello hello) {
        this.hello = hello
    }

    @Override
    public String sayHello(String name) {
        return hello.sayHello(name).toUpperCase(); //위임과 부가기능 적용
    }
}
@Test
public void simpleProxy() {
    Hello proxiedHello = new HelloUppercase(new HelloTarget());
    asserThat(proxiedHello.sayHello("Havi"), is("HELLO HAVI"));// true
}

```

---
참고:

aop에서 사용하는 다이나믹 프록시:  
https://haviyj.tistory.com/28 [Duck Programming]  
https://haviyj.tistory.com/26?category=695904 [Duck Programming]  
