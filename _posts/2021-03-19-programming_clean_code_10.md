---
layout: post
title:  "[클린 코드 리뷰] 클래스 10장"
date:   2021-03-19
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- PROGRAMMING
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 클래스 체계
아래의 순서로 클래스를 신문 기사처럼 읽히도록 구성한다.
우선 변수 목록이 나온다.

`정적 공개(static public) 상수 -> 정적 비공개(static public) 변수 -> 비공개 인스턴스 변수`

다음 함수가 나온다. 추상화 단계가 순차적으로 내려간다.

`공개 함수 -> 비공개 함수(자신을 호출하는 공개 함수 직후)`

## 클래스는 작아야 한다
클래스를 설계할 때도, 함수와 마찬가지로, '작게'가 기본 규칙이다. 그럼 얼마나 작아야 하는가?

함수는 물리적인 행 수로 크기를 측정했다. 클래스는 클래스가 맡은 책임을 센다.

`만능 클래스는 No!`

클래스 이름은 해당 클래스 책임을 기술해야 한다. 클래스 이름이 모호하다면 책임이 너무 많아서다.
* 예) Processor, Manager, Super

또한 클래스명은 "if", "and", "or", "but"을 사용하지 않고 25단어 내외로 가능해야 한다.

* 단일 책임 원칙
  * 큰 클래스 몇 개가 아니라 작은 클래스 여럿으로 이뤄진 시스템이 더 바람직하다
  * 작은 클래스는 각자 맡은 책임이 하나며, 변경할 이유가 하나며, 다른 작은 클래스와 협력해 시스템에 필요한 동작을 수행한다
* 응집도
  * 클래스는 인스턴스 수가 작아야 한다
  * 응집도가 높다는 말은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미다
  * '함수를 작게, 매개변수 목록을 짧게'라는 전략을 따르다 보면 때때로 몇몇 메서드만이 사용하는 인스턴스 변수가 아주 많아진다
  * 응집도가 높아지도록 변수와 메서드를 적절히 분리해 새로운 클래스 두세 개로 쪼개준다
* 응집도를 유지하면 작은 클래스 여럿이 나온다
  * 큰 함수를 작은 함수 여럿으로 쪼개다 보면 종종 작은 클래스 여럿으로 쪼갤 기회가 생긴다. 그러면서 프로그램에 점점 더 체계가 잡히고 구조가 투명해진다
* 리팩토링을 하면 프로그램이 길어지는데, 그 이유는?
  * 좀 더 길고 서술적은 변수 이름을 사용
  * 코드에 주석을 추가하는 수단으로 함수 선언과 클래스 선언을 활용
  * 기능 단위로 클래스를 나누어 클래스 개수가 많아짐
  * 가독성을 높이고자 공백을 추가하고 형식을 맞춤

## 변경하기 쉬운 클래스
대다수 시스템은 지속적인 변경이 가해진다. 어떤 변경이든 손대면 다른 코드를 망가뜨릴 잠정적인 위험이 존재한다.

* 변경이 필요해 '손대야' 하는 클래스
  * 하나의 클래스에 select, find, create 등 너무 많은 기능을 담당하고 있음

```
public class Sql {
  public Sql(String table, Column[] columns)
  public String create()
  public ...
  public ...
  public ...
  public ...
  public ...
  public ...
  public ...
  public ...
}
```

* 닫힌 클래스 집합
  * 공개 인터페이스를 각각 Sql 클래스에서 파생하는 클래스로 만듦
  * 비공개 메서드는 해당하는 파생 클래스로 옮김
  * 모든 파생 클래스가 공통으로 사용하는 비공개 메서드는 따로 유틸리티 클래스로 만듦
  * 클래스가 서로 분리됨
  * 다른 기능을 추가할 때도 기존 클래스를 변경할 필요가 없음

```
abstract public class Sql {
  public Sql(String table, Column[] columns)
  abstract public String generate();
}

public class CreateSql extends Sql {
  public CreateSql(String table, Column[] columns)
  @Override public String generate();
}

public class ... extends Sql {
  public ...
  @Override public String generate();
}
```

* 변경으로부터의 격리
  * 요구사항은 언제나 변하기 마련이며, 어차피 수정될 코드라 생각해야 한다
  * 상세한 구현에 의존하는 코드는 테스트가 어렵다
  * 상세한 구현에 의존하는 클래스는 구현이 바뀌면 위험에 빠진다
  * 인터페이스와 추상 클래스를 사용해 구현이 미치는 영향을 격리하자
  * 결합도를 낮추면 유연성과 재사용성이 높아진다
  * 결합도가 낮다는 건 시스템 요소가 다른 요소로부터 그리고 변경으로부터 잘 격리되어 있다는 의미다


> 참고  
[파이썬(PYTHON) 클린코드 #9_ SOLID, 인터페이스 분리 원칙(ISP)](https://doorbw.tistory.com/239)




---


## Previous
'[클린 코드 리뷰] 단위 테스트 9장' -> [Next](https://akfmdl.github.io//programming_clean_code_9/){: .btn}

## Next
'[클린 코드 리뷰] 시스템 11장' -> [Next](https://akfmdl.github.io//programming_clean_code_11/){: .btn}