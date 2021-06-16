---
layout: post
section-type: post
title: "pojo란? JavaBean이란? "
category: Java
tags: [ 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

# pojo란?!
## overview
- Plain Old Java Object
- 보통 JavaBean과 비교를 많이 당한다.
- pojo는 java bean으로 바꿀 수가 있는데 어떻게 바뀌는 지에 보면 도움이 된다.




## POJO가 그래서 뭔데
- 포조는 어떤 프레임워크랑도 연관이 없는 그 자체이다.

``` java
public class SingerPojo {

    public String name;
    public String nickName;
    private LocalDate startDate;

    public SingerPojo(String name, String nickName, LocalDate startDate) {
        this.name = name;
        this.nickName = nickName;
        this.startDate = startDate;
    }

    public String name() {
        return this.name + " " + this.nickName;
    }

    public LocalDate getStart() {
        return this.startDate;
    }
}
``` 




# Java Bean
- Java bean은 단지 기준일 뿐이다.
- 단일 객체로 캡슐화를 목적으로 만들어진 클래스





## Java Bean의 필수사항
1. access level
- 모든 필드는 private이며, getter/setter메서드를 통해서만 접근이 가능하다.

2. default constructor
- Argument가 없는(no-argument) 생성자가 존재한다.

3. serializable
- java.io.Serializable 인터페이스를 구현한다.




## 코드
``` java
import java.io.Serializable;

public class SomeBean implements Serializable {
    private String beanName;
    private int beanValue;

    public SomeBean() {
        // no-argument constructor
    }

    public String getBeanName() {
        return beanName;
    }

    public void setBeanName(String beanName) {
        this.beanName = beanName;
    }

    public int getBeanValue() {
        return beanValue;
    }

    public void setBeanValue(int beanValue) {
        this.beanValue = beanValue;
    }
}
```



