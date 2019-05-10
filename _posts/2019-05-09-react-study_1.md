---
layout: post
section-type: post
title: "[React] react 점심스터디(react-route, link, exact, NavLink, props)"
category: React
tags: [ 'React', 'SKEncarLunchStudy' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---


src에서 jsconfig.json라는 파일을 넣어서 env 들을 관리할 수 있다.
그러면 상대경로를 안 쓸 수 있어서 좀 더 보기 좋다.

# 리엑트 라우팅
react-router-dom으로 한다.

## Link란?
a tag와 같은 역할을 한다.
Router를 감싸면 페이지 라우팅이 가능하다.
이걸 이용해서 page 깜박임 없이, spa쓸 수 있다.

## exact란?
/를 기반으로 먼가를 하면은 무조건 그 밑에 나온다.
그래서 *exact* 를 쓴다.
``` html
<li><NavLink to="/" exact activeClassName="red">home</NavLink></li>
```

## props는?
router를 썼기 때문에 props가 생긴다.
route로 그린 컴포넌트만 props를 가지게 된다.

## NavLink란?
하이라이팅 된다.
``` html
<li><NavLink to="/" exact activeClassName="red">home</NavLink></li>
```
route와 같은 문제가 일어날 수 있음으로 exact를 써야한다.

``` html
<Route path={['/list', '/items']} component={List} />
```
이렇게 쓸수 도 있따.
그러면 /list일때랑 /items 모두에서 List가 나온다.
