---
layout: post
title:  "[클린 코드 리뷰] 경계 8장"
date:   2021-03-01
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- CLEAN CODE
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 외부 코드 사용하기
인터페이스 제공자는 적용성을 최대한 넓히려 애쓰고, 사용자는 자신의 요구에 집중하는 인터페이스를 바란다. 이런 문제로 인해 시스템 경계에서 문제가 생길 소지가 많다.
* 마음만 먹으면 어떤 사용자든지 객체를 지울 수 있는 인터페이스
* 중복 코드가 많은 인터페이스
위와 같은 외부 API는 캡슐화시켜 내부에서 사용하도록 해야 한다.

## 경계 살피고 익히기
외부 코드는 익히기도 어렵고 통합하기도 어렵다. 바로 코드를 작성해 외부 코드를 호출하는 대신 먼저 간단한 테스트 케이스를 작성해 외부 코드를 익히면 좋다. 이를 학습 테스트라고 부른다.

예를 들어, log4j 패키지의 도큐먼트를 자세히 읽기 전에 화면에 "hello"를 출력하는 테스트 케이스를 작성한다.

```
@Test
public void testlogCreate() {
  Logger logger = Logger.getLogger("MyLogger);
  logger.info("hello);
}
```

돌려보니 Appender라는 게 필요하다고 해서 문서를 읽어보니 ConsoleAppender라는 클래스가 있다. 그래서 Console Appender를 생성한 후 다시 돌린다.

```
@Test
public void testlogCreate() {
  Logger logger = Logger.getLogger("MyLogger);
  ConsoleAppender appender = new ConsoleAppender();
  logger.addAppender(appender);
  logger.info("hello);
}
```

이번엔 Appender에 출력 스트림이 없다는 사실을 발견하고 구글을 검색한 후 다음과 같이 시도한다.

```
@Test
public void testlogCreate() {
  Logger logger = Logger.getLogger("MyLogger);
  logger.removeAllAppenders();
  logger.addAppender(new ConsoleAppender(
    new PatternLayout("%p &t %m%n")
    ConsoleAppender.SYSTEM_OUT));
  logger.info("hello);
}
```

이제서야 제대로 돌아간다. "hello"가 들어간 로그 메세지가 콘솔에 찍힌다. 그런데 ConsoleAppender에게 콘솔에 쓰라고 알려야 한다니 뭔가 수상하다. ConsoleAppender.SYSTEM_OUT 인수를 제거했더니 문제가 없다. 여전히 "hello"가 찍힌다.

...

이렇게 조금씩 구글을 뒤지고, 문서를 읽어보고, 테스트를 돌린 끝에 log4j가 돌아가는 방식을 상당히 많이 이해했으며 여기서 얻은 지식으로 간단한 단위 테스트 케이스도 더 만들 수 있었다.

그리고 마침내 독자적인 로거 클래스로 캡슐화할 수 있게 되었다.

## 학습 테스트는 공짜 이상이다
학습 테스트에 드는 비용은 없다. 오히려 필요한 지식만 확보하는 손쉬운 방법이다. 학습 테스트는 이해도를 높여주는 정확한 실험이다.

학습 테스트를 이용한 학습이 필요하든 그렇지 않든, 실제 코드와 동일한 방식으로 인터페이스를 사용하는 테스트 케이스가 필요하다. 이런 경계 테스트가 있다면 패키지의 새 버전으로 이전하기 쉬워진다. 그렇지 않다면 낡은 버전을 필요 이상으로 오랫동안 사용하려는 유혹에 빠지기 쉽다.

## 아직 존재하지 않는 코드를 사용하기
아는 코드와 모르는 코드를 분리하는 경계 테스트 케이스가 필요할 때가 있다. 때로는 우리 지식이 경계를 너머 미치지 못하는 코드 영역도 있다.

예)

* API를 팀을 나누어 서로 다른 모듈을 작업할 때 다른 팀이 어떻게 구현할지 모르는 상황에서 테스트를 하기 위해 자체적으로 FakeAPI를 만든다
* 우리가 통제하지 못하며 정의되지도 않은 API는 분리한다
* ADAPTER 패턴으로 API 사용을 캡슐화해 API가 바뀔 때 수정할 코드를 한곳으로 모았다

## 깨끗한 경계
통제하지 못하는 코드를 사용할 때는 향후 비용이 지나치게 커지지 않도록 각별히 주의해야 한다.  
경계에 위치하는 코드는 깔끔히 분리한다. 또한 기대치를 정의하는 테스트 케이스도 작성한다. 통제가 불가능한 외부 패키지에 의존하는 대신 통제가 가능한 우리 코드에 의존하는 편이 훨씬 좋다.

* 외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리하자
* 새로운 클래스로 경계를 감싸거나 APAPTER 패턴을 사용해 우리가 원하는 인터페이스를 패키지가 제공하는 인터페이스로 변환하자

이렇게 하면 코드 가독성이 높아지며, 경계 인터페이스를 사용하는 일관성도 높아지며, 외부 패키지가 변했을 때 변경할 코드도 줄어든다.


---


## Previous
'[클린 코드 리뷰] 오류 처리 7장' -> [Next](https://akfmdl.github.io//programming_clean_code_7/){: .btn}

## Next
'[클린 코드 리뷰] 단위 테스트 9장' -> [Next](https://akfmdl.github.io//programming_clean_code_9/){: .btn}