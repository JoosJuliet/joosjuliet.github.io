---
layout: post
section-type: post
title: "URL 인코딩 및 디코딩, 한글 인코딩, %인코딩 처리, Percent-encoding"
category: Web
tags: [ 'Web', 'encoding', 'decoding' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# Character Set(Character encoding)이란?
- Character Set(문자셋) 그리고 Character encoding(문자 인코딩)은 같은 말로 쉽게 말해서 어떤 인코딩 시스템에 의해서 존재하는 문자들을 표현하려는 방법을 의미한다.
- ASCII나 Unicode가 문자 인코딩들의 대표적으로 알려진 예시입니다.


# Percent-encoding이란?
- Percent-encoding이란 URI 혹은 URL에 문자를 표현하는 인코딩 방식으로 ``` RFC 3986 ``` 에 따라서 알파벳이나 숫자 등 몇몇 문자를 제외한 문자들에 대해서 옥텟 값으로 묶어서 16진수 값으로 코딩하는 방식
- 예시 : "/internet url" -> "internet%20url"


# Percent-encoding의 방법
- ``` RFC3986 ``` 문서를 찾아보면 정해진 몇몇개의 문자들을 제외하고는 octet(8bit가 한데 모인 것)으로 인코딩한 후에 %를 붙여서 인코딩 한다고 나와있다.
- 여기서 한국어는 octet(8bit가 한데 모인 것)으로 변형되어서 표시되며 Unicode에 따라서 UTF-8 방식으로 바뀌어서 인코딩 되게 됩니다.


# 인코딩이란?
- 정보의 형태나 형식을 변환하는 처리나 처리 방식
- 내용에는 변화가 없다
- 암호화로는 사용 불가능
- 종류로는 ASCII , URL , HTML , Base64 , MS Script 인코딩이 있다

전기환경차 검색,
http://localhost:8080/ev/ev_carsearchlist.do?carType=ev&searchType=model&wtClick_kor=003&TG.R=D#!
엔카진단차량
http://localhost:8080/ev/ev_carcheckedlist.do?carType=ev&wtClick_kor=053&TG.R=D1#!
헛걸음 보상차량
http://localhost:8080/ev/ev_carcompensatelist.do?carType=ev&WT.hit=header_carcompensatelist&TG.R=F1#!
# 디코딩이란?

# percent-encoding
- URL encoding
- Percent-encoding이란 URI 혹은 URL에 문자를 표현하는 인코딩 방식
- *RFC3986* 에 따라서 알파벳이나 숫자 등 몇몇 문자를 제외한 문자들에 대해서 옥텟 값으로 묶어서 16진수 값으로 코딩하는 방식
- 예시) "/internet url" -> "internet%20url"

*RFC3986*
- URI 표준 규정




# encodeURI()와 decodeURI() 함수
encodeURI() : 일반 문자열을 퍼센트 인코딩된 문자열로 변환
decodeURI() : 인코딩된 문자열을 일반 문자열로 변환



---
참고:  
https://itstory.tk/entry/인코딩이란-ASCII-URL-HTML-Base64-MS-Script-인코딩 [덕's IT Story]  
https://twpower.github.io/113-uri-encode-decode-in-javascript  
https://twpower.github.io/123-how-to-encode-korean-to-percent-encoding  
