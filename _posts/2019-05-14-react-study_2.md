---
layout: post
section-type: post
title: "[React] react 점심스터디 2일차 (promise, async await)"
category: React
tags: [ 'React', 'SKEncarLunchStudy' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


# promise
promise는 then으로 앞에 결과값을 가져온다.
장점은 채인으로 되있어서 좀 더 보기 좋다.

promise객체는 바로 쓸수 없다.
promise에서 then 으로 실행이 된다.

``` js
promise_object.then((res)=>{
  console.log(res);
})
```
이렇게 실행된다.
실패시 catch로 받으면 된다.
``` js
promise_object.then(()=>{

  }). catch
  ```
# async await
비동기 요청할 함수에 async로 표시를 한다.
요청 결과는 await로 기다린다.
``` js
fetchData = async () =>{
  const result = await axios.post({
    // ...
  });
}
```
async await쓰면 async가 선언된 함수에서 await 뒤에 있는 것들이 실행이 안된다.

``` js
fetchData = async () =>{
  try {
    const result = await axios.post({
      // ...
    });
  } catch (e) {

  }
}
```


비동기 통신에서는 componentDidMount,componentUpdateMount에서 많이한다.


*xhr보면 이건 비동기 통신 결과나온다.*
