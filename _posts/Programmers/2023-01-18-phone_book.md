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

이 문제는 해시로 분류되어있는 문제 중 하나로 출제자의 의도는 아마 hash를 사용하여 이 문제를 푸는 것이었을 것이다  
하지만 아직 hash를 사용하여 푸는 방법을 더 고민해보지 못해서 일단 그 외의 방법으로 푼 방법을 기록해두고 추후 내용을 더 업데이트 하려고 한다

일단 Arrays.sort를 이용해 문자열 배열을 정렬해주었다  
문자열의 정렬이란 숫자와는 다르게 1, 12, 2, 13 이런식으로 값이 있다면 1, 12, 13, 2 순서대로 정렬이 된다  
가장 첫글자끼리 비교하여 정렬하고 그다음은 첫글자가 같은 item 끼리 두번째 글자를 비교하고 하는 식이라고 할 수 있겠다  
따라서 문자열 배열을 sort 하게 되면 자동으로 뒤의 문자가 앞의 문자열을 을 포함하고 있는 구조로 정렬이 되기 때문에 앞과 뒤만 서로 비교를 해주면 되었다

여기서 문자열의 앞쪽에 특정 문자열을 포함하고 있는지에 관한 질의는 `startsWith()`라는 메서드를 이용했다  
startsWith()은 메서드 이름과 같이 앞의 문자열이 매개변수로 주어진 문자열로 시작하느냐를 판단하여 boolean 값을 반환하는 메서드이다

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
