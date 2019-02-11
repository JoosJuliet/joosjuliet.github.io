---
layout: post
section-type: post
title: "[db index 3편] index structure의 종류와 선정 지침 (인덱스 선정 지침이란?, 인덱스가 사용되지 않는 경우는?, query tuning을 위한 추가 지침)"
categories: DB
tags: [ 'DB', 'database', 'index', 'computer_science', '글또2기' ]
comments: true
---

이 컨텐츠는 시리즈물입니다.  
[db index 1편] index 란?: https://joosjuliet.github.io/index/  
[db index 2편] index structure란?: https://joosjuliet.github.io/index_structure/   


#시리즈를 마치며 quiz
## 왜 DB 테이블의 모든 컬럼에 인덱스를 걸면 어떻게 될까?
- 인덱스를 생성하면 레코드가 추가/삭제/변경 될때마다 인덱스 값도 추가/삭제/변경해야 함 -> Disk I/O를 유발, 공간을 차지함.
- InnoDB의 인덱스는 B+ Tree인데, CRUD할 때마다 Tree를 reorganization해줘야 함. -> 비용이 많이 듬. Bulk loading이 대안책!
- Bulk loading이란? 삭제할 때 reorganization 해야하는데, 그냥 표시만 해놓는다. 삭제는 안하고, 실 데이터보다 index크기가 더 커질수 있다.


## 인덱스 선정 지침이란?
- tuple이 많이 들어있는 대용량의 relation
- relation에서 대부분의 query가 검색하는 tuple이 2%~4% 인 경우에는 인덱스를 생성하는 것이 좋다.
- 가능하면 한 relation에 세 개 이하의 인덱스를 만드는 것이 좋다. -> CRUD가 일어나면 인덱스를 많이 업데이트 해야하니까!
- 갱신이 빈번하게 이루어지는 attribute/relation은 인덱스를 많이 만드는 것을 피해야한다.
- file의 recode들을 충분히 분할할 수 있어야 한다.
- 가능하면 Integer Attribute에 인덱스를 만드는 것이 가장 좋고, 고정 길이 attribute에 인덱스를 만드는 것이 좋다. 이유는…모른다! 댓글좀 달아주세요!
- 대량의 데이터를 삽입할 때는 모든 인덱스를 제거하고 데이터 삽입이 끝난 후에 인덱스들을 다시 생성하는 것이 좋다.


## 인덱스가 사용되지 않는 경우는?
- relation의 크기가 너무 작아서 인덱스가 도움이 되지 않는다고 판단되었을 경우(손익분기점을 넘었을 경우)
  - mysql에서 손익분기점을 못넘으면 index를 자동으로 사용안한다
- attribute에 산술연산자가 사용되었을 경우
  -  ``` WHERE SALARY * 12 > 400000000;```
  - 12에 대한 index가 없어서, 그럼 index사용안된다.
- 널값에 대해서는 인덱스가 사용되지 않음 
  - ``` WHERE MANAGER Is NULL; ```
- != 는 sql <>가 문법인데 이거에는 index가 사용 x


## query tuning을 위한 추가 지침
- GROUP BY HAVING의 사용을 느리니까 최소화 해라(임시공간 사용, 다 돌면서 group도 지어야한다)
- group by와 where의 차이는 group by는 이건 뇌피셜 임시공간 필요없다. group by는 전체 테이블을 full search해야한다.
- 중복이 많이 없으면 N**2 ``` select sum(*) from employee group by salary; ```
- 임시 relation을 웬만해선 사용하지 말자.
- ``` SELECT * FROM … ``` 대신에 ``` SELECT atr1, atr2 FROM … ``` 같이 구체적으로 attribute를 명시하자.  


---
참고:  Index관련 동영상 강의: https://www.youtube.com/watch?v=de0Ky5IhW0E  
