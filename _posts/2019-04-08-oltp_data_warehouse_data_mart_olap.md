---
layout: post
section-type: post
title: "OLTP, Data Warehouse, Data Mart, OLAP 용어정리"
categories: DB
tags: [ 'DB', 'database', 'computer_science' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

<img alt="flow" src = "/images/2019-04-08-oltp_data_warehouse_data_mart_olap/flow.png
"/>

# Batch Processing
- <span style="background-color:yellow"><b> 작업을 몰아두었다가 한번에 처리하는 시스템 </b></span>
- 예)선거투표결과 추출, 게임 이벤트 아이템 일괄 지급 등




# OLTP(OnLine Transaction Processing)
- <span style="background-color:yellow"><b> 실시간으로 db의 데이터를 트랜잭션 단위로 갱신/조회하는 처리방식 </b></span>
- Batch 와 반대되는 개념
- 예)은행, 증권사 등에서 씀. 기존과 달리 다수의 client가 거의 동시에 이용할수 있도록 송수신자료를 트랜잭션단위로 압축한것이 특징.




# DW(Data Warehouse)
- <span style="background-color:yellow"><b> 중앙집중식 데이터 집합체의 개념 </b></span>
- DW는 기존 데이터를 어떻게 수집/분석하고 어떻게 재사용할 것인가에 초점  
- 수년간 발생한 데이터를 모아서 주제별로 합쳐 분석할 수 있게 하는 통합시스템.  
- 예) 운영데이터, 분산데이터, 시장데이터를 추출하여 DW를 구축하고 그걸 DSS나 OLAP로 분석




# Data Mart  
- <span style="background-color:yellow"><b> data mart는 데이터 저장소의 역할을 하고 특정 목적을 위해 쉬운 접근성과 사용성  </b></span>
- DW의 하위단위




# OLAP(OnLine Analytical Processing)
- <span style="background-color:yellow"><b> DW에서 데이터를 분석해서 의미있는 형태로 만들기 위한 과정및 도구 </b></span>
- 의사결정 지원 시스템의 하나.




---
참고자료:  
https://118k.tistory.com/66  
