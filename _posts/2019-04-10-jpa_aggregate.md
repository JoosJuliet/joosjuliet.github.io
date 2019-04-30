---
layout: post
section-type: post
title: "[작성중]JPA에는 aggregate나 sum, max,min같은 함수가 없나?"
categories: Spring
tags: [ 'Spring', 'orm', 'stream' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---



JPA를 쓰다가 고민이 생겼다.
움... 작업을 하다보면 어떤 값의 max, min, sum등을 하게 된다.
그럴 때 장고나, 노드에서는 그런 작업들을 하기 쉽게 장고에서 그런 함수를 사용할 수 있게 해준다.

(feat. annotate, aggregate, sum, max, min)
(참고자료 : http://raccoonyy.github.io/django-annotate-and-aggregate-like-as-excel/)

그렇다면 spring boot의 orm인 jpa의 구현체 hibernate는 그에 관련된 함수는 어디있지?
라는 생각이 들었다.

그렇게 생각을 하고 미친듯이 spring쪽을 찾아보니 쿼리를 날리는 것 밖에 없어보인다.
(참고자료 : https://www.baeldung.com/hibernate-aggregate-functions)



지금의 나는 왜 저런 function을 찾고 있는가?
그건 sum 함수를 쓰면 알아서 framework단에서 디비 쿼리를 만들어서 보내주기를 원하기 때문이다.
즉 db에서 작업을 하게 하고, 서버에서는 그에 대한 결과만 받게 되는것을 원한다.(즉 연산을 db가 하게 하는 것)

기본으로 제공되는 findbyid 같은 것들은 연산을 db에서 하게 해주는 것이다.
그렇다면 java의 stream을 사용하면 어떤 결과가 나올까? debug를 찍어봐서 그에 대한 결과를 찾아보자.

(관련 url : https://lng1982.tistory.com/273)
findbyid는 왜 db에서 해주는거 repository에서 선언이 되있어서 그게 되는 거 아닌가?

Q. 어느단계에서 db쿼리로 바꿔주는 거지?


# 기존 JDBC 개발방식을 보자
JDBC를 이용해서 애플리케이션을 개발 할 때 쿼리를 실행하면 DB로 쿼리를 바로 날린다.
아래와 같이 코드를 작성하고 execute하면 DB로 쿼리해서 데이터를 가져오는 식이다.

``` java
String sql = "SELECT id, first, last, age FROM Registration";
ResultSet rs = stmt.executeQuery(sql); // DB로 쿼리한다.
```

# JPA 개발 방식

영속성 컨텍스트는 JDBC와 DB 사이에 위치하여 뭔가의 작업을 진행한다.
그 무엇인가는 다음과 같다.

1. 조회할 데이터가 영속성 컨텍스트에 존재하는지 확인
2. 데이터가 없으면 쿼리를 생성
3. 쿼리를 DB에 전송
4. 결과 값을 영속성컨텍스트가 전달 받음
5. 전달 받은 데이터를 엔티티로 저장
6. 엔티티 인스턴스를 리턴
위의 많은 처리를 코드 단 한 줄이 수행한다.

``` java
Emp emp = em.find(Emp.class, 1);
```


# 장점
1. select * from emp wherer id = 1 로 조회해서 데이터를 가져오면 동일 아이디로 쿼리 재요청 시 영속성 컨텍스트에 있는 엔티티를 가져와 재사용
2. 특정 비즈니스에서 update, insert, delete 를 여러 번 구현했을 때 이전 방식에서는 코드가 수행될 때마다 DB에 요청을 보내는 반면 영속성 컨텍스트는 쿼리를 생성하여 특정 영역에 저장만 해두었다가 flush가 되는 순간 한꺼번에 DB로 쿼리를 날린다. 이를 JPA에서는 "쓰기 지연" 이라고 한다.
3. 업데이트 처리가 필요할 때 Emp emp = em.find(Emp.class, 1); 와 같이 엔티티를 가져온 후 emp.setName("nklee"); 와 같이 엔티티의 속성 값을 변경하면 엔티티 매니저가 flush 되면서 update 쿼리문을 DB로 쿼리한다.
4. 지연 로딩을 통해 특정 엔티티의 데이터를 사용하는 시점에 초기화하여 DB 요청을 보낼 수 있다.
5. 화면마다 쿼리 안 만들어도 된다.
6. 리펙토링이 쉽다.


즉 영속성 컨텍스트가 있어서 stream 만으로도 그 aggregate 같은 db function의 사용시 이점을 사용 할 수 있는 것 같다.
-> 아니다. 각 애들끼리 준다.

즉
``` JAVA

library.stream()
          .map(book -> book.getAuthor())
          .filter(author -> author.getAge() >= 50)
          .map(Author::getSurname)
          .map(String::toUpperCase)
          .distinct()
          .limit(15)
          .collect(toList()));


```
If the data originally comes from a DB it is better to do the filtering in the DB rather than fetching everything and filtering locally.

First, Database management systems are good at filtering, it is part of their main job and they are therefore optimized for it. The filtering can also be sped up by using indexes.

Second, fetching and transmitting many records and to unmarshal the data into objects just to throw away a lot of them when doing local filtering is a waste of bandwidth and computing resources.

참고 : https://stackoverflow.com/questions/43304023/why-would-you-prefer-java-8-stream-api-instead-of-direct-hibernate-sql-queries-w

결론 : 다 fetch 한 다음에 한다.
db에게 시키는게 좋으니 따로 쿼리 날려라
근데 greaterthan같은 함수는 쓰면 좋다.쿼리 그걸로 만들어 날리니가
Between, LessThan, GreaterThan, Like같은 연산자의 지원을 받을 수 있습니다.
참고 : http://arahansa.github.io/docs_spring/jpa.html



# [언제 영속성 컨텍스트 flush가 이뤄지나?]

해당 테스트 케이스를 만들기 위해서 테스트 데이터를 생성할 때 별도의 트랜잭션에서 처리되도록 하였고,
또한 Account 의 상태 변경을 처리할 때에도 별도의 트랜잭션에서 동작하도록 코드를 작성하였다.
test 데이터 생성시 별도의 트랜잭션에서 데이터 생성
> 테스트 데이터를 생성하는 testData 메서드가 종료되면 영속성 컨텍스트가 flush 되고 해당 데이터가 DB에 반영된다.
accountService의 updateAccount 메서드를 호출하면 별도의 트랜잭션이 생성되고 Account where = 2의 name필드 값을 변경한다.
> updateAccount 메서드도 종료되면 영속성 컨텍스트가 flush 되면서 update 문이 DB에 전송된다.
em.find(Account.class, 2); 와 같이 조회를 하면 select 쿼리가 DB에 전송되고 변경된 이름을 확인할 수 있다.
테스트에서 볼 수 있듯이 영속성 컨텍스트는 트랜잭션이 종료되면 flush 가 동작하게 된다.

즉, 트랜잭션과 영속성 컨텍스트는 동일한 라이프 사이클을 가지고 있다고 보면 된다.




---

영속성 :
http://wonwoo.ml/index.php/post/997

http://arahansa.github.io/docs_spring/jpa.html
