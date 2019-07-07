---
layout: post
section-type: post
title: "(작성중)[legacy 환경설정으로 얻은 지식들] (JSP) Model, ModelAndView 사용법"
category: Spring
tags: [ 'Spring', '환경설정', 'SKencar', 'JSP' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---
기본적인 흐름  
<span style="background-color:black; color:white;"><b> client가 요청 -> @Controller 에 진입 -> @Controller 요청에 대한 작업 수행 ->  @Controller 뷰쪽으로 데이터 전달 </b></span>




# 컨트롤러 클래스 제작 순서
1. @Controller를 이용해서 클래스를 생성한다.
2. @RequestMapping을 이용해, view의 요청 경로 지정한다.
3. 요청 처리 메소드(로직) 구현한다.
4. 뷰 이름 리턴한다.

``` java
@Controller // 컨트롤러 지정
public class HomeController {

    // 뷰의 요청 경로 지정
    @RequestMapping(value = "/", method = RequestMethod.GET)
    public String home(Locale locale, Model model) {

        // 로직 수행
        logger.info("Welcome home! The client locale is {}.", locale);
        Date date = new Date();
        DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
        String formattedDate = dateFormat.format(date);

        // Model 객체를 이용해서, view로 Data 전달
        model.addAttribute("serverTime", formattedDate );

        return "home"; // 뷰 파일 리턴
    }
}
```



# Model 객체 사용법
Model 객체를 파라미터로 받아서 데이터를 뷰로 넘길 수 있다.

``` java
@RequestMapping("/singer/plan")
public String view(Model model) {
    // 데이터만 설정이 가능
    model.addAttribute("singer", "IU");
    return "singer/plan";
}

```
Model 객체를 파라미터로 받는다.

``` java
model.addAttribute("변수이름", "변수에 넣을 데이터값");
```

- model.addAttribute를 이용해서, 넘길 데이터의 이름과 값을 넣는다.
- 그러면, 스프링은 그 값을 뷰쪽으로 넘겨준다.

> ${변수이름}

즉 뷰에서는 ${}를 이용해서 값을 가져온다.  
> 당신의 가수는 ${singr} 입니다.  

이면 "당신의 가수는 IU 입니다"로 뜹니다.(url은 /singer/plan 이다.)  



# ModelAndView 객체 사용법
가장 큰 차이점은 반환값으로 ModelAndView 객체를 반환한다  

``` java
@RequestMapping("/singer/favorite")
public ModelAndView content() {
    // 데이터와 뷰를 동시에 설정이 가능
    ModelAndView mv = new ModelAndView();
    mv.setViewName("/singer/favorite"); // 뷰의 이름
    mv.addObject("singer", "IU"); // 뷰로 보낼 데이터 값

    return mv;
}
```

1. ModelAndView 객체를 선언 및 생성한다.
2. 뷰의 이름을 설정하기 위해 setViewName() 메소드를 사용
  - ``` mv.setViewName("뷰의 경로"); ```
3. 데이터를 보내기 위해 addObject() 메소드를 사용
  - ``` mv.addObject("변수 이름", "데이터 값"); ```
4. ModelAndView 객체를 반환한다.
  - ``` return mv; ```

> 나의 최애 아이돌은 ${singer} 이다.

이건 ``` 나의 최애 아이돌은 아이유 이다. ``` 가 된다.
url은 /singer/favorite 되있다.




---
출처: https://hongku.tistory.com/116 [IT에 취하개 :: 취미로 하는 개발]
