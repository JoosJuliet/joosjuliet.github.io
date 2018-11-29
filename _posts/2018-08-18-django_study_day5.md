---
layout: post
section-type: post
title: "[two scoop of django] 9장 함수기반뷰의모범적인이용 && 10장 클래스 기반 뷰의 모범적인 이용"
categories: Django
tags: [ 'Django', 'two_scoop_of_django', 'python' ]
comments: true
---

# 9장 함수기반뷰의모범적인이용

## 1.들어가며
처음에는 함수뷰로 먼저 장고를 배우고 요즘에는 class뷰로 옮기고 있긴 하지만,
확실히 함수뷰를 전혀 안쓰는 것 보다는 적당히 섞어 쓰는 것이 확실히 좋다.


## 2. 내용
### 9.1 함수 기반 뷰의 장점

· 뷰 코드는 작을수록 좋다.
 뷰에서 절대 코드를 반복해서 사용하지 말자.
· 뷰는 프레젠테이션(presentation) 로직을 처리해야 한다. 비즈니스 로직은 가능한 한 모델 로직에 적용시키고 만약 해야 한다면 폼 안에 내재시켜야 한다.
·뷰를 가능한 한 단순하게 유지하자.
· 403, 404, 500을 처리하는 커스텀 코드를 쓰는 데 이용하라. · 복잡하게 중첩된 if 블록 구문을 피하자.

### 9.2 HttpRequest 객체 전달하기
뷰에서 코드 재사용하기를 원하는 경우가 생긴다.
하지만 미들웨어나 콘텍스트 프로세서 같은 글로벌 액션에 연동되 있지 않아 재사용에 문제
=> 해결책
프로젝트 전체를 아우르는 유틸리티 함수를 만드는 것을 추천


#### Tip1) HttpRequest 를 이용해라
매개변수화 시켜서 사용하는 것이 더 좋다
객체에 여러 추가적인 속성을 덧붙일 수 있다.

``` python
# sprinkles/views.py
from django.views.generic import DetailView
from .utils import check_sprinkles
 from .models import Sprinkle

class SprinkleDetail(DetailView):
     """표준 상세 뷰"""
    model = Sprinkle
    def dispatch(self, request, *args, **kwargs):
         request = check_sprinkles(request)
        return super(SprinkleDetail, self).dispatch(
                                            request, *args, **kwargs)
```
이렇게 클래스 안에 함수를 넣는법

### 9.3 편리한 데코레이터
그런데 이 건 데코레이터로 할 수도 있다.

``` python
# sprinkles/decorators.py
from functools import wraps
from . import utils

# 예제 8.5의 데코레이터 템플릿에 기반을 두고
def check_sprinkles(view_func):
    """사용자가 스프링클(별사탕)을 추가할 수 있는지 확인한다."""
    @wraps(view_func)
    def new_view_func(request, *args, **kwargs):
    # request 객체를 utils.can_sprinkle()에 넣는다.
        request = utils.can_sprinkle(request)
        # 뷰 함수를 호출
        response = view_func(request, *args, **kwargs)
        # HttpResponse 객체를 반환
        return response return new_view_func
```

이를 함수에 추가한다.

``` python
# views.py
from django.shortcuts import get_object_or_404, render
from .decorators import check_sprinkles
from .models import Sprinkle
# 뷰에 데코레이터를 추가
@check_sprinkles
def sprinkle_detail(request, pk):
    """표준 상세 페이지"""
    sprinkle = get_object_or_404(Sprinkle, pk=pk)
    return render(request, "sprinkles/sprinkle_detail.html", {"sprinkle": sprinkle})
```

### 9.3.1 데코레이터 남용하지 않기

적당히... 뭐든 적당히가 좋다 어쩌다 보면...
함수에 엄청나게 많은 데코레이터를 만들 때가 있다.
그럴 때는 함수뷰가 아닌 클래스 뷰를 사용하는 것이 더 좋은 것 같다.

### 9.4 HttpResponse 객체 넘겨주기

HttpRequest 객체에서 그랬듯이, HttpResponse 객체 또한 함수와 함수 사이에서 서로 전달받을 수 있다. Middleware.process_request() 메서드를 떠올리면 될 것이다


## 3.요약
http request받아서 넘겨주기가 핵심




# 10장 클래스 기반 뷰의 모범적인 이용

## 1.들어가며
요즘 대세는 클래스 뷰라고  볼 수 있다.
장고 자체가 워낙 객체지향적으로 짜게 만들어놔서 그런지 더욱이 클래스 기반 뷰가 모든 면에서 좋다.
그리고 장고는 정말 클래스뷰도 잘 만들어 놨다..
특히 Generic view나 listview보면 장고는 정말 내가 코딩을 해야하는 것이 별로 없단 것을 느끼게 된다.

## 2. 내용


### 10.1 클래스 기반 뷰를 이용할 때의 가이드라인
· 뷰 코드의 양은 적으면 적을수록 좋다.
· 뷰 안에서 같은 코드를 반복적으로 이용하지 말자.
· 뷰는 프레젠테이션 로직에서 관리하도록 하자. 비즈니스 로직은 모델에서 처리하자. 매우 특별한 경우에는 폼에서 처리하자.
 뷰는 간단 명료해야 한다.
· 403, 404, 500 에러 핸들링에 클래스 기반 뷰는 이용하지 않는다. 대신 함수기반 뷰를 이용하자.
403 permission denied
404 file not found
500 internal error
· 믹스인은 간단 명료해야 한다.

### 10.2 클래스 기반 뷰와 믹스인 이용하기
사전지식: 파이선은 다중상속이 된다 && 그럼으로 믹스인을 만들 수 있다.
Mixin 은 클래스에 추가적인 속성이나 메소드를 제공하는 것

파이썬은 Mixin 을 위한 특별한 키워드는 없으며, 단지 다중상속을 통해서 만들기 때문에 이 과정에서 문제가 생길 소지가 생긴다.
``` python
class Mixin1(object):
    def test(self):
        print "Mixin1"

class Mixin2(object):
    def test(self):
        print "Mixin2"
class MyClass(BaseClass, Mixin1, Mixin2):
    pass
```

이건 나쁜 예) 바로 밑 코드 처럼 해야한다.
```shell
>>> obj = MyClass()
>>> obj.test()
Mixin1
```


오른쪽 부터 왼쪽으로 계승이 되는데, 즉 Mixin2 클래스가 가장 상위클래스가 되고 그 후에 Mixin1 , BaseClass 가 차례대로 하위 클래스가 되는데 일반적인 경우 덮어 써질 염려가 없지만 , 위 처럼 메소드 명이 같을 경우 가장 하위의 클래스가 적용되어 덮어 써진다.


 믹스인이란 실체화된 클래스가 아니라 상속해 줄 기능들을 제공하는 클래스
프로그래밍 언어에서 다중 상속을 해야 할 때 믹스인을 쓰면 클래스에 더 나은 기능과 역할을 제공

``` python
from django.views.generic import TemplateView

class FreshFruitMixin(object):
    def get_context_data(self, **kwargs):
        context = super(FreshFruitMixin,
            self).get_context_data(**kwargs)
        context["has_fresh_fruit"] = True
        return context
class FruityFlavorView(FreshFruitMixin, TemplateView):
    template_name = “fruity_flavor.html"
 ```
이런식으로 해야한다.
이런식으로 가져다 쓴다
> 실체화 = 인스턴스화(instantiation)  
> 클래스의 객체에 대해 메모리를 할당하여 인스턴스를 만드는 것

#### 상속에 관한 규칙
케네스 러브(Kenneth Love)가 제안한 상속에 관한 규칙을 이용하자.  
이는 파이썬의 메서드 처리 순서(MRO)에 기반을 둔 것으로, 왼쪽에서 오른쪽의 순서로 처리한다고 표현할 수 있다.

- **규칙1.** 장고가 제안하는 기본 뷰는 '항상' 오른쪽으로 진행한다.  
- **규칙2.** 믹스인은 기본 뷰에서부터 왼쪽으로 진행한다.  
- **규칙3.** 믹스인은 파이썬의 기본 객체 타입을 상속해야만 한다.

### 10.3 어떤 장고 제네릭 클래스 기반 뷰를 어떤 태스크에 이용할 것인가?


장고 클래스 기반 뷰/제네릭 클래스 기반 뷰의 이용에 대한 세 가지 의견

#### 1.‘제네릭 뷰의 모든 종류를 최대한 이용’하자는 그룹[최대 지지]
장고를사용하는이유는개발작업의양을최소화하는데그최대의목적이있다는철학에기 반을둔그룹의주장이다.작업양을최소화하기위해제네릭뷰가제공하는모든종류의뷰를 최대한 이용하기를 장려한다. 우리 또한 이를 지지하는 바이다. 우리의 경험으로 보건데 이러 한 방법으로 다수의 프로젝트를 빠르고 쉽게 개발, 유지 보수하는 데 큰 성공을 거두었다.
#### 2.‘심플하게 django.views.generic.View 하나로 모든 뷰를 다 처리’하자는 그룹
장고의 기본 클래스 기반 뷰로만으로도 충분히 원하는 기능을 다 소화할 수 있으며 진정한 클래스 기반 뷰란 모든 뷰가 제네릭 클래스 기반 뷰여야 한다는 주장이다. 지난 몇 년 동안 ‘제네릭 뷰의 모든 종류를 최대한 이용’하자는 리소스 기반 접근 방식이 실패한, 난해한 테스크들에 대해서 이 방법이 매우 효율적이라는 점을 발견했다. 이번 장에서 이러한 몇 가지 경우에 대해 이야기할 것이다.
#### 3.‘뷰를 정말 상속할 것이 아닌 이상 그냥 무시’하자는 그룹
제이콥 캐플런모스(Jacob Kaplan-Moss)는 다음과 같이 말했다. “내 일반적인 조언은 읽 기 쉽고 이해하기도 쉬운 함수 기반 뷰로 시작하라는 것이다. 그리고 클래스 기반 뷰가 반드 시 필요한 상황이 되었을 때만 클래스 기반 뷰를 이용하는 것이다. 어떤 상황에서 클래스 기 반뷰를반드시이용해야할까?여러뷰에서재사용할수있는코드양이꽤많은경우다.”

### 10.4 장고 클래스 기반 뷰에 대한 일반적인 팁

#### 10.4.1 인증된 사용자에게만 장고 클래스 기반 뷰/제네릭 클래스 기반 뷰 접 근 가능하게 하기

django.contrib.auth.decorators.login_required 데 코레이터와 클래스 기반 뷰를 이용하는 데 도움이 되긴 하지만, 예제들이 정형화 된 틀에 너무 박혀 있는 문제점이다.
``` python
# flavors/views.py
from django.views.generic import DetailView
from braces.views import LoginRequiredMixin
 from .models import Flavor
class FlavorDetailView(LoginRequiredMixin, DetailView):
      model = Flavor

```
제네릭 클래스 기반 뷰 믹스인 순서를 명심하자
다음을 꼭 기억하자
・ LoginRequiredMixin은 가장 왼쪽에 위치한다.
・ 베이스 뷰 클래스는 항상 가장 오른쪽에 위치한다.
순서를 잊고 잘못된 순서로 나열하면 예상치 못한 결과를 초래하게 된다

#### 10.4.2 뷰에서 유효한 폼을 이용하여 커스텀 액션 구현하기
``` python
from django.views.generic import CreateView
from braces.views import LoginRequiredMixin
from .models import Flavor
class FlavorCreateView(LoginRequiredMixin, CreateView):
    model = Flavor
    fields = ('title', 'slug', 'scoops_remaining')
    def form_valid(self, form):
    # 커스텀 로직이 이곳에 위치
        return super(FlavorCreateView, self).form_valid(form)
```
이미 체크된 폼에 대해 커스텀 로직을 적용하고 싶을 경우, form_valid()에 로직 을 추가하면 된다. form_valid()의 반환형은 django.http.HttpResponseRedirect 가 된다.
#### 10.4.3 뷰에서 부적합한 폼을 이용하여 커스텀 액션 구현하기

``` python
from django.views.generic import CreateView
from braces.views import LoginRequiredMixin
from .models import Flavor
class FlavorCreateView(LoginRequiredMixin, CreateView):
    model = Flavor
    def form_invalid(self, form):
    # 커스텀 로직이 이곳에 위치
        return super(FlavorCreateView, self).form_invalid(form)
```
 django.http.HttpResponse를 반환
form_valid()에서 로직을 추가했던 것과 같은 방법으로 form_invalid()에서도 로직을 추가할 수 있다.
