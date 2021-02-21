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
                (1) 페이지 요청                            Local Server
                
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
* (2) 서버 에서는 (config/urls.py) URL을 해석해 pybo/views.py 파일의 index function 을 호출하고
* (3) pybo/views.py 에서 index function 을 실행하고 그 결과를 웹 브라우저 에게 전달 하는 과정입니다.<br>
      ※ 존재 할 경우 True 안 할 경우 False

앞으로 의 개발 흐름은 이렇습니다<br>
사용자가 /pybo/ 페이지를 요청 했을때 Local Server 에서 URL을 분석후 연결되어있는 function 을 호출하고<br>
function 의 결과를 브라우저에 화면이 전달 되었을때 우리가 보는 화면과 일치하게 됩니다



