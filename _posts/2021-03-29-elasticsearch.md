---
layout: post
section-type: post
title: "왜 elasticsearch는 빠를까?"
category: DataBase
tags: [ 'DataBase', 'elasticsearch' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

# 이글을 쓴 이유
elasticsearch을 회사에서 대충대충(?) 쓰고 있었다.
검색에 최적화 되있다고 해서… 그렇구나? 뭔가 index라는 개념이 있네  
index를 걸면 빠르니까 그래서 빠르구나(?) 이러고 있었다.  
그리고 그것이 다가 아니었다.    


빠른 이유를 가장 크게는 두가지 이유 덕분이다.
- Inverted Index
- sharding




# 첫번재인 Inverted Index
- word가 key가 되고 그 word가 존재하는 Document 들이 value가 된다.
- 마치 책을 읽을 때 가장 뒤쪽에 있는 특정 단어가 어디페이지에 있는지를 알려주는 목차와 형태가 비슷하다 보면 된다.
- Elasticsearch는 Open Source Project인 Apache Lucene을 기반으로 만들어진 Search Engine이다.
- 이 Apache Lucene에서의 Index는 Inverted Index를 사용하기 때문에, Elasticsearch도 그러하다.




# 두번째 Sharding
- elasticsearch의 sharding 기본 개수는 5개이다.   
- `데이터가 너어무 많아서 검색이 느린데 빠를 방법이 없을까? -> 테이블 나눠서 검색~!` 인데 이걸 구현한 것이 sharding이다.
- 즉 어떤 shard에 있는지만 알면 검색이 더 빠를수 밖에 없다.
- 색인은 방대한 양의 데이터를 저장할 수 있는데, 이 데이터가 단일 노드의 하드웨어 한도를 초과할 수도 있습니다. 
- 예를 들어 10억 개의 문서로 구성된 하나의 색인에 1TB의 디스크 공간이 필요할 경우, 단일 노드의 디스크에서 수용하지 못하거나 단일 노드에서 검색 요청 처리 시 속도가 너무 느려질 수 있습니다.
- Elasticsearch는 이러한 문제를 해결하고자 색인을 이른바 샤드(shard)라는 조각으로 분할하는 기능을 제공합니다. 
- 색인을 생성할 때 원하는 샤드 수를 간단히 정의할 수 있습니다. 각 샤드는 그 자체가 온전한 기능을 가진 독립적인 "색인"이며, 클러스터의 어떤 노드에서도 호스팅할 수 있습니다.




## 고려사항
- 분산된 db 에 data를 어떻게 잘 분산시켜 저장?
- 분산된 db에서 data 어떻게 읽을 것인가?




## sharding 종류
### Shard key
- 나눠진 shard중 어떤 shard를 선택할지 결정하는 키
- Shard key 결정 방식에 따라 sharing 방법이 나뉜다.



### Hash Sharding
- shard 0~3 이 샤드키
- 구현쉬움 -> 구현자체 hash수만큼 샤딩하면 되니까
- 샤드 늘어나면 해시함수 달라져야해서 적합성이 달라져서 확장성 달라진다
- 공간 효율성도 생각 x


### Dynamic Sharding
- 공간효율성 생각
- 샤드 하나 생겨서 locator service나온다.
- 단점 -> 나머지 샤드들이 해당 서비스에 종속적이여서 장애전파된다.




---
참고:  
Open Distro ->Amazon Web Services 에 올려놓은 elastic search정보들  
https://opendistro.github.io/for-elasticsearch-docs/  
[10분 테코톡] 👨‍💻히브리의 Sharding, Clustering, Replication : https://www.youtube.com/watch?v=y42TXZKFfqQ  
elastic search 기본개념 : https://www.elastic.co/guide/kr/elasticsearch/reference/current/gs-basic-concepts.html  
https://www.elastic.co/guide/en/elasticsearch/reference/current/scalability.html -> 이건 공식문서  
