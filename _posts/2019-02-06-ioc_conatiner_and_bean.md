---
layout: post
section-type: post
title: "[Spring] IoC(Inversion of Control) 컨테이너와 빈"
category: Spring
tags: [ 'Spring', 'Java', 'SKEncar', 'JPA' ]
comments: true
---
(소개와 이해를 중심)
학습 목표:
- 스프링 프레임워크의 핵심 기술 IoC, AOP, PSA를 이해합니다.
- 스프링 프레임워크 IoC 컨테이너의 다양한 기능을 사용할 수 있습니다.
- 다양한 방법으로 빈을 정의하고 의존 관계를 주입할 수 있습니다.




스프링 부트의 시작점인 Application 클래스는 보통 아래와 같은 구조를 가지고 있다.

(Spring Boot 2.x에서는 `@SpringBootApplication` 을 사용한다.)

    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.boot.builder.SpringApplicationBuilder;

    @SpringBootApplication
    public class Application {
    	public static void main(String[] args) {
    		new SpringApplicationBuilder(Application.class).run(args);
    	}
    }

이`@SpringBootApplication` 을 열어보면 아래와 같은 구조를 가지고 있다.

여기서부터 하나씩 알아보자.

    @Target(ElementType.TYPE)
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Inherited
    @SpringBootConfiguration
    @EnableAutoConfiguration
    @ComponentScan(excludeFilters = {
    		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
    		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
    public @interface SpringBootApplication {
     //...
    }

## 빈 등록하기 - `@ComponentScan`

스프링에서 관리하는 POJO(Plain Old Java Object)를 '빈(Bean)'이라 한다.

`@ComponentScan` 어노테이션은 현재 패키지 이하에서 `@Component` 어노테이션이 붙어 있는 클래스들을 찾아서 빈으로 등록하는 역할을 한다.

    @Controller
    public class XXController {
    	//...
    }

`Spring MVC` 에서 자주 사용되는 `@Controller` 어노테이션도 내부를 까보면 이 `@Component` 를 가지고 있는 것을 확인할 수 있다.

    @Target({ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Component
    public @interface Controller {

    	/**
    	 * The value may indicate a suggestion for a logical component name,
    	 * to be turned into a Spring bean in case of an autodetected component.
    	 * @return the suggested component name, if any (or empty String otherwise)
    	 */
    	String value() default "";

    }

심지어 설정 파일 어노테이션인 @Configuration 자체도 @Component이다.

    @Target({ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Component
    public @interface Configuration {
        @AliasFor(
            annotation = Component.class
        )
        String value() default "";
    }

# 설정 자동 등록하기 - `@EnableAutoConfiguration`

`@EnableAutoConfiguration` 은 Spring Boot의 핵심으로써, 미리 정의되어 있는 빈들을 가져와서 등록해준다.

요 녀석도 @SpringBootApplication 어노테이션에 포함되어 있다.

    @Target(ElementType.TYPE)
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Inherited
    @SpringBootConfiguration
    @EnableAutoConfiguration
    @ComponentScan(excludeFilters = {
    		@Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
    		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
    public @interface SpringBootApplication {

**@EnableAutoConfiguration**

    public @interface EnableAutoConfiguration {

    	String ENABLED_OVERRIDE_PROPERTY = "spring.boot.enableautoconfiguration";

그렇다면 기본적으로 설정되어 있는 빈들은 어디에 정의되어 있는 것일까?

그 빈들은 외부 라이브러리(External Libraries)중 spring-boot-autoconfigure에 정의되어 있다.


---
참고자료:
백기선님 강의 [스프링 프레임워크 핵심 기술]  https://www.inflearn.com/course/spring-framework_core  
https://www.notion.so/Spring-Boot-Config-Annotation-315eb0d5a947457f944309f23290f514  
