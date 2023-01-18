---
title: "[Lv.2] 전화번호 목록"
excerpt: "전화번호 목록 풀이"

categories:
  - Programmers
tags:
  - [Programmers, Java, Lv.2]

comments: true
toc: true
toc_sticky: true

date: 2023-01-18
last_modified_at: 2023-01-18
---

<p align="center">
  <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/programmers/phone_book.png">
</p>

> ## 내 풀이

<details class="no-arrow" markdown="1">
<summary>[코드보기]</summary>

```java
public boolean solution(String[] phone_book) {
  Arrays.sort(phone_book);
  for( int i=0; i< phone_book.length-1; i++ ){
    if(phone_book[i+1].startsWith(phone_book[i])){
      return false;
    }
  }
  return true;
}
```

</details>
