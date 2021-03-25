---
layout: post
title:  "[클린 코드 리뷰] 시스템 11장"
date:   2021-03-24
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- PROGRAMMING
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 시스템 제작과 시스템 사용을 분리하라
* Main 분리
  * 시스템 생성과 시스템 사용을 분리하는 방법
  * 생성과 관련한 코드는 모두 main이나 main이 호출하는 모듈로 옮기고, 나머지 시스템은 모든 객체가 생성되었고 모든 의존성이 연결되었다고 가정한다
  * main 함수에서 시스템에 필요한 객체를 생성한 후 이를 애플리케이션에 넘긴다
  * 애플리케이션은 그저 객체를 사용한다
  * 애플리케이션은 main이나 객체가 생성되는 과정을 전혀 모른다
    * 단지 모든 객체가 적절히 생성되었다고 가정한다
* 팩토리
  * 객체가 생성되는 시점을 애플리케이션이 결정해야 할 때 사용
  * ABSTRACT FACTORY 패턴을 사용한다
  * [추상 팩토리 패턴 ( Abstract Factory Pattern )](https://victorydntmd.tistory.com/300)
* 의존성 주입
  * 내부가 아니라 외부에서 객체를 생성해서 넣어주는 것
  * 재사용성을 높여줌
  * 테스트에 용이
  * 코드 단순화
  * 종속적이던 코드의 수도 줄여줌
  * 왜 사용하는 지 파악하기가 수월, 코드를 읽기 쉬워짐
  * 종속성이 감소. 구성 요소의 종속성이 감소하면, 변경에 민감하지 않게 됨
  * 결합도(coupling)는 낮추면서 유연성과 확장성은 향상시킬 수 있음
  * 객체간의 의존관계를 설정할 수 있음
  * 객체간의 의존관계를 없애거나 줄일 수 있음
  * 참고
    * [[DI] Dependency Injection이란 무엇일까?](https://velog.io/@wlsdud2194/what-is-di)
    * [[DI] Dependency Injection 이란?](https://medium.com/@jang.wangsu/di-dependency-injection-%EC%9D%B4%EB%9E%80-1b12fdefec4f)
* 확장
  * TDD, 리팩터링, 깨끗한 코드는 코드 수준에서 시스템을 조정하고 확장하기 쉽게 만든다
* 횡단(cross-cuttin) 관심사
  * 실제 핵심 로직을 수행하는 Method에서 아무리 설계를 잘하더라도 분리된 모듈로 작성하기 힘든 부분이 발생하는데, 이를 횡단 관심사라 한다
* AOP(Aspect Oriented Programming)
  * 횡단 관심사를 한데 모아 처리
  * 참고
    * [AOP(Aspect Oriented Programming) 란?](https://jaehun2841.github.io/2018/07/20/2018-07-20-spring-aop2/#aop%EC%9D%98-%EB%93%B1%EC%9E%A5%EB%B0%B0%EA%B2%BD)

---


## Previous
'[클린 코드 리뷰] 클래스 10장' -> [Next](https://akfmdl.github.io//programming_clean_code_10/){: .btn}

## Next
'[클린 코드 리뷰] 창발성 12장' -> [Next](https://akfmdl.github.io//programming_clean_code_12/){: .btn}