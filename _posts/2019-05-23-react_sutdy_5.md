---
layout: post
section-type: post
title: "(작성중) [react study 5]javascript falsy"
category: Javascript
tags: [ 'Javascript', 'react' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

- local storage 에 저장하는 부분은
should component에 넣어서 아이에 한 method로 빼는 게 좋을 것 같다,

- client side 랜더링


# 코드 스플리팅
클라이언트 사이드 렌더링의 단점으로 점점 프로젝트의 규모가 커질 수록 js 파일의 크기가 커지고 초기에 이를 모두 로드하기 때문에 초기 로딩시간이 길어지게 됩니다.

이를 해결하기 위한 방법이 코드 분할, 코드 스플리팅 입니다.

## 1. dynamic import (동적 import)

before
```js
    import { add } from './math';
    console.log(add(16, 26));
```
after
``` js
    import("./math").then(math => {
      console.log(math.add(16, 26));
    });
```


아직 표준 문법이 아니라 제안 상태 입니다.

현재 stage3 이기 때문에 가까운 미래에 표준이 될 것으로 보입니다.

webpack이 이 구문을 만나게 되면 앱의 코드를 분할 하여 별로의 js로 빌드 합니다.
*즉 진짜 사용될 때 보는 것이다.*
 create react app을 사용하고 있다면 별도의 설정없이 사용가능합니다.

실제 리액트 컴포넌트 스플리팅에 사용하기에는 불편한 부분이 있습니다.


## 2. React.lazy

리액트에서 지원하는 lazy 함수를 사용할 수 있습니다.

아직 서버 사이드 렌더링을 지원하지 않습니다. 그렇기 때문에 서버 사이드 렌더링을 하려고 하면 공식 문서에서는 loadable-components 모듈을  추천하고 있습니다.

[https://github.com/smooth-code/loadable-components](https://github.com/smooth-code/loadable-components)

before

    import OtherComponent from './OtherComponent';

    function MyComponent() {
      return (
        <div>
          <OtherComponent />
        </div>
      );
    }

after

    const OtherComponent = React.lazy(() => import('./OtherComponent'));

    function MyComponent() {
      return (
        <div>
          <OtherComponent />
        </div>
      );
    }

*버튼 클릭시 불러오니까 그러다보면 사용자가 빈 화면을 볼수도 있다.
그래서 suspense를 사용하는 것이다.*
### Suspense

컴포넌트를 로드하는 동안 보여질 내용을 정의할 수 있습니다.
``` js
  const OtherComponent = React.lazy(() => import('./OtherComponent'));
  const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

  function MyComponent() {
    return (
      <div>
        <Suspense fallback={<div>Loading...</div>}>
          <section>
            <OtherComponent />
            <AnotherComponent />
          </section>
        </Suspense>
      </div>
    );
  }
```

OtherComponent, AnotherComponent 둘 다 되기 전까지는 suspense만 가져온다.
OtherComponent만 성공했다. 그럼 AnotherComponent일 때는 suspense하나로 묶어놓으면 어떤 callback이 나오는가?

## 적용

모든 코드를 코드 스플리팅 하는 것은 안좋고, 특정 것만 해야한다.
왜냐면 자꾸 깜빡이면서 불러오기 때문이다.
page단위로 스플리팅을 적용한다.

사용자 경험을 해치지 않고 코드 스플리팅을 도입할 부분을 결정하는 것은 조금 까다롭습니다.

보통 코드 스플리팅을 모든 컴포넌트에 적용하기 보다는 페이지 (라우팅) 단위로 적용하는 것을 공식 문서와 다양한 사례에서 추천합니다.
``` js
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import React, { Suspense, lazy } from 'react';

    const Home = lazy(() => import('./routes/Home'));
    const About = lazy(() => import('./routes/About'));

    const App = () => (
      <Router>
        <Suspense fallback={<div>Loading...</div>}>
          <Switch>
            <Route exact path="/" component={Home}/>
            <Route path="/about" component={About}/>
          </Switch>
        </Suspense>
      </Router>
    );
    ```
