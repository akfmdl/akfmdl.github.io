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

# 의도를 분명히 밝혀라
* 주석이 필요하다면 의도를 분명히 드러내지 못한 것이다
* 이름을 주의 깊게 살펴 더 나은 이름이 떠오르면 개선하자
* 변수(혹은 함수나 클래스)의 존재 이유, 수행 기능, 사용 방법이 이름에 잘 녹아내도록 짓자

# 그릇된 정보를 피하라
* 변수가 해당 타입이 아니면 이름이 적지마라
  * 예) 여러 계정을 그룹으로 묶을 때, accountList가 실제 List가 아니면 List를 적으면 안된다. accountGroup, bunchOfAccounts와 같이 쓴다
* 서로 흡사한 이름을 사용하지 말자
  * 자동 완성 기능 때문에 제대로 살펴보지 않고 이름을 선택할 수 있다
* 변수 이름에 variable, 표이름에 table이라는 단어를 쓰지 말자
  * NameString이 Name보다 뭐가 나은가?
* 불용어를 추가한 이름의 클래스를 만들지 말자
  * 예) ProductInfo가 있는데 ProductData를 또 만듦. -> 뭘 써야할지 나중에 헷갈림
  * 예) Customer&Customer Object, message&theMessage
* 부르기 쉬운 이름을 붙여라
* 검색하지 쉬운 이름을 사용하라 - 의미만 잘 전달할 수 있다면 긴 이름이 짧은 이름보다 좋다.

```for (int j=0; j<34; j++>){
    s += (t[j]*4)/5;
}```

## Previous
'[클린 코드 리뷰] 깨끗한 코드(1장)' -> [Next](https://akfmdl.github.io//programming_clean_code_1/){: .btn}

## Next
'[클린 코드 리뷰] 함수(3장)' -> [Next](https://akfmdl.github.io//programming_clean_code_3/){: .btn}