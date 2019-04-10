---
layout: post
section-type: post
title: "Spring MVC UriComponentsBuilder(서버단에서 쉽게 URI 만들기)"
category: Spring
tags: [ 'Spring', 'java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---

UriComponentsBuilder의 주된 장점은 URI 템플릿 변수의 유연성과 Spring Controller 메소드에 직접 삽입 할 수 있다는 것입니다.


Spring 서버단에서 문자열 URI를 만들어야 할때가 있다.
자바 String으로 만들어도 되지만!
Spring MVC의 org.springframework.web.util 패키지의 UriComponentsBuilder를 사용하면 조금더 쉽고, 명확하게 URI 문자열을 생성


 @Value("${encar.api.location.url}")
    private String locationUrl;

URI같은 것을 동적으로 만드는 거 자체가 짜증나

```java

URI uri = UriComponentsBuilder.fromUriString(legacyViewUrl)
                .path("/trend/target/dealers/sale/car")
                .queryParams(request.toMap())
                .build()
                .encode()
                .toUri();


@Test
	public void testURI() throws Exception{

		UriComponents uriComponents = UriComponentsBuilder.newInstance()
				.path("/samplehome/board/read")
				.queryParam("bno", 12)
				.queryParam("perPageNum", 20)
				.build();

		logger.info("/samplehome/board/read?bno=12&perPageNum=20");
		logger.info(uriComponents.toString());  // /samplehome/board/read?bno=12&perPageNum=20 가 생성된다.
	}

	@Test
	public void testURI2() throws Exception{
		UriComponents uriComponents = UriComponentsBuilder.newInstance()
				.path("/{a}/{b}/{c}")
				.queryParam("bno", 12)
				.queryParam("perPageNum", 20)
				.build()
				.expand("samplehome", "board", "read")
				.encode();

		logger.info("/samplehome/board/read?bno=12&perPageNum=20");  
		logger.info(uriComponents.toString()); // /samplehome/board/read?bno=12&perPageNum=20 가 생성된다.
	}
```

In addition to creating a simple link, we may want to encode the final result. Let’s see this in practice:

---
참고자료:

https://blog.hanumoka.net/2018/08/10/spring-20180810-spring-UriComponentsBuilder/(이거 보면 되게 좋다.)

https://www.baeldung.com/spring-uricomponentsbuilder
