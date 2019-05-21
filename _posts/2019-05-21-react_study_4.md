---
layout: post
section-type: post
title: "(작성중) javascript falsy"
category: Javascript
tags: [ 'Javascript', 'falsy' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

# falsy값
- undefined
- nullable
- False
- 0, -0, NaN(조건절에서 false)
- ""(빈문자열도 false된다.)


falsy값 아니면 다 true다.

``` javascript
var a = 42
var b = 'abc',
var c = null
```
---
a||b
42
---
a && b  -> a 반환 후 b반환해서 b까지 연산갔으니 b값 반환한다.
'abc'
---
c || b -> c가 false이기 때문에 b까지 연산이 가고 그래서 b값 반환
'abc'
---
c && b  -> c이미 false이기에 이미 연산이 끝났음으로 c로 간다.
null
---
*예외*
근데 이거쓸일은 거의 없다.
documnet.all이라는 falsy한 객체도 있다.


``` javascript

function foo(a, b) {
	a = a || 'hello';
	b = b || 'world';

	console.log(a + ' ' + b);
}

foo(); // hello world
foo('오 마이', '갓!'); // 오마이 갓!
foo('그렇군!', ''); // 그렇군! world
```
