---
layout: post
section-type: post
title: "(작성중)[db index 2편] index structure의 종류? (cluster index, non-cluster index )"
categories: DB
tags: [ 'DB', 'database', 'index', 'computer_science' ]
comments: true
---



# Index Architecture
![clustered vs non-clustered index](https://dl.dropbox.com/s/ac278pxr0ujg3rq/Screenshot%202019-01-09%2017.05.54.png)

실제 데이터 엔트리와 데이터 레코드의 순서가 같으면 Clustered Index, 아니면 Non-Clustered Index


## Clustered Index
- clustered index가 걸린 컬럼은 자동으로 그 컬럼을 기준으로 정렬한다.(테이블 당 하나의 컬럼만 가능)
  - 두개의 컬럼에 하면 정렬이 불가능함으로

![clustered index](https://dl.dropbox.com/s/77rvc1e8ae45boa/Screenshot%202019-01-09%2018.59.09.png)

- primary index에 주로 clustered index를 적용(primary key를 걸면 default로 clustered index가 걸린다.)
- 범위의 시작값을 찾고 연속된 디스크 블록을 읽으면 되니, Range Query에 좋다.
  - hard disk에는 세가지 time이 있다.
    - 1.seek time (어떤 track을 찾는냐)
    - 2.rotation latency(원판 도는 time)
    - 3.transmission time(data 읽어서 전송하는 시간)
  disk가 원판으로 생겨서 돌아가면서 데이터를 읽는다.
  원판에는 track이 있고 그 track들에 data가 들어가 있는것이다. 가장 오래걸리는 시간은 seek time 그런데 data 연속되 있으면 1,2번이 적어서 물리적으로 효율 적이다. 그래서 range query가 좋다


## Non-Clustered Index
- 특정 index에 맞춰서 ordering할 필요가 없으니 테이블 당 여러개의 컬럼에 index 거는 게 가능
- secondary index에 주로 non-clustered index를 적용

![non-clustered index](https://dl.dropbox.com/s/ll1o7dn5lihia96/Screenshot%202019-01-09%2019.03.12.png)

- Range Query를 하면 데이터 레코드를 읽을 때마다 매번 디스크 블록에 접근 -> 접근 횟수가 db 성능에 critical
- 따라서 해당하는 데이터 엔트리를 찾는 속도는 (index 없는 것 보다) 빠르지만, 레코드를 읽는 속도는 (clustered index보다 상대적으로)느리다.
- mysql의 InnoDB의 경우 unique를 걸면 자동으로 non-clustered index가 걸린다.
  - unique는 중복이 제거된 것이기 때문에 indexing이 되면 효율이 높아지기 때문에 optimizer가 자동으로 해준다.


### etc
- 순차탐색(처음부터 차례대로 찾는 것), index걸면 순차탐색보다 더 안좋아 질 수도 있다.
  - 중복데이터가 많은 경우이다.
    - tree형태로 되있어서 계속 찾아다니므로 순차탐색보다 더 느리다.
  - 중복 없을 때는 index효율이 좋다.
- equality 연산은 index에 좋다.
- InnoDB에서는 Foreign key를 써도 자동으로 non-cluster Index를 생성한다.
  - join연산을 where문 속에 넣으면 primary key와 foreign key의 equality연산을 하기 때문이다.

---
참고:
InnoDB는 B+tree를 사용한다: https://blog.jcole.us/2013/01/10/btree-index-structures-in-innodb/
B-tree 관련: https://medium.com/@mena.meseha/what-is-the-difference-between-mysql-innodb-b-tree-index-and-hash-index-ed8f2ce66d69
DB테이블에 전부 인덱스를 걸면? : https://hashcode.co.kr/questions/1551/%EC%99%9C-db-%ED%85%8C%EC%9D%B4%EB%B8%94%EC%9D%98-%EB%AA%A8%EB%93%A0-%EC%BB%AC%EB%9F%BC%EC%97%90-%EC%9D%B8%EB%8D%B1%EC%8A%A4%EB%A5%BC-%EA%B1%B8%EB%A9%B4-%EC%95%88%EB%90%98%EB%82%98%EC%9A%94
Index관련 동영상 강의: https://www.youtube.com/watch?v=de0Ky5IhW0E
Fractal Tree - https://12bme.tistory.com/143?category=682920 - http://gywn.net/2014/05/fractal-index-in-tokudb/
