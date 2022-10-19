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

> 이미지에 링크 삽입

`[![이미지설명(이미지 소스 URL)]](링크 URL)` 형식으로 입력

<br>

## 2. 이미지 삽입
