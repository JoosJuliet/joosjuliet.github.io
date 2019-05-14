---
layout: post
section-type: post
title: "(작성중)Legacy 극복 프로젝트"
category: OOP
tags: [ 'legacy', 'skencar' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

---
# 1. 이글을 쓴 이유
회사를 가면 언제나 만나는 것은 *Legacy* 다.
특히 이번 회사는 난이도는 많이 높았다.
난이도가 높은 이유는 3가지였다.

1. 테스트 코드가 없다.(coverage 0%...)
2. 코드에 가독성이 떨어진다.(변수가 막 한글자에 indent무시는 기본이고 정말 엄청난 스파게티다.)
3. 프론트와 백의 분리가 안되있다.(그 덕에 test 짜는게 더 노답이다.)
4. 너무 오래된 기술 stack(파릇한 경력인 나에게는 knockout.js에 java5에 classes로 배포할 정도로 역사깊은 코드는 버겁다.)

"레거시 코드 활용 전략"까지 다 읽으면 좋지만 일단은 일을 해야함 간단히 정리해 보겠다.




# 2. 지금 내가 극복 하려 하는 Legacy
다해히 지금 하는 일은 front와 back이 나눠져 있다.

*문제점*
- 한 abstract을 다른 곳에서 사용할 때 상속을 받아서 나머지 기능들을 만드는데, abstract에 있는 method가 너무 많다.
- class에서의 기능도 이곳저곳에 흩어져 있다.
  - 모듈화가 하나도 되어있지 않다.


테스트 코드가 있으면 개발 흐름은 이렇게 될 것입니다.
<span style="background-color:#000; color : #fff;"><b>테스트 코드를 배치한다 (feat. 소스 분석, 이해) -> 변경한다 -> 테스트 코드로부터 피드백을 받는다 -> 리팩토링 -> 확신에 찬 배포 -> 나의 성과!</b></span>



# 레거시 코드를 감수해야 한다면?
레거시 코드에 신규 기능 개발 요청이 들어왔을 때, 레거시 코드의 의존관계가 많이 존재하고 테스트 코드가 아직 준비되지 않은 상황에서 보통 레거시 코드를 변경하는 순서는 다음과 같을 것입니다.

1. 신규 기능을 반영할 지점을 판별한다.
2. 테스트 코드를 작성할 위치를 찾는다.
3. 의존 관계를 제거한다.
4. 테스트 코드를 작성한다.
5. 변경 및 리팩토링을 수행한다.


기존의 동작에 영향을 미치지 않고 유지해야 한다는 전제조건이 매우 위험 부담을 갖게 되는데요. 왜냐하면 코드를 변경할 때 어떤 동작에 영향을 미칠지 모르는 블랙박스이기 때문입니다. 그렇다고 기존 레거시 코드 안에서 어떻게든 해결하려고 하면 기존의 메소드, 클래스는 매우 비대해져서 나중에는 걷잡을 수 없는 상황이 초래될 수 있습니다.

그나마 덜 위험도를 가질 수 있는 레거시코드를 포장하는 방법에 대하여 적용해보았던 것을 설명



# 레거시 메소드를 포장하자.
실제로 운영하는 코드를 보여드릴 수는 없어서 아래처럼 주문을 생성하는 레거시 코드가 있다고 가정합니다. 기능은 간단하게 주문이 생성되는 메소드 안에 추상화 단계가 같은 여러 메소드가 존재합니다. 새로운 주문에 대한 주문번호를 생성하고 해당 주문에 대한 정보를 조회하여 결제를 진행합니다. 그리고 결제 결과에 따라서 주문에 대한 처리가 완료인지 실패인지를 리턴해주는 메소드입니다.

``` java
// 레거시코드 : 온라인 결제를 진행한 주문을 생성한다.
public void createOrder(){
	String orderNo = createOrderNo();
	Order order = createOrder(orderNo);
	PayResult payResult = pay(order);

	if(isPaid(payResult))
		orderComlete(order);
	else
		orderFail(order);
}

public PayResult pay(Order order){
	// do something..
}
```
기존에는 온라인 결제만 가능한 레거시 코드였으나 오프라인 결제도 가능하도록 해달라는 신규 요구사항이 발생하였습니다.

아래는 온라인/오프라인 결제 기능 추가 요구사항을 반영한 코드입니다.
``` java
// 신규 요구사항 적용 코드 : 온라인 결제만 진행하던 것을 오프라인 결제도 진행할 수 있다.
public void createOrder(){
	String orderNo = createOrderNo();
	Order order = createOrder(orderNo);
	PayInfo payInfo = order.getPayInfo();
	PayResult payResult = pay(payInfo); // 변경 포인트: 신규 pay() 메소드.

	if(isPaid())
		order.complete();
	else
		order.fail();
}

// 추가된 로직 : 결제를 온라인 결제와 오프라인 결제 중 선택 할 수 있다.
public PayResult pay(PayInfo payInfo){
	if(isOnlinePay(payInfo))
		return payOnline(); //원래 pay() 메소드.
	else
		return payOffline();
}

```
위와 같
---
참고 : http://woowabros.github.io/experience/2019/02/27/Working_Effectively_with_Legacy_Code.html  
