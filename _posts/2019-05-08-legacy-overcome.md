---
layout: post
section-type: post
title: "(작성중)ALPHA - Legacy 극복 프로젝트"
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




# 레거시를 극복하는 KeyPoint wrapper!
- 레거시 메소드 포장
- 레거시 클래스 포장

레거시 코드는 일단 포장을 해서 무언가를 해야한다.


## 레거시 메소드를 포장
- 간단하게 주문이 생성되는 메소드 안에 추상화 단계가 같은 여러 메소드가 존재합니다.
- 새로운 주문에 대한 주문번호를 생성하고 해당 주문에 대한 정보를 조회하여 결제를 진행합니다.
- 결제 결과에 따라서 주문에 대한 처리가 완료인지 실패인지를 리턴해주는 메소드입니다.


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
1. <b>신규 기능을 반영할 지점을 판별한다.</b>
- 결제방법을 온라인으로 할 것인지 오프라인으로 할 것인지에 대한 선택에 따라 결제가 이루어져야 합니다.
- 이 신규 기능이 들어가야 할 포인트는 pay() 메소드로 보입니다.
- 기존 메소드에 추가된 기능을 포장하여 신규 메소드로 구현하였고 이는 기존 로직에 영향을 주지 않기 때문입니다.

2. <b>테스트 코드를 작성할 위치를 찾는다.</b>
- 현재 작성 가능한 테스트 코드는 기존메소드를 신규메소드로 변경한 pay()가 됩니다.
- 나머지 로직에 대한 테스트 코드는 영향범위를 당장 파악할 수 없기 때문에 현재 기능이 잘 운영되고 있다면, 믿어야 하겠습니다.

3. <b>의존 관계를 제거한다.</b>
- pay()에서는 Order클래스에 대한 의존성이 있었습니다.
- Order클래스의 얻어진 항목들이 모두 pay() 에 필요한 항목이 아님에도 불구하고 Order클래스가 없으면 안 되게끔 구현되어 있다.
- 실질적으로 pay() 에 필요한 항목들에 필요한 파라미터만 별도의 객체로 정리하였습니다.

4. <b>테스트 코드를 작성한다.</b>
- 이제 전달받은 입력 파라미터 항목은 정리되어 어떠한 상황이든 결제에 필요한 값만 들어오게 되었다.
- pay() 의 결과는 결제가 되었는지 안되었는지만 확인하면 되므로, 결제시 발생할 수 있는 모든사항에 대한 테스트 코드를 작성할 수 있게 되었습니다.

5. <b>리팩토링을 수행한다.</b>
- 더 좋은 설계구조가 도출될 수 있도록 작성된 테스트 코드를 바탕으로 안정된 리팩토링을 계속 수행할 수 있을 것으로 기대됩니다.
- 물론 더 멀리 나아가 나머지 레거시 코드들에 대해서 영향범위를 파악해서 테스트코드 작성을 한 뒤에 리팩토링도 진행되어야 하겠죠.


## 레거시 클래스를 포장
- 주문을 관리하는 Order클래스가 있습니다.
- 아래 코드는 신규로 들어온 주문에 대해 접수처리를 하는 로직

``` java
public class Order {

	public Order(String orderNo){
		createNewOrder(orderNo);
	}

	// 생략...

	public void receitOrder(String orderNo){
		OrderStatus orderStatus = findOrderStatus(orderNo);

		if(orderStatus.isWait()){
			acceptOrder(orderStatus);
		} else {
			throw new Exception("접수할 수 없는 주문입니다.");
		}
	}

	public void acceptOrder(OrderStatus orderStatus){
		orderStatus.changeOrderStatus("accept");
	}

	// 생략...
}
```

이 Order클래스에서 주문접수 데이터를 로깅하여 로깅시스템으로 보내야 하는 신규 요구사항이 발생하였습니다.
아래 LoggingOrder클래스는 레거시 클래스인 Order클래스를 인자로 전달받아 덮어쓰면서 기존의 acceptOrder()기능과 동시에 로그데이터를 보내는 신규기능도 추가된 새로운 클래스입니다.

``` java
public class LoggingOrder {
	private Order order;

	public LoggingOrder(Order order) {
		this.Order = order;
	}

	// 생략...

	public void acceptOrder() {
		order.acceptOrder();
		submitLoggingSystem(order); //신규기능 추가: 주문접수 데이터를 로깅시스템으로 보낸다.
	}

	public void submitLoggingSystem(Order order){
		// do something..
	}

	// 생략...
}
```
위 2개의 클래스를 포장하는 법은 다음과 같습니다. 최종적으로는 데코레이터 패턴의 형태가 도출됩니다.
``` java
// 사용
LoggingOrder order = new LoggingOrder(new Order("Test1234"));
order.acceptOrder();
```

1. <b>신규 기능을 반영할 지점을 판별한다.</b>
- 주문접수 데이터의 로깅처리를 위하여 acceptOrder()에 로깅데이터 전달 기능이 추가되면 좋을 것 같다는 생각이 듭니다.
- 그리고 로깅시스템으로 보내는 신규 메소드를 추가하면 요구사항은 만족하게 됩니다.
- 하지만 여기서 고려해야 할 부분이 있습니다.

- 이 Order 클래스는 레거시 코드이며, 이 클래스 내부에 신규 기능을 추가하여 오염시키기 보다는 새로운 클래스로 만들어 레거시 코드의 영향범위를 늘리고 싶지 않았습니다.
- 새로운 클래스로 만든다는 것은 새로운 책임과 기존의 책임을 분리 한다는 의미이다.
- 이후 코드의 변경이 일어나는 시점은 새로운 클래스부터 적용되고 레거시 코드는 독립적으로 남아있게 되어 이후 벌어질 수 있는 리스크는 최소화가 될 수 있습니다.

2. <b>테스트 코드를 작성할 위치를 찾는다.</b>
- 새로운 클래스가 도출되고 기존 레거시 클래스를 덮어쓰게 되면 테스트 코드는 명료해집니다.
- 기존 레거시 클래스의 기능은 이상없이 잘 운영되고 있다는 전제하에 submitLoggingSystem()에 대한 테스트코드를 우선 제일 먼저 만들 수 있습니다.

3. <b>의존 관계를 제거한다.</b>
- 현재 LoggingOrder클래스에서는 의존 관계라고 보이는 것은 레거시인 Order클래스 입니다.
- 하지만 레거시 임으로 지금 당장 제거하기 보다는 현상 유지하고, 이후를 기약하며 잠시 욕심을 내려놓습니다.

4. <b>테스트 코드를 작성한다.</b>
- 현재는 submitLoggingSystem()에 대한 테스트 코드만 작성할 수 있습니다.

5. <b>변경 및 리팩토링을 수행한다.</b>
- Order클래스의 레거시 코드를 그냥 레거시 코드로 둘수는 없습니다.
- Order클래스 또한 테스트 코드를 추가하며 리팩토링 해야합니다.
- 그렇지만 현 상황에서는 레거시코드를 건드리지 않는 선에서 신규 기능에 대한 개발은 급한 불은 끈 셈입니다.


# 이렇게 하면 얻는 것은 무엇인가?
- 신규 기능이 추가되더라도, 기존 코드로직에 영향을 주지 않게 됩니다.
- 신규 코드가 레거시코드와 섞이지 않기 때문에 잘 운영되고 있는 레거시 코드를 변경할 일이 적어집니다.
- 최소 신규코드에 한해서는 테스트 코드를 작성할 수 있고 신규코드가 레거시 코드가 되더라도 안정감을 느낄수 있습니다.

---
참고 : http://woowabros.github.io/experience/2019/02/27/Working_Effectively_with_Legacy_Code.html  
