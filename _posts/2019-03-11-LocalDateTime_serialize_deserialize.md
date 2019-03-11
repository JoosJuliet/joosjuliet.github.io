---
layout: post
section-type: post
title: "(alpha)[SpringBoot] json-jpa LocalDateTime serialize deserialize"
category: SpringBoot
tags: [ 'SKencar', 'json', 'SpringBoot', 'serialize', 'deserialize' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.  
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.  
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.  
감사합니다:)  
---

초기에 직렬화를 못해 String으로 받은 후 서비스 레이어에서 변환을 했었다.  
spirng 에는 직렬화 과정을 쉽게 해결할 수 있는 법이 있다. ~근데 난 이것도 번거롭긴하다.~

# 1. Request - 직렬화(Serialize)
@JsonFormat, @DateTimeFormat  어노테이션 모두가 있으면 @JsonFormat이 진행된다  
@JsonFormat이 틀리면 @DateTimeFormat이 맞더라도 직렬화는 실패한다  
단, @DateTimeFormat이 있다면 @DateTimeFormat의 포맷으로 직렬화가 진행된다.  


@DateTimeFormat은 Spring에서 지원하는 어노테이션으로 LocalDate와 LocalDateTime와 같은 날짜 관련 타입의 직렬화를 지원하는 어노테이션입니다.  
``` java

@DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss")  

```
@RequestParamter 는 날짜 직렬화가 필요할 경우 @DateTimeFormat을 사용하면 된다  


Post로 보내는 Request Body (JSON 객체)는 @DateTimeFormat과 @JsonFormat 모두 사용할 수 있음  

# 2. Response Body - 비직렬화(deserialize)

@DateTimeFormat 에서 실패  
 Response Body에서는 @JsonFormat만 가능  


# 3. @DateTimeFormat vs @JsonFormat
- @JsonFormat 은 Jackson의 어노테이션이고,
- @DateTimeFormat 은 Spring의 어노테이션

## @JsonFormat 이란?
<span style="background-color:yellow"><b> @JsonFormat 은 LocalDate 혹은 LocalDateTime을 JSON으로 직렬화할때 포맷 </b></span>
- Spring의 기본 JSON 컨버터는 Jackson, JSON으로 변환을 할때 Jackson을 통해서 진행
- JSON 직렬화 과정에서 @JsonFormat이 없다면 Spring에서는 @DateTimeFormat를 통해 직렬화를 진행
- 반면 Jackson은 Spring의 어노테이션인 @DateTimeFormat 을 전혀 알 수 없습니다.
*둘은 완전히 별개의 라이브러리들*

- 그래서 @DateTimeFormat 을 지정했다 하더라도, Jackson은 이 어노테이션을 전혀 고려하지 않고 JSON 직렬화을 진행
- <b> JSON 직렬화 외에는 Jackson이 사용되지 않기 때문에 @JsonFormat은 효과가 없습니다. </b>
- 그래서 RequestParameter나 ModelAttribute에선 @DateTimeFormat 만 적용될 수 있습니다.

# 결론
- Get요청시에는 @DateTimeFormat
- Post 요청, ResponseBody에서는 @JsonFormat
- Post 요청시에도 @DateTimeFormat이 적용될 수 있으나, @JsonFormat이 지정되어 있지 않을때만 가능하다.


---
참고:  
https://jojoldu.tistory.com/361
https://www.baeldung.com/jackson-jsonformat
