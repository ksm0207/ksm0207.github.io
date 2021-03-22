---
title: 블로그 에러 - (1) bundle 문제
author: Kim
date: 2021-03-22 16:13 +0900   # 2019-08-20 19:34:00 0900
categories : ["Error", ""]
tags: [null,null]
comments : true
---

# 블로그 업데이트 에러 발생

블로그 업데이트 중 서버에서 에러가 발생했다는 메시지를 보고 한참 헤매게 되었습니다<br>
나는 무엇이 문제인지 도통 감이 안잡혔고 문제된 에러는 다음과 같았습니다<br>

<img src = "/post/images/error.png">


```
Run bundle exec jekyll b -d "_site$BASE_URL"
bundler: failed to load command: jekyll (/home/runner/vendor/bundle/ruby/2.7.0/bin/jekyll)
LoadError: libffi.so.6: cannot open shared object file: No such file or directory - /home/runner/vendor/bundle/ruby/2.7.0/gems/ffi-1.14.2/lib/ffi_c.so
  /home/runner/vendor/bundle/ruby/2.7.0/gems/ffi-1.14.2/lib/ffi.rb:6:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/ffi-1.14.2/lib/ffi.rb:6:in `rescue in <top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/ffi-1.14.2/lib/ffi.rb:3:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/sassc-2.4.0/lib/sassc/native.rb:3:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/sassc-2.4.0/lib/sassc/native.rb:3:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/sassc-2.4.0/lib/sassc.rb:31:in `require_relative'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/sassc-2.4.0/lib/sassc.rb:31:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-sass-converter-2.1.0/lib/jekyll/converters/scss.rb:3:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-sass-converter-2.1.0/lib/jekyll/converters/scss.rb:3:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-sass-converter-2.1.0/lib/jekyll-sass-converter.rb:4:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-sass-converter-2.1.0/lib/jekyll-sass-converter.rb:4:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-4.2.0/lib/jekyll.rb:195:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-4.2.0/lib/jekyll.rb:195:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-4.2.0/exe/jekyll:8:in `require'
  /home/runner/vendor/bundle/ruby/2.7.0/gems/jekyll-4.2.0/exe/jekyll:8:in `<top (required)>'
  /home/runner/vendor/bundle/ruby/2.7.0/bin/jekyll:23:in `load'
  /home/runner/vendor/bundle/ruby/2.7.0/bin/jekyll:23:in `<top (required)>'
Error: Process completed with exit code 1.
```

뭔가 코드 1번 에서 에러가 발생하여서 프로세스가 종료되었다 뭐.. 이런 내용인 것 같은데<br>
처음에 저게 뭔지 몰라서 열심히 구글링을 해본 것 중 ``` bundler ``` 를 업데이트 해서 성공했다는 사례가 있어<br>
재빨리 업데이트를 시작했습니다<br>
시도해본 명령어 :  ``` bundle update ``` 

약간의 시간이 흘렀고 업데이트가 완료된 순간 커밋을 일단 올리고 봤습니다<br>
커밋된 파일은 ``` Gemfile.lock `` 이였고 변경된 내용을 확인해 본 결과 <br>

<a href = "https://github.com/ksm0207/ksm0207.github.io/commit/77b3457cfd562e3cfc4d80c21cdbaf3063f48d5e">Bundle 업데이트</a>

버전이 업데이트 되면서 블로그도 다시 정상적으로 작동하게 되어 무척 다행이라 생각이 들게 되었습니다<br>
하지만 이번 이슈를 다시 한번 꼼꼼히 살펴볼 필요가 있다고 판단되어<br>
이번 계기로 인해  이 문제에 대한 이슈에 대해 알아봐야겠습니다<br>