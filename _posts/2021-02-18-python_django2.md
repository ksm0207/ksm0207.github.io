---
title: Django로 게시판 만들기 - 01 ( 개발환경 준비하기 )
author: Kim
date: 2021-02-18 08:56 +0900   # 2019-08-20 19:34:00 0900
categories : ["Python", "Django"]
tags: [Django]
comments : true
---

본 포스팅은 Python + Django 개발환경을 준비해보는것이 주 목적 입니다<br>
Django는 Python 으로 만들어진 웹 프레임워크 이기 때문에 Python 설치는 필수로 해줘야 합니다

# Python 설치하기 
<br>

<a href="https://www.python.org/downloads/">Python Downloads</a>
자신의 개발환경에 맞게 적절하게 설치를 진행합니다<br>

설치 작업을 하기 전에 ``` Add Python version to Path ``` 옵션을 선택하여  Path 설정을 해줍니다<br>
※ Path 설정은 Python이 설치된 경로를 컴퓨터가 인식할수 있도록 알려주는것 입니다

설치가 완료 되었다면 cmd로 확인해볼까요?
```
 C:\Users\user>python -v
 Python 3.8.3 (어쩌구 저쩌구.. 설치된 날짜  .. 등등)
```

만약에 찾을 수 없는 명령 이라고 나온다면 내려받은 설치 파일을 다시 실행하여 재설치를 권장합니다


# Python 가상 환경 만들기

Python 가상 환경은 프로젝트를 진행할 때 독립된 환경을 만들어 주는 도구 입니다
이것이 필요한 이유는 다음과 같은 예시로 들어보겠습니다

개발자 A는 2개의 Python 프로젝트를 관리해야한다고 가정하고 프로젝트 이름은 Python -1 Python -2 라고 합니다
이때 각자 필요한 Python 버전이나 라이브러리 버전이 다를 수 있는데 이때 하나의 컴퓨터에 서로 다른 버전의 Python을 설치해야 하는 문제가 생깁니다

이러면 개발 환경은 구축하기도 어렵고 사용하기도 힘들어서 이를 해결해주는것이 가상 환경 입니다 <br>
하나의 컴퓨터에 독립된 가상 환경을 여러 개 만들 수 있는 장점이 있습니다

# 가상 환경 및 디렉토리 생성하기

가상 환경을 만들어 보기위해 명령 프롬포트 (CMD) 를 실행하여 다음과 같은 명령어를 입력해줍니다

```
C:\Users\user>cd \

C:\>mkdir myDjango

C:\>cd myDjango

C:\myDjango>

루트 디렉토리는 반드시 myDjango 이라고 지을 필요는 없습니다.
```

이제 디렉토리를 만들었으니 가상 환경을 만들어 봅시다

```
C:\myDjango>python -m venv myfirst_web 가상 환경 이름
해석 : C:\ 가상환경_디렉토리> python -m venv 가상환경 이름 짓기 

python -m venv 이것은 Python 모듈 중 venv 라는 모듈을 사용한다는 의미입니다

```

가상환경에 진입해볼까요?

```
C:\myDjango> cd C:\myDjango\myfirst_web\Scripts 명령 실행 (1)
'
'
'
C:\myDjango\myfirst_web\Scripts> activate 명령 실행 (2)
※ 가상환경에 진입하려면 생성한 myfirst_web 가상 환경에 있는 Scripts 디렉토리의 activate 명령을 수행합니다

(1) (2) 절차를 진행하게 되면 아래 와 같은 결과를 확인할 수 있습니다 

(myfirst_web) C:\myDjango\myfirst_web\Scripts>

※ 가상환경에 벗어나려면 deactivate 명령을 실행합니다 벗어나면 (myfirst_web) 프롬프트가 사라져 있을것 입니다
```

# Django 설치하기
<br>
이제 앞에서 만든 가상 환경에 Django를 설치하겠습니다

설치는 아래와 같은 명령어로 진행해줍니다 ( CMD으로 진행 )
```
C:\myDjango\myfirst_web\Scripts> pip install django==3.1.3
```
pip은 Python 라이브러리를 설치하고 관리해 주는 Python 도구입니다<br> 
명령프롬포트에 만약 pip 버전이 최신버전이 아니라는 메세지를 나타난다면 
<br>
아래와 같은 명령어로 해결해줍니다

``` python -m pip install -- upgrade pip ```

여기까지 진행하였다면 개발환경은 모두 맞추게 된것입니다<br>
다음 포스팅에는 Django 프로젝트 생성하는법을 알아보도록 하겠습니다 감사합니다.




