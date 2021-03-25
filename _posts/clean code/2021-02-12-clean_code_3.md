---
layout: post
title:  "[클린 코드 리뷰] 함수 3장"
date:   2021-02-12
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- PROGRAMMING
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 작게 만들어라
되도록이면 5줄 이내로 짧게 만들자
* if/else/while 문 등에 들어가는 블록은 한 줄이어야 한다. 대개 거기서 함수를 호출하고, 함수 이름도 명료하다면 코드를 이해하기 쉬워진다
* 들여쓰기 수준은 1단이나 2단을 넘어가지 말자

## 한 가지만 해라
문제는 그 '한 가지'가 뭔지 감이 안잡힐 때가 있다. 함수의 내용 중 일부를 명료한 이름으로 다른 함수로 추출할 수 있다면 그 함수는 여러 작업을 하는 것이다. 한 가지만 하는 함수는 자연스럽게 섹션으로 나누기 어렵다.

## 함수 당 추상화 수준은 하나
```
# 추상화 수준 高
getHtml()

# 추상화 수준 中
String pagePathName = PathParser.render(pagepath)

# 추상화 수준 下
.append("\n")
```
한 함수내에서 추상화 수준을 섞으면 코드를 읽는 사람이 헷갈린다.

## Switch문
본질적으로 switch문은 N가지를 처리한다. switch문을 완전히 피할 방법은 없다. 하지만, 저차원 클래스에 숨기고 절대로 반복하지 않는 방법은 있다. 상속 관계로 숨긴 후에는 다른 코드에 노출하지 않는다.

## 서술적인 이름을 사용하라
이름이 길어도 괜찮다. 길고 서술적인 이름이 짧고 어려운 이름보다 좋다.
```
testableHtml -> SetupTeardownIncluder.render

isTestable

includesetupAndTeardownPages
```
단 이름을 붙일 때는 일관성이 있어야 한다. 모듈 내에서 함수 이름은 같은 문구, 명사, 동사를 사용한다.
* 예) includesetupAndTeardownPages, includeSetupPages, includeSuiteSetupPages, includeSetupPage 등
* 문체가 비슷하면 이야기를 순차적으로 풀어가기도 쉬워진다

## 함수 인수
함수에서 이상적인 인수 개수는 0개이다. 3개 이상은 피하는 편이 좋다. 테스트 관점에서 보면 인수는 더 어렵다. 인수가 3개를 넘어가면 인수마다 유효한 값으로 모든 조합을 구성해 테스트하기가 상당히 부담스러워진다.

인수가 1개인 경우는 대표적으로 두 가지다
```
1. 인수에 질문을 던지는 경우
bool fileExists("MyFile")

2. 인수를 뭔가로 변환해 결과를 반환하는 경우
InputStream fileOpen("MyFile")

+ 이벤트 함수
passwordAttemptFailedNtimes(int attempts)
```
이 이외에는 인수가 1개인 단항 함수는 가급적 피한다.
* 입력 인수를 변환하는 함수라면 변환 결과는 반환값으로 돌려준다
  * 예) void transform(StringBuffer out) -> StringBuffer transform(StringBuffer in)

## 플래그 인수
이것은 함수가 한꺼번에 여러 가지를 처리한다고 대놓고 공표하는 셈이다. 플래그가 참이면 이걸 하고 거짓이면 거절 한다는 뜻이다.

## 이항 함수
인수가 2개인 함수는 단항 함수보다 이해하기 어렵다. 물론 프로그램을 짜다보면 불가피한 경우도 생기긴 하지만, 그 외에는 무조건 단항함수로 바꾸도록 애써야 한다.
* 예) writeField(outputStream, name) -> outputStream.writeField(name)
  * 혹은 FieldWriter라는 새 클래스를 만들어 구성자에서 outputStream을 받고 write 메서드를 구현한다

## 삼항 함수
삼항 함수를 만들 때는 신중히 고려해야 한다. 순서, 주춤, 무시로 야기되는 문제가 두 배 이상 늘어나기 때문이다.

반면 assertEquals(1.0, amount, .001)와 같은 함수는 이해하기 쉽기 때문에 사용해도 된다.

## 인수 객체
인수가 2-3개 필요하다면 일부를 독자적인 클래스 변수로 선언할 가능성을 짚어보자.
```
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

## 인수 목록
때로는 인수 개수가 가변적인 함수도 필요하다.
```
String.format("%s worked %.2f hours.", name, hours);
```
실제로 String.format 선언부를 살펴보면 이항 함수라는 사실이 분명히 드러난다.
```
public String format(String format, Object... args)
```

## 동사와 키워드
함수의 의도나 인수의 순서와 의도를 제대로 표현하는 좋은 함수 이름을 짓자
* 예) assertEquals -> assertExpectedEqualsActual(expected, actual)
  * 이러면 인수 순서를 기억할 필요가 없어진다

## 부수 효과를 일으키지 마라
* 예) password를 초기화 하는 함수 안에 session 초기화 시키는 기능을 넣어버림

## 출력 인수
일반적으로 우리는 인수를 함수의 입력으로 해석한다. 따라서 인수를 출력으로 사용하지 않도록 주의하자
* 예) appendFooter(s) -> report.appendFooter()

## 명령과 조회를 분리하라
```
# 나쁜 예
-> 이것은 "username"이 "unclebob"으로 설정되어 있는지 확인하는 코드인가? 아니면 설정하는 코드인가??
if set("username", "unclebob")...

# 좋은 예
if attributeExists("username") {
  setAttribute("username", "unclebob");
}
```

## 오류 코드보다 예외를 사용하라
```
if (deletePage(page) == E_OK)...
```
위 코드는 else if... else문을 여러 단계로 중첩되는 코드를 야기한다. 반면 오류 코드 대신 예외를 사용하면 오류 처리 코드가 원래 코드에서 분리되므로 코드가 깔끔해진다.
```
try {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makekey());
}
catch (Exception e) {
  logger.log(e.getMessage());
}
```
단, try/catch 블록은 코드 구조에 혼란을 일으키며, 정상 동작과 오류 처리 동작을 뒤섞는다. 그러므로 try/cath 블록을 별도의 함수로 뽑아내는 것이 더 좋다.
```
private void deletePageAndAllReferences(Page page) throws Exception {
  deletePage(page);
  registry.deleteReference(page.name);
  configKeys.deleteKey(page.name.makekey());
}

private void logError(Exception e) {
  logger.log(e.getMessage());
}
```

## 오류 처리도 한 가지 작업니다.
함수가 한 가지 일만 해야 하듯이, 오류 처리도 한 가지 작업만 해야 한다.

## 의존성 자석
아래와 같은 클래스는 다른 클래스에서 import해 사용해야 하므로, 하나의 enum만 변해도 클래스 전부를 다시 컴파일하고 다시 배치해야 한다.
```
public enum Error {
  OK,
  INVALID,
  NO_SUCH,
  LOCKED,
  OUT_OF_RESOURCES,
  WAITING_FOR_EVENT;
}
```
오류 코드 대신 예외를 사용하면 Exception 클래스에서 파생된다. 따라서 재컴파일/재배치 없이도 새 예외 클래스를 추가할 수 있다.

## 반복하지 마라
반복되는 작업을 함수로, 더 바깥 함수로 묶어 사용하자

## 구조적 프로그래밍
* 함수는 return을 하나만 해야 한다
* 루프 안에서 break나 continue를 사용해선 안된다
* goto는 <b>절대</b> 사용하면 안된다

단일 입/출구 규칙보다 의도를 표현하기 쉬울 때, 함수가 작을 때는 return, break, continue를 여러 차례 사용해도 괜찮다

## 함수 잘 짜는 법
처음엔 길고 복잡하다 -> 하지만 빠짐없이 그 서투른 코드를 테스트하는 단위 테스트 케이스도 만든다 -> 계속 다듬고, 함수를 만들고, 이름을 바꾸고, 중복을 제거한다 -> 메서드를 줄이고 순서를 바꾼다

때로는 전체 클래스를 쪼개기도 한다. 이 와중에도 코드는 항상 단위 테스트를 통과해야 한다.

그제서야 최종적으로 이 장에서 설명한 규칙을 따르게 된다. 처음부터 잘 짜는 사람은 없다.


---


## Previous
'[클린 코드 리뷰] 의미 있는 이름 2장' -> [Next](https://akfmdl.github.io//programming_clean_code_2/){: .btn}

## Next
'[클린 코드 리뷰] 주석 4장' -> [Next](https://akfmdl.github.io//programming_clean_code_4/){: .btn}