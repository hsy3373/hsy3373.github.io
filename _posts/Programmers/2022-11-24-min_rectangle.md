---
title: "[Lv.1] 최소 직사각형"
excerpt: "최소 직사각형 풀이"

categories:
  - Programmers
tags:
  - [Programmers, Java, Lv.1]

comments: true
toc: true
toc_sticky: true

date: 2022-11-24
last_modified_at: 2022-11-24
---

<p align="center">
  <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/programmers/min_rectangle.png">
</p>

> ## 내 풀이

이 문제의 포인트는 각 명함들을 어떻게 눕히느냐에 따라 가로 세로 길이가 반전될 수도 있다는 부분같다  
나는 for문으로 주어진 배열을 돌며 총 두개의 값을 추출해내는것으로 접근했다  
1\. int max : 각 명함의 길이 중 가장 큰 값들만을 비교해 그중에서 제일 큰 값을 저장  
2\. int min : 각 명함의 길이 중 가장 작은 값들만을 비교해 그중에서 제일 큰 값을 저장  
그리고 모든 루프를 돌고 난 후 나온 값으로 면적을 구해 return 을 걸어주는 방식으로 마무리 지었다

<details class="no-arrow" markdown="1">
<summary>[코드보기]</summary>

```java
 public int solution(int[][] sizes) {
        int max = 0;
        int min = 0;

        for(int[] arr : sizes ) {
        	if (arr[0] >= arr[1]) {
        		max = max >= arr[0] ? max : arr[0];
        		min = min >= arr[1] ? min : arr[1];
        	}else {
        		max = max >= arr[1] ? max : arr[1];
        		min = min >= arr[0] ? min : arr[0];
        	}
        }
        return max * min;
    }
```

</details>

<br>

> ## 다른사람의 풀이

나는 위에서 각 명함의 가로세로 길이를 if문을 통해 일일이 비교했다  
하지만 다른 사람들의 풀이를 찾아보니 `Math.max()`와 `Math.min()`을 사용해 풀어낸 경우가 많았다  
명함의 길이 중 가장 큰값들 중의 큰값, 가장 작은값들 중의 큰값을 구해내는 기본 원리는 같았지만  
if문과 삼항연산자를 섞어서 늘어놓은 내 코드와는 달리 한눈에 알아보기 쉽게끔 짜여져있어 기록해둔다

<details class="no-arrow" markdown="1">
<summary>[코드보기]</summary>

```java
for (int[] card : sizes) {
    length = Math.max(length, Math.max(card[0], card[1]));
    height = Math.max(height, Math.min(card[0], card[1]));
}
```

</details>

<br>
