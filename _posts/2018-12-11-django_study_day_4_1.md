---
layout: post
section-type: post
title: "[two scoop of django] 8장 함수 기반 뷰와 클래스 기반 뷰"
categories: Python
tags: [ 'Django', 'two_scoop_of_django', 'python' ]
comments: true
---


8장 함수 기반 뷰와 클래스 기반 뷰

# 1.요약
함수기반 뷰와 클래스 기반 뷰
url.py와  view.py 어떻게 쓰면 좋나에 대한 내용
# 2.내용

## 함수기반 뷰와 클래스 기반 뷰
장고에서 이용되는 뷰의 기본 형태는 기억해 두자.

함수 기반 뷰의 기본 형태
``` python
# simplest_views.py
from django.http import HttpResponse
from django.views.generic import View

def simplest_view(request):
    # 비즈니스 로직이 여기에 위치한다.
    return HttpResponse("FBV")
```

클래스 기반 뷰의 기본 형태
``` python
class SimplestView(View):
    def get(self, request, *args, **kwargs):
        # 비즈니스 로직이 여기에 위치한다.
    return HttpResponse("CBV")
```
기본 형태가 왜 중요한가?
*종종 우리에겐 한 기능만 따로 떼어 놓은 관점이 필요할 때가 있다.*
*가장 단순한 형태로 된 기본 장고의 뷰를 이해했다는 것은 장고 뷰의 역할을 명확히 이해했다는 것이다.*
*장고의 함수 기반 뷰는 HTTP 메서드에 중립적이지만, 클래스 기반 뷰의 경우 HTTP 메서드의 선언이 필요하다는 것을 설명해 준다.*




글 목록 전체 표시 (List)로 함수 기반 뷰와 클래스 기반 뷰를 비교해 보겠습니다.


## 1-1. FBV 를 활용하여 글 목록 전체 표시
``` python
# * urls.py
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
# * views.py
from django.shortcuts import render
from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5] # 최근 5개의 질문 리스트만 가져온다.
    context = {'latest_question_list' : latest_question_list}
    return render(request, 'polls/index.html', context)
```
##  1-2. CBV - ListView 를 활용하여 글 목록 전체 표시

* 게시판의 글 목록 전체를 표시하거나, 특정 DB table의 record 전체 (혹은 일부)를 List로 표시할 때 활용할 수 있다.
* 리스트가 테이블의 모든 레코드인 경우 모델 클래스만 지정하면 된다.

``` python

# * urls.py
from bookmark.views import BookmarkLV

urlpatterns = [
        url(r'^bookmark/$', BookmarkLV.as_view(), name='index' ),
]
# * views.py
from django.views.generic import ListView
from bookmark.models import Bookmark

class BookmarkLV(ListView):
        """
        ListView 디폴트 지정 속성
        1) 컨텍스트 변수 : object_list
        2) 템플릿 파일 : bookmark_list.html (모델명소문자_list.html)
        """
        model = Bookmark
```
기적....

``` python
# * urls.py
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^$', views.IndexView.as_view(), name='index'), # as_view() 클래스 함수를 통해 함수뷰 생성
]
# * views.py
from django.views.generic import ListView
from .models import Question

class IndexView(ListView):
    template_name = 'polls_cbv/index.html' # 디폴트 템플릿명: <app_label>/<model_name>_list.html
    context_object_name = 'question_list' # 디폴트 컨텍스트 변수명 :  object_list
    def get_queryset(self): # 컨텍스트 오버라이딩
      return Question.objects.order_by('-pub_date')[5:]
# * 디폴트 설정을 그대로 사용한다면 아래와 같이 간단하게 작성할 수 있다.
from django.views.generic import ListView
from .models import Question

class IndexView(ListView):
    def get_queryset(self): # 컨텍스트 오버라이딩
      return Question.objects.order_by('-pub_date')[5:]
```



## 8.1 함수기반 뷰와 클래스기반 뷰를 각각 언제 이용할 것 인가?

일단 우리 stamp는 함수기반 뷰인 것 같아요.
지금은 함수기반 뷰에서 vue로 옮기고 있지만


근데 그냥 뭐든 적당히 섞어 쓰는게 젤 좋은 것 같다...
url.py와 view.py 어떻게 쓰면 좋나에 대한 내용
## 8.2 URLCONF로부터 뷰 로직을 분리하기

장고로 오는 요청들은 urls.py라는 모듈 내에서 URLConf를 통해 뷰로 라우팅된다. 장고는 아주 단순하고 명료하게 URL 라우트를 구성하는 방법을 제공한다.
1. 뷰 모듈은 뷰 로직을 포함해야 한다.
2. URL 모듈은 URL 로직을 포함해야 한다.

나쁜 예
``` python

from django.conf.urls import url
from django.views.generic import DetailView

from tastings.models import Tasting

urlpatterns = [
    url(r'^(?P<pk>\d+)/$',
        DetailView.as_view(
            model=Tasting,
            template_name="tastings/detail.html"),
        name="detail"),
    url(r'(?P<pk>\d+)/results/$',
        DetailView.as_view(
            model=Tasting,
            template_name="tastings/results.html"),
        name="results"),
]
```


## 8.3 URLCONF에서 느슨한 결합 유지하기
``` python
# tastings/views.py
from django.views.generic import ListView, DetailView, UpdateView
from django.core.urlresolvers import reverse

from .models import tasting

class TasteListView(ListView):
    model = Tasting

class TasteDetailView(DetailView):
    model = Tasting

class TasteResultView(TasteDetailView):
    template_name = "tastings/results.html"

class TasteUpdateView(UpdateView):
    model = Tasting

    def get_success_url(self):
        return reverse("tastings:detail", kwargs={"pk": self.object.pk})
# tastings/url.py
from django.conf.urls import url

from . import views

urlpatterns = [
    url(
        regex=r'^$',
        view=views.TasteListView.as_view(),
        name='list'
    ),
    url(
        regex=r'^(?P<pk>\d+)/$',
        view=views.TasteDetailView.as_view(),
        name='detail'
    ),
    url(
        regex=r'^(?P<pk>\d+)/results/$',
        view=views.TasteResultView.as_view(),
        name='results'
    ),
    url(
        regex=r'^(?P<pk>\d+)/update/$',
        view=views.TasteUpdateView.as_view(),
        name='update'
    )
]
```

이리 바꿔야 한다. 그 이유는
뷰들 사이에서 인자나 속성이 중복 사용하면 x [DRY원칙]
* URLConf는 URL 라우팅이라는 명확한 작업만 처리만 하고 로직은 뷰로 다 보내는기
* 클래스 기반임으로 뷰 상속 가능. :
    * 인증 절차 추가, 권한 설정 추가 등 비즈니스 로직 수월
* 표준화된 정의를 구현해 커스텀 로직 얼마든지 구현 가능 :
8.4 URL 이름공간 이용하기

URL 이름공간은 앱 레벨 또는 인스턴스 레벨에서의 구분자를 제공한다.
 tastings_detail 대신 tasting:detail로 하면 굿
실제 Django 의 project 는 app 이 몇개라도 올 수 있습니다.
Django 는 이 app 들의 URL 을 URLconf 에 이름공간(namespace)을 추가해 구별한다.
 polls/urls.py 파일에 app_name 을 추가하여 어플리케이션의 이름공간을 설정할 수 있습니다.

``` python
# polls/urls.py
from django.urls import path

from . import views

app_name = 'polls'
# urlpatterns = [
# #    path('', views.index, name='index'),
#     path('<int:question_id>/', views.detail, name='detail'),
#     path('<int:question_id>/results/', views.results, name='results'),
#     path('<int:question_id>/vote/', views.vote, name='vote'),
# ]
```
이제, polls/index.html template 의 기존 내용을
``` python
# polls/templates/polls/index.html
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```
아래와 같이 이름공간으로 나눠진 detail 의 view 를 가르키도록 변경하세요.

polls/templates/polls/index.html
``` python
<li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>
```


## 8.4.3 검색, 업그레이드, 리팩터링을 쉽게 하기

 tastings:detail 과 같은 이름은 검색 결과를 좀 더 명확하게 해준다.
이는 새로운 서드 파티 라이브러리와 상호 연동 시에 프로젝트를 좀 더 쉽게 업그레이드 및 리팩터링하게 만들어 준다.
안해봤지만...

## 8.4.4 더 많은 앱과 템플릿 리버스 트릭을 허용하기

꼼수(trick)은 일반적으로 확실한 이득을 주기보다는 프로젝트의 복잡성만 높이는 결과를 가져다 주지만, 몇몇 꼼수는 간단히 짚고 넘어갈 정도의 가치는 있다.
* django-debug-toolbar 같은 디버그 레벨에서 내부적인 검사를 실행하는 개발 도구
* 최종 사용자에게 ‘모듈’을 추가하게 하여 사용자 계정의 기능을 변경하는 프로젝트
개발자들은 언제든지 이러한 경우에 URL 이름공간을 이용한 창의적인 꼼수를 구현할 수 있지만, 가장 단순 명료한 해결 방안을 먼저 강구하고 시도하는게 옳바르다.


## 8.5 URLCONF에서 뷰를 문자열로 지목하지 말자

urls.py에서 뷰를 지목(reference)하자. 아래는 urls.py를 올바르게 정의하는 방법이다.
``` python

# polls/urls.py
from django.conf.urls import url

from . import views

# urlpatterns = [
#     # 뷰를 명시적으로 정의
#     url(r'^$', views.index, name='index'),
# ]
```



## 8.6 뷰에서 비즈니스 로직 분리하기
해당 코드를 뷰 밖으로 이동시킨다.


## 8.7 장고의 뷰와 함수

기본적으로 장고의 뷰는 HTTP를 요청하는 객체를 받아서 HTTP를 응답하는 객체로 변경하는 함수다. 수학의 함수와 비슷한 개념이다.
## 함수로서의 장고 함수 기반 뷰
HttpResponse = view(HttpResponse)

## 기본 수학식의 형태로 풀이해 봄(수학에서 이용한 함수식)
y = f(x)

## ... 그리고 이를 CBV 예로 변형해 보면 다음과 같다.
HttpResponse = View.as_view()(HttpResponse)

이런 일련의 과정을 거치는 변환 개념은 함수 또는 클래스 기반 뷰 모두를 통틀어 똑같이 일어난다.
클래스 기반 뷰의 경우 실제로 함수로 호출된다.

장고의 클래스 기반 뷰의 경우 함수 기반 뷰와 비교하면 사뭇 다른 모습을 보여준다.
하지만 사실 URLConf에서 View.as_view()라는 클래스 메서드는 실제로 호출 가능한 뷰 인스턴스를 반환하다.
 다시 말하면 요청/응답 과정을 처리하는 콜백 함수 자체가 함수 기반 뷰와 동일하게 작동한다는 것이다.


## 8.8 LOCALS()를 뷰 콘텍스트에 이용하지 말자

locals()를 쓰지 말고 dict{}을 써라.
명시적이었던 디자인이 암시적 형태의 안티 패턴 형식
뷰가 어 떤 걸 반환하려고 했는지 알 길이 없어졌기 때문

나쁜 예
``` python
# def ice_cream_store_display(request, store_id):
#     store = get_object_or_404(Store, id=store_id)
#     date = timezone.now()
#     return render(request, 'melted_ice_cream_report.html', locals())
# #리팩토링
# def ice_cream_store_display(request, store_id):
#     return render(request, 'melted_ice_cream_report.html', dict{
#         'store': get_object_or_404(Store, id=store_id,
#         'now': timezone.now()
#         })

```

3. 요약

우선 함수 기반 뷰 또는 클래스 기반 뷰를 언제 이용해야하는지, 그에 따른 선호하는 패턴을 다루었다.
그리고 URLConf에서 뷰 로직을 분리하는 기법을 다루었다. 뷰 코드는 앱의 views.py 모듈에, URLConf 코드는 앱의 urls.py 모듈에 소속되어야한다.
