---
layout: post
section-type: post
title: "[two scoop of django] 7장 쿼리와 데이터베이스 레이어"
categories: Python
tags: [ 'Django', 'two_scoop_of_django', 'python' ]
comments: true
---

7장 쿼리와 데이터베이스 레이어

1.들어가기
# 에러처리
# 쿼리의 가독성을 높이는 법
# 쿼리 도구 잘 이용하기[UPPER, F,등 다양한  query expression]
  주의사항 - 로우 sql은 지향[ORM 장점을 이용하려고 쓰는데 이거 안쓰면..? ]
# 인덱스
# 트랜잭션

2.내용

#에러처리

7.1 단일 객체에서 get()대신 get_object_or_404() 이용하기
     -  헬퍼 함수, 폼, 모델 메서드, 뷰를 제외한 다른 곳 그리고 뷰와 직접적으로 관련된 곳이 아닌 곳에서는 이용하지 말자.

7.2 예외를 일으킬 수 있는 쿼리를 주의하자
    - get_object_or_404()를 이용할 때를 제외한 경우에는 try-except를 이용한 예외 처리를 해야 한다.


   팁1 ObjectDoesNotExist와 DoesNotExist
ObjectDoesNotExist : 모든 모델 객체에서 이용 가능 (import 필요)
DoesNotExist : 특정 모델에서만 이용 가능

``` python
from django.core.exceptions import ObjectDoesNotExist

from flavors.models import flavor
from store.exceptions import OutOfStock

def list_flavor_line_item(sku):
  try:
    return Flavor.objects.get(sku=sku, quantity__gt=0)
  except Flavor.DoesNotExist:
    msg = "{} 재고가 없습니다. ".format(sku)
    raise OutOfStock(msg)

def list_any_line_item(model, sku):
  try:
    return model.objects.get(sku=sku, quantity__gt=0)
  except ObjectDoesNotExist:
    msg = "{} 재고가 없습니다.".format(sku)
    raise OutOfStock(msg)
```
팁2 여러 개의 객체가 반환되었을 때
    - 쿼리가 하나 이상의 객체를 반환할 수도 있다면 MultipleObjectsReturned 예외
``` python
from flavors.models import Flavor
from store.exceptions import OutOfStock, CorruptedDatabase
def list_flavor_line_item(sku):
    try:   
        return Flavor.objects.get(sku=sku, quantity__gt=0)
    except Flavor.DoesNotExist:
        msg = "We are out of {}".format(sku)
        raise OutOfStock(msg)
    except Flavor.MultipleObjectsReturned:
        msg = "Multiple items have SKU {}. Please fix!".format(sku)
        raise CorruptedDatabase(msg)
```
# 쿼리의 가독성을 높이는 법


7.3 쿼리를 좀더명확하게하기위해 지연연산이용하기

코드를 명확하게 복잡한 쿼리의 경우 몇 줄 안 되는 코드에 너무 많은 기능을 엮어서 기술하는 것은 피해야한다.
``` python
#나쁜예
from django.models import Q
from promos.models import Promo

def fun_function(**kwargs):
  """유효한 아이스크림 프로모션 찾기"""
  # 너무 길게 작성된 쿼리 체인이 화면이나 페이지를 넘겨 버리게 되므로 좋지 않다.
  return Promo.objects.active().filter(Q(name__startswith=name)|Q(description__icontains=name))
```
지연연산 (Lazy Evaluation) 을 활용하여 장고 코드를 좀 더 깔끔하게 만들 수 있다.
지연연산?
데이터가 정말로 필요하기 전 까지는 장고가 SQL을 호출하지 않는 특징
따라서 ORM 메소드와 함수를 얼마든지 연결해서 코드를 쓸 수 있다.
한 줄에 길게 쓰는 대신에 여러줄에 나눠서 쓰면 가독성을 엄청나게 향상시키며, 유지보수를 쉽게 해준다.
``` python
#리팩토링 버전[지연 연산 한 버전]
from django.models import Q

from promos.models import Promo

def fun_function(**kwargs):
  """유효한 아이스크림 프로모션 찾기"""
  results = Promo.objects.active()
  results = results.filter(
              Q(name__startswith=name)|
              Q(description__icontains=name)
              )             
  results = results.exclude(status='melted')
  results = results.select_related('flavors')
  return results
```

Promo 모델 중에서 active 메소드로 리턴된 모든 레코드
그 중에서 name 값이 name으로 시작하거나, description 값 중에 name이 포함되어 있는 모든 레코드
그 중에서 status가 ‘melted’인 레코드는 제외
Foreign Key 항목인 flavors도 함께 가져와서 리턴
# 쿼리 도구 잘 이용하기

7.4 고급 쿼리 도구 이용하기
장고의 ORM은 강력하지만 부족한 곳은 고급 쿼리 도구를 이용하여 데이터베이스를 통한 데이터 가공 하면 파이선 통해서 하는 것 보다 성능 좋고 안전하다.
7.4.1 쿼리 표현식
쿼리 표현식을 꼭 익혀두자. 프로젝트의 안전성과 성능을 대폭 향상시켜 줄 것이다.
Query Expressions (공식문서)
나쁜예제
모든 고객 레코드에 대해서 for loop가 돌고있다. => 매우 느리고, 메모리 소모가 크다
경합상황 (race condition)에 직면할 가능성이 크다. => 데이터 분실 우려
경합상황 : 다중 프로그래밍 시스템이나 다중 처리기 시스템에서 두 명령어가 동시에 같은 기억 장소를 액세스할 때 그들 사이의 경쟁에 의해 수행 결과를 예측할 수 없게 되는 것.
``` python

# 나쁜 예제
from models.customers import Customer

customers = []
for customer in Customer.objects.iterator():
  if customer.scoops_ordered> customer.store_visits:
    customers.append(customer)
수정 후
쿼리표현식을 통해서 코드들이 서로 경합을 펼치는 상황을 피할 수 있다.
#나쁜 예제 리팩버전
from django.db.models import F
from models.customers import Customer

customers = Customer.objects.filter(scoops_ordered__gt=F('store_visits'))
```

위 코드 쿼리표현식 중 F() expressions의 기능
파이썬이 아닌 데이터베이스 자체 내애서 해당 조건을 비교하는 기능을 가진다.
경합조건을 피할 수 있다.Avoiding race conditions using F
위 코드에서 내부적으로 다음과 같은 SQL문을 생성한다.
SELECT * from customers_customer where scoops_ordered > store_visits

특히나 포퍼먼스 면에서 큰 이득인데

selected_chocie_votes +=1의 경우
db 값 참조 -> memory 로딩 -> 연산 -> 결과 값 db 저장

select_choice.votes = F(“votes”)+1의 경우
db 자체 연산 -> 결과값 저장

굿


7.4.2 데이터베이스 함수들
UPPER(), LOWER(), COALESCE(), CONCAT(), LENGTH(), SUBSTR()
    Coalesce를 사용하여 aggregate가 None을 반환하는 것을 방지하기
    https://wayhome25.github.io/django/2017/09/02/django-queryset-aggregate-coalesce/
저자가 가장 좋아하는 기능이다. 왜냐하면
쉽고 간결하다.
성능이 굉장히 향상된다. (파이썬으로 데이터 처리속도 < 데이터베이스 내에서 데이터 처리속도)
7.5 필수 불가결한 상황이 아니라면 로우 SQL은 지양하자
그럼 언제 로우 SQL을 사용하나요? => SQL을 직접 이용함으로써 코드가 월등히 간결해지고, 단축되는 경우에만 사용하자.
# 인덱스
7.6 필요에 따라 인덱스를 이용하자
모델의 필드 옵션으로 db_index를 추가하면 해당 필드에 대해서 Database index가 생성된다.
처음에는 인덱스 없이 시작하고 필요에 따라서 하나하나 추가하는 것을 추천한다.
인덱스가 빈번하게 이용될 때 (쿼리의 10~25% 사이) => 생성된 SQL 문에서 WHERE 절과 ORDER_BY 절을 세심하게 살펴보기
인덱싱을 통해서 성능이 향상되는지 테스트 가능할 때
PostgreSQL의 경우 pg_stat_activity 를 통해서 어떤 인덱스가 사용 중인지 확인 가능하다.
날짜도 인덱스 걸 수 있네...
# 트랜잭션
7.7 트랜잭션 (Transactions)


Transaction : (명사) 처리, 처리과정
컴퓨터 과학분야에 트랜잭션은 “쪼개질 수 없는 업무처리의 단위”를 의미
데이터베이스 충돌을 해결하기 위해서 둘 또는 그 이상의 데이터베이스 업데이트를 단일화된 작업 으로 처리하는 기법
하나의 수정작업(update)가 실패하면 트랜젝션 상의 모든 업데이트가 실패 이전 상태로 복구된다.
그러기 위한 트랜젝션의 필수요건! ACID

7.7.1 각각의 HTTP 요청을 트랜잭션으로 처리하라
아래와 같은 설정을 통해서 읽기 데이터를 포함한 모든 요청이 트랜잭션으로 처리되게 할 수 있다.
장점 : 뷰에서의 모든 데이터베이스 쿼리가 보호되는 안정성을 얻을 수 있다.
단점 : 성능 저하를 가져올 수 있다.
쓰기 작업이 많은 프로젝트의 초기 구성에서 데이터베이스 무결성을 유지하는데 효과적인 구성
특정 루틴을 설정에서 제외시키고 싶다면 뷰 함수에서 transaction.non_atomic_requests()로 데코레이팅한다.
의료정보나 금융 정보에 사용한다.

``` python

# settings/base.py

DATABASE = {
  'default': {
    #...생략
    'ATOMIC_REQUESTS': True,
  }
}
```

ATOMIC_REQUESTS를 이용할 때 주의해야 할 또 다른 점은, 오직 에러가 발생하 고 나서야 데이터베이스 상태가 롤백된다는 것이었다. 사용자에게 해당 작업에 대한 처리 확인 메일을 보내는 경우를 생각해보자.
작업 처리 중 확인 메일을 보낸 후 에러 발생 해 롤백을 하면 화나니...
일단 non_atomic_requests()로 데코레이팅 하고, atomic()을 쓰는 것을 추천하는 것 같다(나의 생각)

``` python

# flavors/views.py
from django.db import transaction
from django.http import HttpResponse
from django.shortcuts import get_object_or_404 from django.utils import timezone
from .models import Flavor

    @transaction.non_atomic_requests
    def posting_flavor_status(request, pk, status):
        flavor = get_object_or_404(Flavor, pk=pk)
        # 여기서 오토커밋 모드가 실행될 것이다(장고 기본 설정).
        flavor.latest_status_change_attempt = timezone.now()
        flavor.save()

        with transaction.atomic():
            # 이 코드는 트랜잭션 안에서 실행된다.
            flavor.status = status
            flavor.latest_status_change_success = timezone.now()
            flavor.save()
            return HttpResponse("Hooray")

        # 트랜잭션이 실패하면 해당 상태 코드를 반환한다.
    return HttpResponse("Sadness", status_code=400)
```



장고는 트랜잭션 메커니즘을 두가지 제공
데코레이터(decorator)를 이용한 트랜잭션 예시
``` python

from django.db import transaction

@transaction.atomic
def transaction_test1(arg1, arg2):
    # start transaction
    a.save()

    b.save()
    # end transaction

```

with 명령어를 이용한 트랜잭션 예시

``` python

from django.db import transaction

def transaction_test2(arg1, arg2):
    a.save()    # 항상 save 처리됨, 예외가 발생할 경우 에러 발생
    with transaction.atomic():
        # start transaction
        b.save()
        c.save()
        # end transaction

```

try / except 블록에서 원자를 래핑하면 무결성 오류를 자연스럽게 처리 할 수 있습니다.

``` python

from django.db import IntegrityError, transaction

@transaction.atomic
def viewfunc(request):
    create_parent()

    try:
        with transaction.atomic():
            generate_relationships()
    except IntegrityError:
        handle_exception()

    add_children()

```

7.7.2 명시적인 트랜잭션 선언
사이트 성능을 개선하는 방법 중 하나
트랜젝션에서 어떤 뷰와 비지니스 로직이 하나로 엮여 있는지 명시해 주는 것 (개발 시간이 오래 걸림)
대부분의 사이트는 ATOMIC_REQUESTS 설정으로 충분하다.
독립적인 ORM 메서드 호출은 이미 내부적으로 트랜잭션을 이용하고 있다.
 여러 ORM 메서드 들을 뷰나 함수 내에서 호출할 때 트랜잭션을 이용하는게 좋다
트랜잭션 가이드라인
· 데이터베이스에 변경이 생기지 않는 데이터베이스 작업은 트랜잭션으로처 리하지 않는다.
· 데이터베이스에 변경이 생기는 데이터베이스 작업은 반드시 트랜잭션으로 처리한다.
· 데이터베이스 읽기 작업을 수반하는 데이터베이스 변경 작업 또는 데이터베이스 성능에 관련된 특별한 경우에는 앞의 두 가이드라인을 모두 고려한다.


7.7.3 django.http.StreamingHttpResponse와 트랜잭션
뷰가 django.http.StreamingHttpResponse를 반환한다면 중간에 트랜잭션 에러를 처리하기는 불가능하다.
이를 해결하려면 아래와 같은 방법이 있다.
‘ATOMIC_REQUESTS’설정을 False 로 설정하고 명시적 트랜잭션 선언을 검토
해당 뷰를 django.db.transaction.non_atomic_requests 데코레이터로 감싸기
7.7.4 MySQL 에서의 트랜잭션
MySQL 데이터베이스 타입에 따라서 트랜잭션 지원 여부가 달라진다. (InnoDB - 지원함, MyISAM - 지원안함)
트랜잭션을 지원하지 않는다면, ATOMIC_REQUESTS 설정에 상관없이 항상 오토커밋 모드로 작동한다.



3.요약
orm을 쓸 때 함수 잘쓰고 에러처리는 잘하고 transaction을 센스 있게 잘쓰자
에러처리를 적당히 해야하는데 그게 참 힘든듯...

 Q. 한번에 두 프로세스 접근 하면 lock을 걸어야 하는데...python은 어떻게 되있지?

[락 얘기]
https://stackoverflow.com/questions/42520917/does-django-atomic-transaction-lock-the-database
