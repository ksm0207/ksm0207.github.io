---
title: Django로 게시판 만들기 - 04 ( Django 개발 흐름 )
author: Kim
date: 2021-02-19 17:05 +0900   # 2019-08-20 19:34:00 0900
categories : ["Python", "Django"]
tags: [Django]
comments : true
---

본 포스팅 은 앞으로 의 개발 과정 을 진행하기전에 흐름을 정리 해볼 것 입니다<br>

# Step 1 개발 흐름 정리하기 

<br>

```
        (1) Local Server 에 해당 페이지 요청              Local Server
                
        http://localhost:8000/pybo/   ---------------------------------------------------------
[ My Web ]    --------->              |   [config/urls.py]   (2) 분석   [pybo/views.py]       |
    ▲                                 |   pypo/ -> views.index ----->   def index(request)    |
    |                                 |                                                       |
    |                                 |                                                       |  
    |                                 |       True      config/urls.py = call index           |
    |                                 |       False     config/urls.py = http404              |
    |                                 |                                                       |
    |                                  --------------------------------------------------------
    |                                                              |
    |                  (3) Result = Views.py def index(request)    |
    ----------------------------------------------------------------   
```

* (1) 사용자는 웹 브라우저 주소창에 localhost:8000/pybo/ 페이지 를 Request 합니다
* (2) Local Server 에서는 (config/urls.py) URL을 해석해 pybo/views.py 파일의 index function 을 호출하고
* (3) pybo/views.py 에서 index function 을 실행하고 그 결과를 웹 브라우저 에게 전달 하는 과정입니다.<br>
      
      ※ 존재 할 경우 True 안 할 경우 False , 결과 화면을 전달합니다

앞으로 의 개발 흐름은 이렇습니다<br>
사용자가 /pybo/ 페이지를 요청 했을때 Local Server 에서 URL을 분석후 연결되어있는 function 을 호출하고<br>
호출하고 실행 하였을때 화면을 전달받는 과정입니다 그리고 이것은 계속 반복되면서 실습을 진행 합니다


# Step 2 URL 분리하기

현재 App 에 관련된 파일들은 대부분 app_name 디렉토리에 존재하지만 App에서 매핑을 위한 urls.py 파일은<br> 존재하지 않기 때문에
매핑을 추가하려면 config 디렉토리에 있는 urls.py 파일을 수정해 줄 필요가 있습니다


config/urls.py 파일을 다시 한번 살펴보겠습니다 

```
파일명 : config/urls.py

from django.contrib import admin
from django.urls import path
from pybo import views


urlpatterns = [
    path("pybo/", views.index),
    path("admin/", admin.site.urls),
]
```

현재 프로젝트의 짜임새를 전혀 고려하지 않은 상태이지만 우리가 만든 App 에 관련된 urls.py 파일을 따로 구성할 방법은 다음과 같습니다<br>


```

파일명 : config/urls.py

from django.contrib import admin
from django.urls import path, include ★ include 추가
from pybo import views


urlpatterns = [
    path("pybo/", include('pybo.urls')), views.index --> include 함수로 변경
    path("admin/", admin.site.urls),
]

```

include 함수를 사용하여서 pybo/로 시작되는 페이지 요청은 모두 pybo/urls.py 파일에 있는 URL 매핑을 참고하고 처리하게 만들었습니다<br>
pybo App에 관련된 URL 요청은 앞으로 pybo/urls.py 파일에서 관리하도록 구성하였고 pybo/ 요청은 config/urls.py 이 아닌 pybo/urls.py 에서 처리됩니다

# Step 3 App 폴더에 urls.py 파일 생성하기

config/urls.py 파일에서 pybo/ 페이지 요청은 우리가 만든 앱 폴더에서 처리할수 있어야 하기 때문에<br>
App 디렉토리에서 urls.py 파일을 생성해줍니다

```
파일명 : App/urls.py

from django.urls import path ★ 추가
from . import views ★ 추가

★ 추가
urlpatterns = [
    path('', views.index),
]
```
▲ path 에서 첫번째 매개변수를 빈 문자열을 넘겨주게 되면 config/urls.py 파일에서 pybo/ 페이지 요청에 대한<br> 처리를 한 상태에서 pybo/urls.py 파일이 실행되게 됩니다


# Django 와 urls.py

Django 에서 urls.py를 읽는 방향 예시 입니다

```
config/urls.py

|----------------------------------------|                                        
|urlpatterns = [                         |
|    path("admin/", admin.site.urls),    |
|    path("pybo/", include("pybo.urls")),| 
|]                                       |
|----------------------------------------|

Django : 사용자 요청 주소는 admin/ 에서 끝나진 않고 pybo/ 에서 끝나는군!!
pybo/urls.py 파일에서 찾아봐야겠는걸?

▼
.
.
.

pybo(App)/urls.py

|--------------------------------------|
|urlpatterns = [path("", views.index)] |
|--------------------------------------|

Django : 좋아 여기는 첫번째 매개변수는 빈 문자열이니 첫번째 매핑으로 View를 불러오자 
```

Django 가 urls.py 를 읽는 방향 과정은 매우 중요하므로 Django 문서를 한번쯤 읽어보는것을 추천합니다<br>
<a href="https://docs.djangoproject.com/ko/3.1/intro/tutorial03/">Django Documents</a><br>

다음 포스팅은 데이터를 관리하는 Model을 직접 만드는 실습을 다뤄보겠습니다 감사합니다.


