---
layout: post
title:  "[클린 코드 리뷰] 의미 있는 이름(2장)"
date:   2021-02-12
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- PROGRAMMING
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 의도를 분명히 밝혀라
* 주석이 필요하다면 의도를 분명히 드러내지 못한 것이다
* 이름을 주의 깊게 살펴 더 나은 이름이 떠오르면 개선하자
* 변수(혹은 함수나 클래스)의 존재 이유, 수행 기능, 사용 방법이 이름에 잘 녹아내도록 짓자

## 변수가 해당 타입이 아니면 이름이 적지마라
* 예) 여러 계정을 그룹으로 묶을 때, accountList가 실제 List가 아니면 List를 적으면 안된다. accountGroup, bunchOfAccounts와 같이 쓴다

## 서로 흡사한 이름을 사용하지 말자
  * 자동 완성 기능 때문에 제대로 살펴보지 않고 이름을 선택할 수 있다

## 변수 이름에 variable, 표이름에 table이라는 단어를 쓰지 말자
* NameString이 Name보다 뭐가 나은가?

## 불용어를 추가한 이름의 클래스를 만들지 말자
* 예) ProductInfo가 있는데 ProductData를 또 만듦. -> 뭘 써야할지 나중에 헷갈림
* 예) Customer&Customer Object, message&theMessage

## 부르기 쉬운 이름을 붙여라
* 검색하지 쉬운 이름을 사용하라 - 의미만 잘 전달할 수 있다면 긴 이름이 짧은 이름보다 좋다.

```
# 나쁜 예
for (int j=0; j<34; j++>){
    s += (t[j]*4)/5;
}

# 좋은 예
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realTaskDays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

## 인코딩을 피하라
* 굳이 부담을 더하지 마라
* 변수 이름에 타입을 넣지 않아도 된다
* 멤버 변수에 "m_" 접두어를 붙이지 마라
  * 요즘은 this나 self로 해결 가능
  * ref : [헝가리안 표기법, 이제는 사라져야 할 구시대의 유물](https://santacop.tistory.com/6)
  * 헝가리안 표기법 : 변수나 함수의 이름에 그 종류, 곧 흔히 데이터 타입 따위를 명시하는 표기법
* 인터페이스 클래스와 구현 클래스
  * 인터페이스 이름은 접두어를 붙이지 않는 게 좋다
  * 인터페이스 클래스 이름과 구현 클래스 이름 중 하나를 인코딩해야 한다면 구현 클래스 이름을 택하자
```
IShapeFactory보단 CShapeFactory
```

## 남들도 알만한 변수명을 지어라
* 루프에서 반복 횟수를 세는 i,j,k는 괜찮다(I는 절대 안됨)
* 전문가 프로그래머는 자신의 능력을 좋은 방향으로 사용해 남들이 이해하는 코드를 내놓는다

## 클래스 이름은 명사나 명사구로
동사는 사용하지 않는다
```
# 좋은 예
Customer, WikiPage, Account, AddressParser

# 나쁜 예
Manager, Processor, Data, Info
```

## 메서드 이름은 동사나 동사구로
* ex) postPayment, deletePage
* 접근자(Accessor), 변경자(Mutator), 조건자(Predicate)는 javabean 표준에 따라 값 앞에 get, set, is를 붙인다
```
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```
* 생성자(Constructor)를 중복정의(overload)할 때는 정적 팩토리 메서드를 사용한다. 메서드는 인수를 설명하는 이름을 사용한다

```
# 좋은 예
Complex fulcrumPoint = Complex.FromRealNumber(23.0);

# 나쁜 예
Complex fulcrumPoint = new Complex(23.0);
```

* 생성자 사용을 제한하려면 해당 생성자를 private으로 선언한다

## 기발한 이름보단 명료한 이름
의도를 분명하고 솔직하게 표현하라

## 한 개념에 한 단어를 사용하라
* 똑같은 메서드를 클래스마다 fetch, retrieve, get으로 제각각 부르면 혼란스럽다
* 메서드 이름은 독자적이고 일관적이어야 한다. 그래야 주석을 뒤져보지 않고도 프로그래머가 올바른 메서드를 선택한다
* 지금까지 구현한 메서드와 다른 개념의 메서드를 만든다면 단어도 다르게 사용하는 것이 맞다

## 코드를 읽을 사람도 프로그래머다
* 전산 용어, 알고리즘 이름, 패턴 이름, 수학 용어를 사용해도 괜찮다
* JobQueue를 모르를 프로그래머가 있을까?

## 맥락이 분명하게 보이는 클래스, 메서드, 변수를 만들어라
함수를 끝까지 읽고 알고리즘을 이해해야 그제서야 변수의 의미를 파악할 수 있는 건, 함수가 너무 길거나 복잡하다는 것이다. 클래스로 만들고 그 안에서 맥락에 맞게 메서드로 쪼개야 한다.

## 불필요한 맥락을 없애라
accountAddress와 customerAddress는 Address 클래스 인스턴스로는 좋은 이름이나 클래스 이름으로는 적합하지 못하다. 그냥 Address가 좋다.

---


## Previous
'[클린 코드 리뷰] 깨끗한 코드(1장)' -> [Next](https://akfmdl.github.io//programming_clean_code_1/){: .btn}

## Next
'[클린 코드 리뷰] 함수(3장)' -> [Next](https://akfmdl.github.io//programming_clean_code_3/){: .btn}