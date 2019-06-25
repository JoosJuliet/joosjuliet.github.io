---
layout: post
section-type: post
title: "[tech interview 6 편] SPRING"
categories: Tech_Interview
tags: [ 'interview', 'technology', 'it', 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
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
# 1. Spring Framework(스프링 프레임워크)

<span style="background-color:yellow"><b>자바(JAVA) 플랫폼을 위한 오픈소스(Open Source) 애플리케이션 프레임워크(Framework)</b></span>

자바 개발을 위한 프레임워크로 상속 받아서 많은 기능을 사용할 수 있게 해준다.  
특히 자바SE(standard edition)로 된 자바 객체(POJO)를 자바EE(enterprise edition)에 의존적이지 않게 연결해주는 역할  
(Java EE는 Java SE 스펙을 기반으로 하는데 이걸 의존적이지 않게 연결 해주니 존좋인듯 하다.)  

스프링 특징 간단히  
  - 크기와 부하의 측면에서 경량.  
  - 제어 역행(IoC)이라는 기술을 통해 애플리케이션의 느슨한 결합을 도모
  - 관점지향 프로그래밍(AOP)을 위한 풍부한 지원
  - 애플리케이션 객체의 생명 주기와 설정을 포함하고 관리한다는 점에서 일종의 컨테이너(Container)라고 할 수 있음
  - 간단한 컴포넌트로 복잡한 애플리케이션을 구성하고 설정할 수 있음

스프링 특징 자세히

a. 경량 컨테이너로서 자바 객체를 직접 관리.
  각각의 객체 생성, 소멸과 같은 라이프 사이클을 관리하며 스프링으로부터 필요한 객체를 얻어올 수 있다.

b. 스프링은 POJO(Plain Old Java Object) 방식의 프레임워크.
  일반적인 J2EE 프레임워크에 비해 구현을 위해 특정한 인터페이스를 구현하거나 상속을 받을 필요가 없어 기존에 존재하는 라이브러리 등을 지원하기에 용이하고 객체가 가볍다.

c. 스프링은 제어의 역행(IoC : Inversion of Control)을 지원.
  컨트롤의 제어권이 사용자가 아니라 프레임워크에 있어서 필요에 따라 스프링에서 사용자의 코드를 호출한다.

d. 스프링은 의존성 주입(DI : Dependency Injection)을 지원
  각각의 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결시켜준다.

e. 스프링은 관점 지향 프로그래밍(AOP : Aspect-Oriented Programming)을 지원
  따라서 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있다.

f. 스프링은 영속성과 관련된 다양한 서비스를 지원
  Hibernate 등 이미 완성도가 높은 데이터베이스 처리 라이브러리와 연결할 수 있는 인터페이스를 제공한다.

g. 스프링은 확장성이 높음.
  스프링 프레임워크에 통합하기 위해 간단하게 기존 라이브러리를 감싸는 정도로 스프링에서 사용이 가능하기 때문에 수많은 라이브러리가 이미 스프링에서 지원되고 있고 스프링에서 사용되는 라이브러리를 별도로 분리하기도 용이하다.

# 2. AOP란 무엇이고 왜 사용하는지



# 3. maven이란?
1. Maven은 무엇인가?
Maven은 자바 프로젝트의 빌드(build)를 자동화 해주는 빌드 툴(build tool)이다.

2. Maven이 참조하는 설정 파일
Maven 전체를 보기보다 프로그래밍에 직접적인 연관이 있는 두 개의 설정파일을 알아보면 된다.

1) settings.xml
settings.xml은 maven tool 자체에 관련된 설정을 담당한다.
MAVEN_HOME/conf/ 아래에 있다. ( * MAVEN_HOME은 환경변수에 설정한 경로
Maven 자체에 설정 값을 바꾸는 일은 일단 잘 없으므로 넘어가고 기획한대로 pom.xml을 살펴본다.

2) pom.xml
하나의 자바 프로젝트에 빌드 툴로 maven을 설정했다면, 프로젝트 최상위 디렉토리에 "pom.xml"이라는 파일이 생성되었을 것이다. pom.xml은 POM(Project Object Model)을 설정하는 부분으로 프로젝트 내 빌드 옵션을 설정하는 부분이다. 꼭 pom.xml이라는 이름을 가진 파일이 아니라 다른 파일로 지정할 수도 있다. (mvn -f ooo.xml test) 그러나 maven의 원칙(습관에 의한 편의성?)으로 다른 개발자들이 헷갈릴 수 있으므로 그냥 pom.xml으로 쓰기를 권장한다.

# 4. Entity란
- JPA entity class는 POJO(Plain Old Java Object)이다.
- 데이터베이스에있는 객체를 나타내는 능력을 가진 것으로 annotated된 일반 자바 클래스.
- JPA를 사용한 database에서 특정 object를 저장하기 위해서 우리는 entity class를 저장해야한다.
- 개념적으로 이는 serialize class와 비슷하며, serialize할 수 있는 능력이 있다는 것을 보여준다.

(Entity에 관련된 내용을 담은 url : https://joosjuliet.github.io/entity/)

## 4-1. EntityGraph란?
- 엔티티들은 서로 연관되어 있는 관계가 보통이며 이 관계는 그래프로 표현이 가능
- EntityGraph는 JPA가 어떤 엔티티를 불러올 때 이 엔티티와 관계된 엔티티를 불러올 것인지에 대한 정보를 제공

- FetchType.LAZY 와 FetchType.EAGER로 연관 엔티티를 가져올 것인지를 결정할 수 있습니다.
- 하지만 이 구문은 정적이며 런타임 시 이 설정을 변경하지 못하는 단점이 있었습니다.
- EntityGraph는 이러한 점을 보완하고 연관 엔티티를 어떻게 로딩할 것인지에 대한 정보를 제공함으로서 엔티티 로딩 속도를 높일 수 있는 장점이 있습니다.

spring에서
Django Debug Toolbar, Django Extensions Debugger 같은 거


# 5. aop란?
비즈니스 로직과 트랜잭션 경계설정의 분리를 통해 성격이 다른 코드를 각각 독릭적인 코드로 만들 수 있다.

# 6. @Embedded - @Embeddable vs @OneToOne
객체를 쪼개고 싶을 때 주로 @Embedded - @Embeddable, @OneToOne 을 쓴다.
@Embedded - @Embeddable 는 table이 분리되어 있지 않지만 종속관계에 있다.
@OneToOne 은 table도 분리하고, 부모와 자식 객체의 라이프사이클이 하나다.

좀 더 자세한 설명은 :  
https://joosjuliet.github.io/embedded-embeddable  

# 7.


---
참고링크 :

1번 참고 - https://hahahoho5915.tistory.com/16

3번 참고 - https://jeong-pro.tistory.com/168?category=793347 [기본기를 쌓는 정아마추어 코딩블로그]

4번 참고 - https://engkimbs.tistory.com/835
