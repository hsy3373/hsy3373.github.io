---
title: "[Lv.1] 하샤드 수"
excerpt: "하샤드 수 구하기 풀이"

categories:
  - Programmers
tags:
  - [Programmers, Java, Lv.1]

comments: true
toc: true
toc_sticky: true

date: 2020-10-22
last_modified_at: 2020-10-22
---

<p align="center">
  <img width="calc(100% - #{$right-sidebar-width-narrow})" height="auto" src="/assets/images/programmers/harshad.PNG">
</p>

> ## 내 풀이

-> 받은 int값을 String 형태로 변환  
-> split("")으로 공백 단위로 분할하여 배열로 저장  
-> for문으로 배열안의 값들을 돌리며 다시 int형으로 변환 및 총합 도출  
-> 총합과 기존 값을 비교하여 true/false 값 반환

<details class="no-arrow" markdown="1">
<summary>[코드보기]</summary>

```java

class Solution {
    public boolean solution(int x) {

        String[] array = Integer.toString(x).split("");

        int sum =0;

        for(String str : array){
            int num = Integer.parseInt(str);
            sum += num;
        }

        return x % sum == 0;
    }
}
```

</details>

<br>

> ## 다른 사람의 풀이

다른 사람들의 풀이를 찾아보니 위처럼 `String[]`을 사용해도 되지만 아예 `char` 형태로 분리하여 사용하는 방법도 있었다.  
그중 `char` 형태와 람다식을 혼합해 사용한 경우를 가져왔다.

`Integer.toString(num).chars().forEach(char -> sum += char - '0');`

String 형으로 변환 후 바로 char 형으로 분리시킨 뒤 람다식을 사용하여 총합을 구하는 함수를 만든 케이스다(sum은 위에서 따로 int형 변수로 선언 해주었다).

여기서 눈길을 끌었던 점은 람다식의 사용도 있지만 `char` 값에 `- '0'`을 해주면 바로 숫자로 변환된다는 점이었다.  
나는 `Integer.parseInt()`를 주로 써와서인지 이런식의 형변환이 매우 신선해보여서 기록해둔다.
