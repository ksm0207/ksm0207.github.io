---
title: Django로 게시판 만들기 - 03 ( Django - URL or View )
author: Kim
date: 2021-02-19 09:36 +0900   # 2019-08-20 19:34:00 0900
categories : ["Python", "Django"]
tags: [Django]
comments : true
---

본 포스팅은 Django 에서 화면간의 URL을 어떻게 처리하고 프로그램을 호출하는지 알아보는것 입니다

지난시간엔 프로젝트를 생성해봤고 이번에는 프로젝트 안에 앱을 생성하여 본격적으로<br>
프로그램을 만들어 보도록 합시다

# 앱 생성하기
<br>
명령 프롬포트에서 django-admin 의 startapp 명령을 이용하여 앱을 생성할 수 있습니다.

``` C:\Users\user\Documents\GitHub\project_name> app_name ```<br>
생성된 앱은 현재 프로젝트 디렉토리 목록을 살펴보면 앱이 추가된것을 확인할 수 있습니다

# 개발 서버 구동하기
<br>
앱 생성까지 완료하였으니 개발 서버 구동을 해볼까요 ? 이제부터 프로그래밍은 시작되는겁니다!

``` C:\Users\user\Documents\GitHub\django_pybo> python runserver ```

그 다음 웹 브라우저에 ```localhost:8000/app_name/ ``` 으로 요청한다고 입력해줍니다<br>
※ 필자의 경우에는 ```localhost:8000/pybo/ 으로 요청하였습니다 ``` 

# URL
<br>
그런데 아주 놀라운 결과를 볼수가 있습니다  ```Page not found (404) ``` 라는 오류 페이지가 나오는걸 보니깐<br>
아직 Django가 일하기가 싫은가 보네요 .. 하지만 우리는 이것을 해결해야 합니다

일단 404 는 HTTP 오류 코드 이며 원인은 요청한 페이지를 찾을 수 없는 경우일때 발생하는데<br>
그렇다면 왜 오류가 발생했을까 ? 라는것을 생각해봐야 합니다

Django는 사용자가 웹 브라우저에서 ```/localhost:8000/pybo/``` 라는 페이지를 요청하면<br>
해당되는 페이지를 가져오는 URL mapping 이 있는지 config/urls.py 파일에서 찾아옵니다

하지만 아직 config/urls.py 에는 ```/pybo/ ``` 페이지에 아무런 정보가 없기 때문에 Django는 찾을수 없다고 나오네요<br>

* ※ config/urls.py 파일은 페이지 요청 시 가장 먼저 호출 되는 파일입니다 주로 요청한 URL 과 이에 맞는 View function 을 연결합니다
  View function 은 우리가 보는 화면을 보여 주기 위한 function 이며 앱 디렉토리에 보이는 views.py가 바로 그 역활을 하는것 입니다

```
현 상황 예시

User : localhost:8000/pybo/ 으로 이동하고싶어
Django : Umm.. /pybo/ 를 요청했네 ? config/urls.py 에 이런게 있나 ?
' 
' 
' 
Django : 이런 아직 pybo/ 라는 url이 등록되어있지 않잖아 ? 유감이지만 Error야 :(

Result = Page not found(404) ....
```


# URL 매핑

이제 해야 할 일은 config/urls.py에 페이지 요청을 이해할 수 있도록 연결망을 만들어 줄겁니다<br>
앞으로 무언가 url을 추가할때 URL 매핑 을 추가하겠다 라고 하겠습니다

* 매핑이란 프로젝트를 실행하게 되면 위 상단 URL 표시에 localhost:8000/프로젝트명/파일명/ 이렇게 하는대신
간단하게 localhost:8000/파일명 으로 나오게 할수 있는것을 의미 합니다 (추후 자세한 내용 추가 할것)

```
파일명 : config/urls.py

from django.contrib import admin
from django.urls import path
from app_name import views ★ 추가


urlpatterns = [
    path('admin/', admin.site.urls),
    path('pybo/', views.index), ★ 추가
 ] 
```

urlpatterns 변수를 보면 Path 함수를 사용하여 pybo/URL 과 views.index 로 매핑을 추가하였습니다.<br>
views.index는 pybo/views.py 파일의 index function 을 의미 합니다 이런 식으로 URL 과 View 함수를 연결시킵니다

```
현 상황 예시

User : 이제 localhost:8000/pybo/ 으로 이동하고 싶은데 
Django : Umm.. /pybo/ 를 요청했네 ? config/urls.py 에 이런게 있나 ?
' 
' 
' 
Django : 오 좋아 pybo/ 라는 url이 존재하고 views.py 의 index function도 있으니 결과를 보여줘야지 
```

# View

이제 연결망 을 만들어주었으니 이제 화면을 나타낼 차례입니다 아직은 오류페이지를 나타내지만<br>
이 페이지에 친숙해질 필요가 있습니다 ! 오류 원인은 URL 매핑을 추가한 View function을 index로 지정했는데<br>
views.py 에는 현재 index 가 없기 때문입니다

얼른 만들어서 해결하도록 하겠습니다

```
파일명 pybo\views.py

from django.http import HttpResponse ★ 추가

--- function 추가

def index(request):
    return HttpResponse("Hello World")

--- end

```
이제 localhost:8000/app_name/ 페이지에 접속하면 웹 브라우저에 Hello World 라는 문자열이 보일 것 입니다<br>

지금은 간단하게 사용해본 HttpResponse 는 페이지 요청에 대한 응답을 할 때 사용하는 장고 클래스 이고<br>
Hello World 라는 문자열을 전달하여 웹 브라우저에 그대로 출력되도록 아주 간단하게 사용한 것 입니다

# index(request)
<br>
* index function 의 매개변수 request는 Django에 의해 자동으로 전달되는 HTTP 요청 객체 입니다
* request 는 사용자가 전달한 데이터를 확인할 때 사용됩니다

# 마무리
<br>
첫번째 Django 프로그램 을 만들어봤고 다음 포스팅에는 개발 흐름 에 대한 내용을 간단하게 포스팅 후<br>
데이터를 개발하는 것 으로 진행하겠습니다 <br>




  


