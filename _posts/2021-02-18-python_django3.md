---
title: Django로 게시판 만들기 - 02 ( 프로젝트 생성 )
author: Kim
date: 2021-02-18 10:40 +0900   # 2019-08-20 19:34:00 0900
categories : ["Python", "Django"]
tags: [Django]
comments : true
---
본 포스팅은 프로젝트 생성하는법을 알아봅니다


# Django 프로젝트 만들기

지난 포스팅에는 개발환경을 설치해보았고 이번에는 본격적으로 프로젝트를 생성해보겠습니다

진행하기전 프로젝트 루트 디렉토리를 만들어줍시다

```
C:\Users\user>cd \

C:\>mkdir my_projects

C:\>cd my_projects

C:\my_projects> 

▲ 프로젝트 루트 디렉터리 생성하는법

▼ 프로젝트 루트 디렉터리 안에서 가상 환경에 진입하는법

C:\first_projects>C:\myDjango\myfirst_web\scripts\activate

최종 결과물
(myfirst_web) C:\first_projects>
```

이번엔 프로젝트를 담을 디렉토리 생성하고 이동합니다
```
(myfirst_web) C:\first_projects>mkdir board_app (프로젝트를 담아줄 디렉토리 이름이 board_app 입니다)

(myfirst_web) C:\first_projects>cd board_app

(myfirst_web) C:\first_projects\board_app>
```

CMD 를 활용하여 명령을 다음과 같이 진행합니다
```
(myfirst_web) C:\first_projects\board_app>django-admin startproject config . 띄어쓰기 주의!!
config . 은 현재 디렉토리에서 프로젝트 디렉토리를 만들라는 의미 입니다
```

프로젝트를 생성하면 파일이 잘 생성 되었는지 확인해볼까요?

```

C:\first_projects\board_app (C 드라이브에 가서 확인해주도록 합니다)
├── config/
│      ├─ asgi.py
│      ├─ settings.py
│      ├─ urls.py
│      ├─ wsgi.py
│      └─ __init__.py
└── manage.py
.....
```
이제 개발 서버를 구동하고 웹 사이트에 접속해봅니다
현재 프롬프트 에서 ``` python manage.py runserver``` 명령을 실행하면 개발 서버가 구동되는것을 확인할수 있습니다.
서버를 종료 시키는 명령은 ``` ctrl+C  ``` 입니다



# 마무리

본 프로젝트는 Visual Studio Code 기준으로 진행되며 Pycham 으로 개발을 하셔도 무방합니다<br>
지금까지 만든 프로젝트 디렉토리를 편집기에서 열어주도록 하여 작업을 진행할것 입니다

장고의 설정값이 들어 있는 Settings.py 파일에서 언어와 시간을 한국 값으로 바꿔볼까요?
먼저 config 폴더에 진입해줍니다

```
파일명 : settings.py

LANGUAGE_CODE = 'ko-kr' 

TIME_ZONE = 'Asia/Seoul'

설정 후 다시 python manage.py runserver 명령 실행

```

이제 개발서버를 구동하였을때 전보다 변화된 브라우저를 확인할수가 있습니다. <br>
다음 포스팅에는 화면을 연결하는 URL 그리고 View에 대해서 알아보도록 하겠습니다 감사합니다.





