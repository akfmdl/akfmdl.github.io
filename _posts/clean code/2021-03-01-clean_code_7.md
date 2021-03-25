---
layout: post
title:  "[클린 코드 리뷰] 오류 처리 7장"
date:   2021-03-01
excerpt: "clean code"
feature: https://media.vlpt.us/images/jwkim/post/9a8598d3-44c6-419d-b509-069370dd5c7e/%EA%B7%B8%EB%A6%BC3.png
tag:
- CLEAN CODE
comments: true
---

로버트 C.마틴의 클린 코드를 읽고 정리한 포스트입니다.

## 오류 코드보다 예외를 사용하라
여기저기 흩어진 오류 처리 코드 때문에 실제 코드가 하는 일을 파악하기 어렵게 만들면 안된다. 오류 플래그를 설정하거나 호출자에게 오류 코드를 반환하는 것이 그 안 좋은 예이다. 오류가 생기면 예외를 던지는 편이 낫다.
* 코드를 복잡하게 만드는 안 좋은 예

```
public class DeviceController {
  ...
  public void sendShutDown() {
    ...
    // 디바이스 상태를 점검한다.
    if (handle != DeviceHandle.INVALID){
      ...
    }
    // 디바이스가 일시정지 상태가 아니라면 종료한다.
    if (record.getStatus() != DEVICE_SUSPENDED)
    {
      ...
    }
    else {
      ...
    }
  }
}
```

* 오류를 발견하면 예외를 던지는 코드 -> 코드가 확실히 깨끗해졌다는 것을 알 수 있다

```
public class DeviceController {
  ...
  public void sendShutDown() {
    try {
      tryToShutDown();
    } catch (DeviceShutDownError e){
      logger.log(e);
    }
  }

  private void tryToShutDown() throws DeviceShutDownError {
    ...
  }
}
```

## Try-Catch-Finally 문부터 작성하라
try 블록은 어느 시점에서든 실행이 중단된 후 catch 블록으로 넘어갈 수 있다. 어떤 면에서 트랜잭션과 비슷하다. try 블록에서 무슨 일이 생기든지 catch 블록은 프로그램 상태를 일관성 있게 유지해야 한다. 그러므로 예외가 발생할 코드를 짤 때는 try-catch-finally 문으로 시작하는 편이 낫다. 그러면 try 블록에서 무슨 일이 생기든지 호출자가 기대하는 상태를 정의하기 쉬워진다.

먼저 강제로 예외를 일으키는 테스트 케이스를 작성한 후 테스트를 통과하게 코드를 작성하는 방법을 권장한다. 그러면 자연스럽게 try 블록의 트랜잭션 범위부터 구현하게 되므로 범위 내에서 트랜잭션 본질을 유지하기 쉬워진다.

## 미확인 예외를 사용하라
* 메서드가 반환할 모든 예외를 열거하는 방식 : 옛날 방식으로, 선언된 에러들도 실제로 일어날 수 있는 에러의 일부에 불과함
* 확인된 예외도 유용하지만 일반적으로 의존성이라는 비용이 발생한다
  * 하위 함수를 변경해 새로운 오류를 던진다고 가정할 경우, 이 함수를 호출하는 함수 모두가 catch 블록에서 새로운 예외를 처리하거나 선언부에 throw 절을 추가해야 한다
  * 최하위 단계에서 최상위까지 연쇄적인 수정이 일어난다
  * throws 경로에 위치하는 모든 함수가 최하위 함수에서 던지는 예외를 알아야 하므로 캡슐화도 깨진다

## 예외에 의미를 제공하라
* 호출 스택만으로 실패한 코드의 의도를 파악하기 힘들다
* 오류 메세지에 정보를 담아 예외와 함께 던진다
  * 실패한 연산 이름과 실패 유형 등
* 로깅 기능을 사용할 경우, catch 블록에서 오류를 기록하도록 충분한 정보를 넘겨준다

## 호출자를 고려해 예외 클래스를 정의하라
* 오류를 분류하는 방법은 수없이 많다
  * 컴포넌트로 분류하거나 유형으로 분류
  * 예) 디바이스 실패, 네트워크 실패, 프로그래밍 오류 등
* 오류를 정의할 때 가장 중요한 것은 오류를 잡아내는 방법이 되어야 한다

발생할 모든 유형을 기록하면 catch문의 중복으로 코드는 상당히 길어지게 된다.

```
ACMEPort port = new ACMEPort(12);

try {
  port.open();
} catch (DeviceResponseException e){
  reportPortError(e);
} catch (ATM1212UnlockedException e) {
  reportPortError(e);
} catch (GMXError e){
  reportPortError(e);
} finally {
  ...
}
```

위 코드는 아래와 같이 API로 감싸면 예외 유형 하나만 반환시키도록 구현할 수 있다.

```
LocalPort port = new LocalPort(12);

try {
  port.open();
} catch (PortDeviceFailure e){
  reportPortError(e);
} finally {
  ...
}
```

LocalPort는 단순히 ACMEPort가 던지는 예외를 잡아 변환하는 감싸기(Wrapper) 클래스일 뿐이다

```
public class LocalPort {
  private ACMEPort innerPost;

  public LocalPort(int portNumber) {
    innerPort = new ACMEPort(portNumber)
  }

  public void open() {
    try {
      innerport.open();
    } catch (DeviceResponseException e){
      throw new PortDeviceFailure(e);
    } catch (ATM1212UnlockedException e) {
      throw new PortDeviceFailure(e);
    } catch (GMXError e){
      throw new PortDeviceFailure(e);
    }
  }
}
```

이처럼 감싸기(Wrapper) 클래스는 매우 유용하다. 실제로 외부 API를 사용하면 다음과 같은 장점이 있다.
* 외부 API와의 의존성이 줄어든다
* 다른 API로 갈아타는 비용이 적다
* 외부 API를 직접 호출하는 대신, 테스트 코드를 넣어주는 방법으로 프로그램을 테스트하기도 쉬워진다
* 외부 API의 설계 방식에 발목 잡히지 않는다

## 정상 흐름을 정의하라
다음은 비용의 총계를 계산하는 코드이다. 식비를 비용으로 청구했다면 직원이 청구한 식비를 총계에 더하고, 그렇지 않다면 일일 기본 식비를 총계에 더한다. 그런데 이것을 catch문 안에 넣어서 논리를 따라가기 어렵게 만든다.

```
try {
  MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
  m_total += expenses.getTotal();
} catch(MealExpensesNotFound e) {
  m_total += getMealPerDiem();
}
```

expenseReportDAO를 고쳐 언제나 getMealPerDiem 객체를 반환하게 만들고 청구한 식비가 없다면 일일 기본 식비를 반환하게 한다면 코드를 더 간결하게 만들 수 있다.

```
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
m_total += expenses.getTotal();

public class perDiemMealExpenses implements MealExpenses {
  public int getTotal() {
    // 기본값으로 일일 기본 식비를 반환한다.
  }
}
```

이를 특수 사례 패턴(Special case pattern)이라 부른다. 클래스를 만들거나 객체를 조작해 특수 사례를 처리하는 방식이다. 클래스나 객체가 예외적인 상황을 캡슐화해서 처리하므로 클라이언트 코드가 예외적인 상황을 고려할 필요가 없어진다.

## null을 반환하지 마라
null을 반환하는 코드는 일거리를 늘릴 뿐만 아니라 호출자에게 문제를 떠넘긴다. 누구 하나라도 null 확인을 빼먹는다면 애플리케이션이 통제 불능에 빠질지도 모른다.

```
public void registerItem(Item item) {
  if (item != null) {
    ItemRegistry registry = peristentStore.getItemRegistry();
    if (registry != null) {
      Item existing = registry.getItem(item.getID());
      if (existing.getBillingPeriod().hasRetailOwner()) {
        existing.register(item);
      }
    }
  }
}
```

위와 같은 애플리케이션에서 날린 NullPointer Exception을 어떻게 처리할지 상상해보라. 위 코드는 null 확인이 너무 많아 문제다.

메서드에서 null을 반환하고픈 유혹이 든다면 그 대신 예외를 던지거나 특수 사례 객체를 반환한다. 외부 API가 null을 반환한다면 감싸기 메서드를 구현해 예외를 던지거나 특수 사례 객체를 반환하는 방식을 고려한다.

* 특수 사례 객체를 반환하는 방식의 예

null 반환을 허용하는 리스트를 사용하는 나쁜 예

```
List<Employee> employees = getEmployees();
if (employees != null) {
  for (Employee e : employees) {
    totalPay += e.getPay();
  }
}
```

getEmployees를 변경해 null 대신 빈 리스트를 반환한다면 코드가 훨씬 깔끔해질뿐더러 NullPointerException이 발생할 가능성도 줄어든다.

```
List<Employee> employees = getEmployees();
for (Employee e : employees) {
  totalPay += e.getPay();
}

public List<Employee> getEmployees() {
  if (.. 직원이 없다면 ..)
    return Collections.emptyList();
}
```

## null을 전달하지 마라
정상적인 인수로 null을 기대하는 API가 아니라면 메서드로 null을 전달하는 코드는 최대한 피한다. 아래 두 case 모두 간결성도 해칠 뿐만 아니라 누군가 null을 전달하면 여전히 실행을 하지 못한다. 결국, 호출자가 실수로 null을 넘기면 적절히 처리하는 방법이 없다. 애초에 null을 넘기지 못하도록 프로그래머들끼리 정책을 확립해야 한다.

```
if (variable != null)
혹은
assert variable != null : "variable should not be null";
```

---


## Previous
'[클린 코드 리뷰] 객체와 자료 구조 6장' -> [Next](https://akfmdl.github.io//programming_clean_code_6/){: .btn}

## Next
'[클린 코드 리뷰] 경계 8장' -> [Next](https://akfmdl.github.io//programming_clean_code_8/){: .btn}