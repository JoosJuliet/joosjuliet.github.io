---
layout: post
section-type: post
title: "[legacy 환경설정으로 얻은 지식들] DataSouce란?, JINDI란? JDBC란?"
category: Spring
tags: [ 'Spring', '환경설정', 'SKencar' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

# 1. JDBC란?
- Java Database Connectivity
- Java에서 DB 프로그래밍을 하기 위해 사용되는 API

database 의 API (드리이버.jar 에 들어있음) 를 사용하여 DB 쿼리를 하기 위한
자바의 API. 어떤 database (JDBC 드리이버)를 사용하더라고 사용법은 동일하다.
> Connection, Statement, ResultSet 등

## JDBC 드라이버 :
database 종류마다 내부 API 가 틀리며, 자바에서 이를 인식하기 위해
JDBC 드라이버를 설치해야한다.


- JDBC 드라이버 : 각 DBMS에 알맞는 클라이언트

JDBC 프로그래밍 코딩 흐름
1) JDBC 드라이버 로드
2) DB 연결
3) DB에 데이터를 읽거나 쓰기 (SQL문)
4) DB 연결 종료

JDBC 드라이버
- DBMS와 통신을 담당하는 자바 클래스
- DMBS 별로 알맞은 JDBC 드라이버 필요 (jar)

JDBC URL

- DBMS와의 연결을 위한 식별 값

- JDBC 드라이버에 따라 형식이 다름

---
참고 : https://dyjung.tistory.com/50

# 2. DataSouce란?

# Datasource
- 순수 jdbc로 데이터베이스에 접근을 하면, 데이터베이스에 접근할 때마다 connection을 맺고 끊는 작업을 한다.


https://deepweller.tistory.com/6



# 3. JNDI란?

JDBC 를 사용할때, 먼저 Connection 을 얻을때마다 드라이버를 DriverManager에 등록
(driver 이름,url,사용자정보를 사용해서) 해야 했으나, JNDI 기법을 사용하면
서버실행시 연동객체를 통해 DriverManager에 드라이버등록해놓고,
JDBC 사용할때 Connection을 얻는 부분에서 연동객체를 이름으로  찾아서 사용.



https://ebonny.wordpress.com/2010/11/11/spring-%EC%97%90%EC%84%9C-jndi%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-%ED%86%B0%EC%BA%A3%EC%9D%98-server-xml-%EC%97%90-%EB%93%B1%EB%A1%9D%ED%95%9C-datasource-%EC%82%AC%EC%9A%A9%ED%95%98/
