---
title: "[Markdown] 링크와 이미지 삽입"
excerpt: "markdown 문법으로 링크 삽입과 이미지 삽입 방법"

categories:
  - Blog
tags:
  - [Blog, Markdown]

comments: true
toc: true
toc_sticky: true

date: 2020-10-19
last_modified_at: 2020-10-19
---

## 1. 링크 넣기

> URL 직접 입력 `<>`

URL을 `<>`로 감싸서 입력.

```
<http://www.google.com>
```

<http://www.google.com>

<br>

> 인라인 주소 삽입

`[주소에 대한 설명](실제 주소)` 식으로 작성.

```
[Google](http://www.google.co.kr) 이렇게 나옵니다
```

[Google](http://www.google.co.kr) 이렇게 나옵니다

<br>

> 링크에 title(설명) 추가

삽입된 링크에 마우스 오버 시 표시되는 title(설명)을 추가할 수 있다.

```
[Google](http://www.google.co.kr "구글로 이동 가능한 URL입니다")
```

[Google](http://www.google.co.kr "구글로 이동 가능한 URL입니다") <- 마우스 커서를 올려 보세요

<br>

> 참조 링크 삽입

같은 링크 URL을 여러번 입력해야하거나 글 안의 링크들을 따로 관리하고 싶을 때 이용하기 편한 기능.

`[주소에 대한 설명]: 참조링크URL` 형태로 선언하고 URL을 삽입하고자 하는 부분에 `[주소에 대한 설명]`부분만 입력

```
[주소설명][주소2]  <- 선언한 참조 링크에 또다른 주소 설명을 달아 이용할 수도 있다
여기는 [주소1] 을 참조하세요
쏼롸쏼롸 몇줄 지남~~
여기도 [주소1]을 참조하시고 이 뒤는 [주소2] 을 참조하세요.

이후 글 마지막 부분에 선언해도 됨
[주소1]: http://www.google.com
[주소2]: http://www.facebook.com "마우스 커서를 올리면 이 설명이 뜹니다"
```

[주소설명][주소2] <- 선언한 참조 링크에 또다른 주소 설명을 달아 이용할 수 있다  
여기는 [주소1] 을 참조하세요  
쏼롸쏼롸 몇줄 지남~~  
여기도 [주소1]을 참조하시고 이 뒤는 [주소2] 을 참조하세요.

이후 글 마지막 부분에 선언해도 됨

[주소1]: http://www.google.com
[주소2]: http://www.facebook.com "마우스 커서를 올리면 이 설명이 뜹니다"

<br>

> 이미지와 링크 연결

`[![이미지설명](이미지 소스 URL)](링크 URL)` 형식으로 입력

```
[![이미지설명](http://www.google.com/images/logo.gif)](http://www.google.com/)

```

[![이미지설명](http://www.google.com/images/logo.gif)](http://www.google.com/)

또는 참조 링크를 사용하여 이미지에 링크를 연결할 수 있다.

```
![이미지설명][logo_img]

[![이미지설명][logo_img]][google_url]

[logo_img]: http://www.google.com/images/logo.gif
[google_url]: http://www.google.com/ "click to visit Google.com"
```

![이미지설명][logo_img]

[![이미지설명][logo_img]][google_url]

[logo_img]: http://www.google.com/images/logo.gif
[google_url]: http://www.google.com/ "click to visit Google.com"

<br>

## 2. 이미지 삽입

> \!\[이미지 설명\]\(경로\)를 사용한다

```
![내 프로필 이미지](/assets/images/profile_400x400.jpg)
```

![내 프로필 이미지](/assets/images/profile_400x400.jpg)

<br>

> 이미지 속성 조정 방법

HTML에서 사용하는 img 태그를 사용하여 속성 부여가 가능하다.

```
<img align="left" width="100" height="100" title="이미지 제목" alt="설명"  src="/assets/images/profile_400x400.jpg">
```

<img align="left" width="100" height="100" title="이미지 제목" alt="설명"  src="/assets/images/profile_400x400.jpg"><br>
　<- 마우스 커서를 올려보세요

<br>

다만 이미지를 가운데로 두고 싶을 때는 \<p>태그로 감싸주어야 한다

```
<p align="center">
  <img width="300" height="300" src="/assets/images/profile_400x400.jpg">
</p>
```

<p align="center">
  <img width="300" height="300" src="/assets/images/profile_400x400.jpg">
</p>

<br>

> 이미지 경로

이미지의 경로는 URL 주소와 상대경로를 사용하는 방법이 있다.  
URL 경로의 경우 github에 업로드 하여 그 이미지 주소를 따오는 방법이 있고  
상대경로를 사용할 경우 위에서 예시로 썼던 것과 같이 경로를 지정해주어 끌어오는 방법이 있다.

만약 github 웹 주소로 이미지 삽입이 제대로 안된다면 raw=true를 붙여 사용해야 한다.  
이와 관련된 [참고 링크(클릭)](https://www.javaer101.com/ko/article/9737552.html)
