---
layout: post
section-type: post
title: "[two scoop of django] 9장 함수기반뷰의모범적인이용"
categories: Python
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
