---
title: "Java 문법 6. 상속 (inheritance) 과 다형성 (polymorphism)"
excerpt: "Java 상속과 다형성의 이해"

categories:
  - JavaGrammar
tags:
  - [Java, Grammar]

comments: true
toc: true
toc_sticky: true

date: 2022-11-29
last_modified_at: 2022-12-04
---

## 상속 (inheritance)

> ### 1. 상속이란

- 기존의 class(부모/슈퍼 클래스)를 재사용하여 새로운 class(자식/서브 클래스)를 작성하는 것을 말한다
- 기존의 class가 가지고 있는 멤버(필드, 메소드)들을 새로 작성할 클래스에서 직접 만들지 않고 상속을 받음으로서 새 클래스가 자신의 멤버처럼 사용할 수 있다
- 여러 후손 클래스들의 중복되는 멤버들을 부모 클래스에서 작성/관리 함으로서 중복도를 줄이고 코드 양을 줄일 수 있다
- <u>클래스의 재사용</u>과 연관된 일련의 클래스들에 대한 공통적인 규약을 정의 할 수 있다
- 자바에서는 멤버의 모호성을 없애기 위해, 클래스 간의 <u>다중상속은 허용하지 않는다</u>  
  => 단일상속만 지원한다

<br>

> ### 2. 특징

- 모든 클래스는 Object 클래스의 후손이다

  - Object 클래스가 제공하는 메소드를 오버라이딩하여 메소드 재구현이 가능하다

- 부모 클래스의 생성자, 초기화 블록은 상속할 수 없다

  - 자식 클래스 생성 시, 부모 클래스 생성자가 먼저 실행됨
  - 자식 클래스 생성자 안에 부모 클래스 생성자를 호출하고 싶으면 super()를 활용

- 부모의 private 멤버는 상속은 되지만 직접 접근이 불가하다

  - 자식 객체 생성시에 부모의 필드 값도 전달 받은 경우, 자식 생성자 안에서 부모의 private필드에 직접 접근하여 대입 불가하다
  - 자식 생성자 안에서 super() 이용하여 전달받은 부모 필드 값을 부모 생성자 쪽으로 넘겨 생성하거나 , setter/getter 메소드를 이용하여 접근한다

- 단일 상속(Single Inheritance)만 가능하다

  - 자바에서는 다중 상속을 지원하지 않는다
  - 클래스간의 관계가 다중상속보다 명확하고 신뢰성 있는 코드를 작성 할 수 있다

- 부모 클래스의 레퍼런스 변수로는 부모클래스에만 접근이 가능하다
  - 자식 객체로 접근하려면 부모 클래스에서 자식 클래스로 강제 형변환을 시켜주어야 한다  
    => ex) `((Child) parent).method();`

<br>

> ### 3. 방법

#### [ 상속 지정 ]

```java
[접근제한자] class 클래스명 extends 부모클래스명 {}
public class Child extends Parent {}

```

- 클래스 간의 상속시에는 `extends` 키워드 사용
- extends 뒤에 부모가 되는 클래스를 입력한다
- 부모가 되는 클래스를 슈퍼(super) 클래스라고하고 자식클래스는 후손/하위/자식/파생(sub) 클래스라고 한다
- 부모 필드의 멤버변수들과 메소드들을 모두 상속받아 사용이 가능하지만 private 멤버는 직접 접근이 불가능하다

<br>

#### [ super()와 super ]

자식클래스에서 부모클래스의 생성자나 멤버에 접근하고싶을 때 `super` 키워드를 사용한다

- `super()` 생성자

  - 부모 생성자를 호출하는 메소드이다
  - 기본적으로 후손 생성자에 부모 생성자가 포함되어있다
  - 후손 객체 생성시에는 부모부터 생성이 되기 때문에 후손 클래스 생성자 안에는 부모 생성자를 호출하는 super()가 첫줄에 존재한다  
    => 부모 생성자가 가장 먼저 실행되어야하기 때문에 명시적으로 작성시에도 반드시 <u>첫 줄에</u> 작성해야 한다  
    => 매개변수가 있는 부모 생성자 호출은 `super(매개변수...)`를 넣어서 사용한다

- `super` 레퍼런스

  - 상속을 통한 자식 클래스 정의 시 해당 자식 클래스의 부모 객체를 가리키는 참조변수
  - 자식 클래스 내에서 부모 클래스 객체에 접근하여 필드나 메소드 호출 시 사용한다  
    => 부모클래스의 멤버를 지칭 시 사용
  - `super.부모메소드()` 형태로 사용한다

<br>

#### [ 오버라이딩(Overriding) 과 오버로딩(Overloading) ]

| 오버라이딩(Overriding)                                                    | 오버로딩(Overloading)                                                |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 하위 클래스에서 메소드 정의                                               | 같은 클래스에서 메소드 정                                            |
| 메소드 이름 동일<br>매개변수 동일(개수, 타입)<br>리턴 타입 동일           | 메소드 이름 동일<br>매개변수 다름(개수, 타입)<br>리턴 타입 상관 없음 |
| 자식 메소드의 접근 범위가 부모 메소드의 접근 범위보다 넓거나 같아야 함    | 접근 제어자와 상관 없음                                              |
| 자식 메소드의 예외 수가 부모 메소드의 예외 수보다 적거나 범위가 좁아야 함 | 예외처리와 상관 없음                                                 |
|                                                                           |

- 오버라이딩(Overriding)

  - 자식 클래스가 상속받은 부모 메소드를 재작성 하는 것이다  
    => 부모가 제공하는 기능을 후손이 일부 고처 사용하겠다는 뜻
  - 자식 객체를 통한 실행 시 <u>후손 것이 우선권</u>을 가진다  
    => 부모쪽에 동일한 이름의 메소드가 있더라도 자식쪽에서 재정의된 메소드를 실행시킨다

  - 특징

    - 메소드 헤드라인 위에 `@Override` Annotation 표시  
      => 작성하지 않아도 동작상의 문제는 없지만 명시해주는 것을 권장한다  
      => 해당 Annotation을 붙였을 경우 문법에 맞지 않는다거나 부모 메소드가 변경되었거나 했을 경우 알아보기 쉽게 표시해주는 등 유지보수에 용이함
    - 접근제어자를 부모것보다 같거나 <u>더 넓은 범위</u>로 변경 가능하다(더 작은 범위는 안됨!)
    - 부모 메소드의 예외처리 클래스 처리범위보다 <u>좁은 범위</u>로 예외처리 클래스 수정 가능

  - 동적 바인딩

    - 바인딩(binding)이란 메소드에 대한 호출과 실제 구현된 메소드의 코드와 연결되는 것을 말한다(크게 정적/동적 바인딩이 있다)
    - 동적 바인딩은 객체의 타입이 실행중에 결정된 것을 말한다  
      (정적 바인딩은 객체의 타입이 컴파일러의 의해 컴파일 되는 시점에 결정되는 것, private, final, static 등)
    - 상속관계의 오버라이딩 된 메소드는 동적 바인딩을 하는 메소드이다

  - 성립 조건(부모와 자식 클래스의 메소드를 비교했을 때)

    - 메소드 이름이 동일해야 한다
    - 매개변수의 개수, 타입이 동일해야한다
    - 리턴 타입이 동일해야 한다
    - private 메소드는 오버라이딩 불가
    - final 메소드는 오버라이딩 불가

- 오버로딩(Overloading)

  - 한 클래스 내에서 같은 이름의 메소드를 여러 개 정의 하는 것
  - 메소드의 리턴타입은 오버로딩 조건과는 관계 없다
  - 동일한 기능을 수행하는 메소드가 전달값을 각각 다르게 받아서 구동 되는 경우 사용된다

  - 성립 조건

    - 메소드 이름이 같을 것
    - 매개변수를 다르게 가질 것(매개변수 타입, 개수, 순서)

<br>

> ### 4. 예외

#### [ final 예약어 ]

더이상 확장이 불가능함을 알리는 예약어로, 지역변수/필드/메소드/클래스에 붙일 수 있으며 각각 의미하는 바가 다르다

- final 클래스

  ```java
  public final class FinalClass {}
  ```

  - 상속이 불가능한 클래스이다(= 종단 클래스)
  - 부모 클래스가 될 수 없는 클래스라는 의미가 된다
  - 클래스에 abstract와 final 동시에 사용이 불가능하다

<br>

- final 메소드

  ```java
  public final void method() {}
  ```

  - 상속 시 오버라이딩이 불가능한 메소드이다
  - 메소드에 static과 abstract 동시에 사용이 불가능하다
  - abstract 메소드의 접근제어자로 private 사용이 불가능하다

- final 변수

  ```java
  final int NUM = 10;
  ```

  - 변수를 상수화한다
  - 변수에 기록된 값을 변경할 수 없도록 한다
  - 상수화시키면 초기값도 변경할 수 없으므로 반드시 선언과 함께 초기화도 해야한다
  - final로 선언된 변수는 모두 대문자로 표기해주는것이 관례이다

<br>

## 다형성 (polymorphism)

> ### 1. 객체지향개념에서의 다형성

- 객체지향 프로그래밍의 3대 특징 중 하나
- 여러가지 타입을 한가지 타입으로 처리할 수 있는 기술
- 자바에서는 한 타입의 참조변수로 여러타입의 객체를 참조할 수 있다  
  => 부모 클래스 타입의 참조변수로 자식클래스의 인스턴스 참조 가능
  => 자식 클래스 타입의 인스턴스를 생성할 때, 부모 클래스 타입의 참조변수 이용 가능

- 장점
  - 하나의 부모 타입으로 모든 자식 객체들을 받을 수 있다
  - 편리함, 코드 수 감소, 생산성 증대를 가져온다

<br>

> ### 2. 클래스 형변환

클래스 간의 형 변환은 반드시 상속관계에 있는 클래스끼리만 가능하다

- 업 캐스팅(Up Casting)

  ```java
  Parent p = new Child();
  //=> Parent p = (Parent) new Child();
  ```

  - <u>상속 관계</u>에 있는 클래스간에 부모타입의 참조형 변수가 모든 자식타입의 객체 주소를 받을 수 있다
  - 자동 형변환의 개념으로 부모타입으로의 형변환은 자동으로 되므로 생략이 가능하다

- 다운 캐스팅(Down Casting)

  ```java
  Parent p = new Child();
  p.printParent();
  ((Child) p).printChild();
  ```

  - 강제 형변환의 개념으로 자식타입으로의 형변환은 생략이 불가능하다
  - 반드시 후손타입을 명시해서 형변환을 진행해야 한다
  - 따로 자식으로의 형변환을 명시해주지 않았다면 부모 자신이 가지고 있는 값들만 접근 가능하다

<br>

> ### 3. 다형성 활용

- 객체배열

  ```java
  Parent[] pArr = new Parent[3];

  pArr[0] = new Child1();
  pArr[1] = new Child2();
  pArr[2] = new Child3();
  ```

  - 하나의 부모 클래스 타입 배열공간에 여러 종류의 자식 클래스 객체 저장 가능

- instanceof 연산자

  ```java
  if( pArr[0] instanceof Child ){ }
  ```

  - 현재 참조형 변수가 어떤 클래스 형의 객체 주소를 참조하고 있는지 확인할 때 사용한다
  - `참조변수 instanceof 검사할클래스명` 으로 사용하며 boolean 값을 리턴한다
  - instanceof의 연산 결과가 true 이면 검사한 타입으로 형변환이 가능하다는 의미이다

- `참조변수.getClass().getName()`

  - Object클래스의 메소드로 부모 클래스 이름을 문자열로 반환해준다
