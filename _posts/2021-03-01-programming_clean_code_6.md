---
layout: post
title:  "[클린 코드 리뷰] 객체와 자료 구조 6장"
date:   2021-03-01
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- PROGRAMMING
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 자료 추상화
변수를 비공개(private)로 정의하는 이유는 남들이 변수에 의존하지 않게 만들고 싶어서다. 변수 사이에 함수라는 계층을 넣는다고 구현이 저절로 감춰지지는 않는다. 구현을 감추려면 추상화가 필요하다.

자료를 세세하게 공개하기보다는 추상적인 개념으로 표현하는 것이 좋다.
* 구체적인 Vehicle 클래스 : 두 함수가 변수값을 읽어 반환할 뿐이라는 사실이 드러난다.
```
public interface Vehicle {
  double getFuelTankCapacityInGallons();
  double getGallonsOfGasoline();
}
```
* 추상적인 Vehicle 클래스 : 정보가 어디서 오는지 전혀 드러나지 않는다.
```
public interface Vehicle {
  double getPercentFuelRamaining();
}
```
이렇듯, 인터페이스나 조회/설정 함수만으로는 추상화가 이뤄지지 않는다. 객체가 포함하는 자료를 표현할 가장 좋은 방법을 심각하게 고민해야 한다.

## 절차적인 코드 VS 객체지향 코드
두 종류의 코드는 서로 상호 보완적인 특질이 있다. 만약 아래 두 코드에 둘레 길이를 구하는 perimenter() 라는 함수를 추가한다고 했을 때, 각각은 아래와 같이 장단점이 있다.
* 절차적인 코드 : 기존 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다. 반면, 새로운 자료 구조를 추가하기 어렵다. 그러려면 모든 함수를 고쳐야 한다.
```
public class Square {
  ...
}

public class Rectangle {
  ...
}

public class Circle {
  ...
}

public class Geometry {
  public final double PI = 3.141;

  public double area(Object shape) throws NoSuchShapeExcption {
    if (shape instanceof Square) {
      ...
    }
    else if (shape instanceof Rectangle) {
      ...
    }
    else if (shape instanceof Circle) {
      ...
    }

    throw new NoSuchShapeExcption();
  }
}
```
* 객체 지향적인 코드 : 기존 함수를 변경하지 않으면서 새 클래스를 추가하기 쉽다. 반면, 새로운 함수를 추가하기 어렵다. 그러러면 모든 클래스를 고쳐야 한다.
```
public class Square implements Shape {
  ...
  public double area() {
    ...
  }
}

public class Rectangle implements Shape {
  ...
  public double area() {
    ...
  }
}

public class Circle implements Shape {
  ...
  public double area() {
    ...
  }
}
```
결국, 모든 함수를 고치냐(절차적인 코드) VS 모든 클래스를 고치냐(객체 지향 코드)의 문제가 된다. 객체 지향 코드에서 어려운 변경은 절차적인 코드에서 쉬우며, 절차적인 코드에서 어려운 변경은 객체 지향 코드에서 쉽다.

* 클래스와 객체 지향 기법
  * 새로운 함수가 아니라 새로운 자료 타입이 필요한 경우
* 절차적 코드와 자료 구조
  * 새로운 자료 타입이 아니라 새로운 함수가 필요한 경우

모든 것을 객체로 구현하려는 생각을 버리자.

## 디미터 법칙
모듈은 자신이 조작하는 개체의 속사정을 몰라야 한다는 법칙이다. 객체에서 허용된 메서드가 반환하는 객체의 메서드는 호출하면 안된다. 예를 들어, 아래와 같이 기차 충돌을 하면 안된다.
```
# 임시 디렉토리의 절대 경로를 얻는 코드임
String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```
위와 같은 코드는 일반적으로 조잡하다 여겨지는 방식이므로 피하는 것이 좋다. 따라서, 아래와 같이 나누는 편이 좋다.
```
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```
하지만, 이 역시도 ctxt 객체가 Options를 포함하며, 그 것이 ScratchDir를, 그리고 그것이 AbsolutePath를 포함한다는 사실을 안다. 함수 하나가 아는 지식이 굉장히 많다. 구조에 따라 디미터 법칙은 위반하는 지 알 수 있다.
* ctxt, Options, ScratchDir가 객체라면 : 내부 구조를 숨겨야 하므로 디미터 법칙을 위반
* ctxt, Options, ScratchDir가 자료 구조라면 : 내부 구조를 노출시켜야 하므로 디미터 법칙을 위반하지 않음

아래와 같이 구현했다면 디미터 법칙을 거론할 필요가 없어진다.
```
final String outputDir = ctxt.options.scratchDir.absolutePath;
```
자료 구조는 무조건 함수 없이 공개 변수만 포함하고 객체는 비공개 변수와 공개 함수를 포함한다면, 문제는 훨씬 간단해진다.

* 잡종 구조 : 절반은 객체, 절반은 자료 구조
  * 새로운 함수, 새로운 자료 구조 둘 다 추가하기 어려운 구조
  * 프로그래머가 함수나 타입을 보호할지 공개할지 확인하지 못해 어중간하게 설계해서 생긴 구조

그렇다면, 기차 충돌도 하지 않고 디미터 법칙을 위반하지 않도록 앞의 코드를 수정하려면 어떻게 해야 할까? 아래는 나쁜 예이다.
```
# ctxt 객체에 공개해야 하는 메서드가 너무 많음
ctxt.getAbsoluePathOfScratchDirectoryOptions();
# getScratchDirectoryOptions()이 객체가 아니라 자료 주고를 반환한다는 가정임
ctxt.getScratchDirectoryOptions().getAbsolutePath()
```
ctxt가 객체라면 뭔가를 하라고 말해야지 속을 드러내라고 하면 안된다. 임시 디렉토리가 왜 필요한지, 무엇을 위한 객체인지 전체 코드를 살펴보면 아래와 같이 임시 파일을 생성하기 위한 목적이라는 사실이 드러난다.
```
String outFile = outputDir + "/" + className.replace('.', '/') + ".class";
FileOutputStream fout = new FileOutputStream(ourFile);
BufferedOutputStream bos = new BufferedOutputStream(fout);
```
그리고 위와 같은 코드가 추상화 수준을 뒤섞어 놓고 점, 슬래시, 파일 확장자, File 객체를 부주의하게 마구 뒤섞여 있다는 것을 알게 되었다. 이 것을 ctxt 안에 감싸서 ctxt 객체에 임시 파일을 생성하라고 시키면 어떨까?
```
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```
이렇게 되면 ctxt는 내부 구조를 드러내지 않으며, 모듈에서 해당 함수는 자신이 몰라야 하는 여러 객체를 탐색할 필요가 없다. 따라서 디미터 법칙을 위반하지 않는다.

## 결론
우수한 소프트웨어 개발자는 편견 없이 이 사실을 이해해 직면한 문제에 최적인 해결책을 선택한다.
* 객체 : 동작을 공개하고 자료를 숨긴다
  * 장점 : 기존 동작을 변경하지 않으면서 새 객체 타입을 추가하기 쉼다
  * 단점 : 기존 객체에 새 동작을 추가하기는 어렵다
  * 활용 : 새로운 **자료 타입**을 추가하는 유연성이 필요한 경우
* 자료 구조(or 절차적인 코드) : 별다른 동작없이 자료를 노출한다
  * 장점 : 기존 자료 구조에 새 동작을 추가하기 쉽다
  * 단점 : 기존 함수에 새 자료 구조를 추가하기 어렵다
  * 활용 : 새로운 **동작**을 추가하는 유연성이 필요한 경우


---


## Previous
'[클린 코드 리뷰] 형식 맞추기 5장' -> [Next](https://akfmdl.github.io//programming_clean_code_5/){: .btn}

## Next
'[클린 코드 리뷰] 오류 처리 7장' -> [Next](https://akfmdl.github.io//programming_clean_code_7/){: .btn}