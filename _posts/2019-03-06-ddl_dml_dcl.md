---
layout: post
section-type: post
title: "[DB] DDL, DML, DCL이란?(feat. DELETE, TRUNCATE, DROP의 차이)"
category: DB
tags: [ 'SKencar', 'db' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


# SQL (Structered Query Language)
 - <span style="background-color:yellow"><b> 관계형 데이터베이스 관리 시스템(RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어 </b></span>
 - 관계형 데이터베이스 관리 시스템에서 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안
 - SQL은 데이터베이스로부터 정보를 얻거나 갱신하기 위한 표준 대화식 프로그래밍 언어
 - 많은 수의 데이터베이스 관련 프로그램들이 SQL을 표준으로 채택




# SQL 문법의 종류 3가지
- DDL
- DML
- DCL




## 데이터 정의 언어 - ( DDL : Data Definition Language )
<span style="background-color:yellow"><b> 테이블이나 관계의 구조를 생성하는데 사용 </b></span>
- CREATE - 새로운 데이터베이스 관계 (테이블) View, 인덱스 , 저장 프로시저 만들기.
- DROP - 이미 존재하는 데이터베이스 관계 ( 테이블 ) , 뷰 , 인덱스 , 저장 프로시저를 삭제한다.
- ALTER - 이미 존재하는 데이터베이스 개체에 대한 변경 , RENAME의 역할을 한다.
- TRUNCATE - 관계 ( 테이블 )에서 데이터를 제거한다. ( 한번 삭제시 돌이킬 수 없음.)




## 데이터 조작 언어 - ( DML : Data Manipulation Language )
<span style="background-color:yellow"><b> 테이블에 데이터 검색, 삽입, 수정, 삭제하는 데 사용 </b></span>
- SELECT - 검색(질의)
- INSERT - 삽입(등록)
- UPDATE - 업데이트(수정)
- DELETE - 삭제




## 데이터 제어 언어 - ( DCL : Data Control Language )
<span style="background-color:yellow"><b> 데이터의 사용 권한을 관리하는 데 사용 </b></span>
- GRANT - 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 부여한다.
- REVOKE - 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 박탈 or 회수 한다.


### 데이터베이스 사용자에게 GRANT 및 REVOKE로 설정 할 수 있는 권한.
- CONNECT - 데이터베이스 or 스키마에 연결하는 권한.
- SELECT - 데이터베이스에서 데이터를 검색할 수 있는 권한
- INSERT - 데이터베이스에서 데이터를 등록(삽입)할 수 있는 권한
- UPDATE - 데이터베이스의 데이터를 업데이트 할 수 있는 권한
- DELETE - 데이터베이스의 데이터를 삭제할 수 있는 권한.
- USAGE - 스키마 또는 함수와 같은 데이터베이스 개체를 사용할 수 있는 권한




# DELETE, TRUNCATE, DROP의 차이
- DELETE
  - 데이터는 지워지지만 테이블 용량은 줄어 들지 않는다.
  - 원하는 데이터만 지울 수 있다.
  - 잘못 삭제 한 경우 삭제한것을 되돌릴 수 있다.
- TRUNCATE
   - 삭제후 용량이 줄어들고 인덱스 등도 모두 삭제된다.
   - 테이블이 삭제 되지는 않으나 데이터만 삭제한다.
   - 선택해서 지울 수 없다.
   - 삭제 후 절대 되돌릴 수 없다
- DROP
  - 테이블 전체를 삭제, 공간, 객체를 삭제한다,
  - 삭제 후 절대로 되돌릴 수 없다.



---
참고
SQL정의 :  
[https://ko.wikipedia.org/wiki/SQL]  

ddl,dml,dcl 차이:  
https://brownbears.tistory.com/180  
https://zzdd1558.tistory.com/88  
