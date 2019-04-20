---
layout: post
section-type: post
title: "Proxy Pattern(프록시 패턴)이란?(feat. Java)"
category: Spring
tags: [ 'Java', 'SKEncarLunchStudy', 'ProxyPattern', 'DesignPattern' ]
comments: true
---

# Proxy 패턴
<span style="background-color:yellow"><b>실제로 액션을 취하는 객체를 대신해서 "대리자 역할"을 해 자신이 보호하고 있는 객체에 대한 액세스 권한을 제어하는 전략</b></span>


## Proxy이 나온 배경과 설명
객체에 관한 권한을 부여를 직접 했으면 좋겠고, "필요에 따라" 객체를 생성시키거나 사용해 메모리를 절약하고 싶어서 만든 것이다.


## Proxy로 만드는 핵심 방법
<span style="background-color:yellow"><b>interface와 interface를 상속받은 class를 만드는 것이다.</b></span>
- interface를 implements한 class에 높은 cost(네트워크 연결, 메모리 안의 커다란 객체, 파일, 또 복제할 수 없거나 수요가 많은 리소스)를 하는 method가 있으면 메모리 낭비가 심하다.
- 그래서 일단 똑같은 interface를 상속받는 class들을 만들고, 그중 한 class를 높은 cost를 가지고 있는 method를 갖게 한다.
- 나머지 class는 그 class를 인스턴스화 해서 그 높은 cost를 가진 메소드에 접근을 결정한다.


## Proxy 구현방법


- 일단 CommandExcutorImpl, CommandExecutorProxy는 똑같은 인터페이스(CommandExecutor)를 상속받음으로 인터페이스의 일관성을 유지한다.
- 생성자에서 CommandExcutorImpl 클래스를 인스턴화 시키고, 인스턴스화 된 executor 객체의 runCommand 메소드를 프록시 클래스의 runCommand 메소드에서 액세스를 결정한다.

``` java
public interface CommandExecutor {
    public void runCommand(String cmd) throws Exception ;
}
public class CommandExcutorImpl implements CommandExecutor {
    @Override
    public void runCommand(String cmd) throws IOException {
      // 높은 cost를 가진 method
        Runtime.getRuntime().exec(cmd);
        System.out.println("cmd: " + cmd);
    }
}

public class CommandExecutorProxy implements CommandExcutor {
    private boolean isAdmin;
    private CommandExecutor executor;

    public CommandExecutorProxy(String user, String pwd) {
        if ( "seotory".equals(user) && "pw".equels(pwd) ) {
            isAdmin = true;
        }
        executor = new CommandExcutorImpl();
        // 생성자에서 CommandExcutorImpl 클래스를 인스턴화
    }

    @Override
    public void runCommand(String cmd) throws Exception {
      // 생성자에서 만든 인스턴스화 된 executor의 runCommand 메소드를 액세스 할지 말지를 결정한다.
        if (isAdmin) {
            executor.runCommand(cmd);
        } else {
            if (cmd.trim().startsWith("rm")) {
                throw new Exception("rm is only admin");
            } else {
                executor.runCommand(cmd);
            }
        }
    }
}

@testing
public class ProxyPatternTest {
    public static void main(String[] args) {
        CommandExcutor executor = new CommandExecutorProxy("seotory", "is_not_pw");
        try {
            executor.runCommand("ls -al");
            executor.runCommand("rm -rf *"); // proxy 클래스에 의해 에러가 날 것이다. -> 위에서 pw가 아닌 is_not_pw로 썼기에
        } catch (e) {
            System.out.println("Exception Message: " + e.getMessage());
        }
    }
}
```
```
결과 output
cmd: ls -al
cmd: rm -rf *// proxy 클래스에 의해 에러가 날 것이다.
Exception Message: rm is only admin
```


## 적용 포인트
- 프록시 패턴의 잘 알려진 예로는 참조 횟수 스마트 포인터 객체이다.

- 가상 프록시
  - 높은 cost 객체 대신 스켈레톤 객체(인터페이스만 존재하고 실제로 인스턴스를 생성하지 않는 객체)를 사용하여 실질적으로 객체가 필요할때까지 높은 cost의 객체 생성을 지연시켜 메모리를 절약할 수 있다.
- 원격 프록시
  - 서로 다른 머신에 있는 객체에 대해 제공할 수 있다(또는 객체를 사용할 수 있다). 일반적인 예는 JAVA의 RMI(다른컴퓨터에서 함수가져오는 것)이다.
- 보호 프록시
  - 객체에 대해 액세스 할 수있는 권한을 부여할 수 있다.
- 정교한 참조
  - 프록시 객체에 정교한 작업을 부여할 수 있다. 예를들어 객체를 생성할 때 카운팅 기능을 추가적으로 작업할 수 있다.


# 스프링 AOP에서 사용하는 "다이나믹 프록시"
클라이언트가 사용하려고 하는 실제 대상인 것처럼 위장해서 클라이언트의 요청을 받아주는 것을 대리자, 대리인과 같은 역할을 한다고 하여 프록시(Proxy)

프록시를 통해 최종적으로 요청을 위임받아 처리하는 실제 오브젝트를 타깃(tartget) or 실체(real subject)

프록시의 특징은 타깃과 같은 인터페이스를 구현했다는 것과 프록시가 타깃을 제어할 수 있는 것이다.
프록시는 사용 목적에 따라 두 가지로 구분할 수 있다.
1)클라이언트가 타깃에 접근하는 방법을 제어하기 위해서다.
2)타깃에 부가적인 기능을 부여해주기 위해서다.


프록시 패턴의 프록시는 프록시를 사용하는 방법 중에서 타깃에 대한 접근 방법을 제어하려는 목적을 가진 경우를 말한다.
프록시 패턴의 프록시는 타깃의 기능을 확장하거나 추가하지 않는다. 대신 클라이언트가 타깃에 접근하는 방식을 변경해준다.
타깃 오브젝트를 필요한 시점까지 생성하지 않고 있다가 타깃 오브젝트에 대한 레퍼런스가 필요하면 프록시 패턴을 적용하면 된다.(지연 생성)
클라이언트에게 타깃에 대한 레퍼런스를 넘겨야 하는데 실제 타깃 오브젝트 대신 프록시를 넘긴다.
그리고 해당 타깃을 사용하려 할 때 프록시가 타깃 오브젝트를 생성하고 요청을 위임해 주는 식이다.
또는 특별한 상황에서 타깃에 대한 접근권한을 제어하기 위해 사용할 수도 있다.
프록시를 만들어 읽기전용으로 강제하고 add, update 등의 메소드를 사용하면 예외를 발생시키면 된다.
구조적으로 보면 프록시와 데코레이터 패턴은 유사하지만 프록시는 코드에서 자신이 접근할 타깃 클래스 정보를 직접적으로 알야야 한다.

다이내믹 프록시
프록시를 만드는 것은 상당히 번거롭다. 하지만 자바에는 java.lang.reflect 패키지 안에 프록시를 손쉽게 만들게 지원해주는 클래스들이 있다. 마치 목프레임워크와 비슷하다. 이를 통해 몇 가지 API를 이용해 프록시처럼 동작하는 오브젝트를 다이내믹하게 생성해 보자. 프록시는 다음의 두 가지 기능으로 구성된다.

타깃과 같은 메소드를 구현하고 있다가 메소드가 호출되면 타깃 오브젝트로 위임한다.
지정된 요청에 대해서는 부가기능을 수행한다.
``` java

public class UserServiceTx implements UserService {
    UserService userService; //타깃 오브젝트
    ...

    public void add(User user) {
        this.userService.add(user); //메소드 구현과 위임
    }

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
위의 코드에서 UserServiceTx 코드는 UserService 인터페이스를 구현하고 타깃으로 요청을 위임하는 트랜잭션 부가기능을 수행하는 코드로 구분할 수 있다. 이렇게 프록시의 역할은 위임, 부가작업이라는 두 가지 기능으로 구분할 수 있다. 프록시가 번거로운 이유는 다음과 같다.

첫째는 타깃의 인터페이스를 구현하고 위임하는 코드를 작성하기가 번거롭다. 일일이 코드를 만들어 주고 타깃 인터페이스의 메소드가 추가되거나 변경될 때마다 함께 수정해야 한다.
둘째는 부가기능 코드가 중복될 가능성이 많다.
리플랙션
이러한 문제들을 해결하기 위해 유용한 것이 다이내믹 프록시이다. 다이내믹 프록시는 리플랙션 기능을 이용해서 프록시를 만들어준다.

리플랙션(java.lang.reflect): 자바의 코드 자체를 추상화해서 접근하도록 만든 것

String name = "Spring";
위의 코드에서 길이를 알고 싶으면 name.length()를 호출하면 된다. 자바의 모든 클래스는 그 클래스 자체의 구성정보를 담은 class 타입의 오브젝트를 하나씩 갖고 있다. '클래스이름.class', getClass() 메소드를 호출하면 클래스 정보를 담은 Class 타입의 오브젝트를 가져올 수 있다. 클래스 오브젝트를 이용하면 클래스 코드에 대한 메타정보를 가져오거나 오브젝트를 조작할 수 있다.

클래스의 이름이 무엇이고, 어떤 클래스를 상속하고, 어떤 인터페이스를 구현했는지, 어떤 필드를 갖고 있는지, 각각의 타입이 무엇인지, 메소드가 어떤게 있는지 등
더 나아가 오브젝트 필드의 값을 읽고 수정할 수도 있고, 원하는 파라미터 값을 이용해 메소드를 호출할 수도 있다.
Method langthMethod = String.class.getMethod("length"); //length 메소드를 가져와 invoke로 실행시키기
int length = lengthMethod.invoke(name) //int length = name.length();
프록시 클래스 예제
간단한 프록시 클래스를 만드는 예제를 진행해 보겠다. 프록시는 데코레이터 패턴을 적용해서 타깃인 HelloTarget에 부가기능을 추가했다.
``` java
interface Hello {
    String sayHello(String name);
}
//구현한 타깃 클래스
public class HelloTarget implements Hello {
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

    public String sayHello(String name) {
        return hello.sayHello(name).toUpperCase(); //위임과 부가기능 적용
    }
}
@Test
public void simpleProxy() {
    Hello proxiedHello = new HelloUppercase(new HelloTarget());
    asserThat(proxiedHello.sayHello("Havi"), is("HELLO HAVI"));
}

```
출처: https://haviyj.tistory.com/28?category=695904 [Duck Programming]
출처: https://haviyj.tistory.com/28?category=695904 [Duck Programming]

aop 간단설명 :비즈니스 로직과 트랜잭션 경계설정의 분리를 통해 성격이 다른 코드를 각각 독릭적인 코드로 만들 수 있다.


출처: https://haviyj.tistory.com/28 [Duck Programming]


---
참고:
메소드 사진 참고:  
http://ehpub.co.kr/tag/%ED%94%8C%EB%9D%BC%EC%9D%B4%EA%B8%89-%ED%8C%A8%ED%84%B4-flyweight-pattern/  

프록시패턴 참고 : https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%ED%8C%A8%ED%84%B4  
https://blog.seotory.com/post/2017/09/java-proxy-pattern  

aop에서 사용하는 다이나믹 프록시:  
https://haviyj.tistory.com/28 [Duck Programming]

출처: https://haviyj.tistory.com/26?category=695904 [Duck Programming]
