# Chapter 3 함수

## 1
- 함수는 작게 만들어라
- 함수 내 들여쓰기는 2단을 넘지 마라

## 2
- 함수는 한 가지 작업만 해야한다
- 함수 이름 아래에서 추상화 수준이 하나인 단계만 수행하는 것이 한 가지 작업

## 3
- 함수 당 추상화 수준은 하나로
```java
//세 가지 추상화 수준. 아래로 갈수록 낮은 수준
//1
getHTML();
//2
String pagePathName = PathParser.render(pagePath);
//3
.append("\n");
```

## 4
- `switch`문을 저차원 클래스에 숨기고 반복하지 않는 법: 다형성 polymorphism 사용
```java
switch (employee.type){
    case Commissioned:
        return calculateCommissionedPay(employee);
    case Hourly:
        return calculateHourlyPay(employee);
    // ...
}
```
```java
public abstract class Employee {
    public abstract boolean isPayDay();
    //...
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r)
        throws ..
}

public class EmployeeFactoryEmpl implements EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r)
        throws .. {
        switch (employee.type ){
            case Commissioned:
                return new CommissionedEmployee(employee);
            case Hourly:
                return new HourlyEmployee(employee);
            // ...
        }
    }
}
```

## 5
- 서술적인 이름 사용 ex. `includeSetupAndTeardownPages`

## 6 함수 인수
- 이상적으로는 0개, 3개 이상은 가능한 피하라
- 단항 함수 형식 예시: 이벤트
- 입력 인수를 변환하는 함수라면 변환 결과는 반환 값으로 돌려준다
- 플래그 인수는 추하다
- 인수가 2~3개 필요하다면 일부를 독자적인 클래스 변수로 선언할 가능성이 있다 ex. `makeCircle(double x, double y, double radius)` -> `makeCircle(Point center, double radius)`  
  이 경우 결국 묶은 변수에 이름을 붙이게 되므로 개념을 표현하게 된다
- 단항 함수는 함수와 인수가 동사/명사 쌍을 이뤄야 한다.  
  ex. `write(name)`
  ex2. `writeField(name)` name이 field임을 알 수 있어 좀 더 낫다
  ex3. `assertExpectedEqualsActual(expected, actual)` 인수 순서를 기억할 필요가 없다

## 7 부수 효과를 일으키지 마라
- ex. `CheckPassword` 함수 안에서 `Session.initialize()` 하지마라
- 출력 인수는 피한다. 함수에서 뭔가의 상태를 변경해야 한다면 함수가 속하는 객체의 상태를 변경해라.  
  ex. `appendFooter(report)` 말고 `report.appendFooter()`

## 8 명령과 조회를 분리
- 함수는 뭔가 수행하거나, 뭔가에 답하거나 둘 중 하나만 한다
```java
set("userName", "X"); //set 해라 인가?
if (set("userName", "X"));  //set 되었는지 확인하는건가?
```
``` js
if (attributeExists("userName"))
    setAttribute("userName", "X");  //set해라 라는 의미가 더 명확하다
```

## 9 오류 코드보다 예외를 사용
- 명령 함수에서 오류 코드를 반환하멘 호출자는 오류 코드를 곧바로 처리해야 한다.
```java
if (deletePage(page) == OK) {
    if (registry.deleteReference(page.name) == OK){
        if (configKeys.deleteKey(page.key)){

        } else {

        }
    } else {

    }
} else {

}
```
```java
try{
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.key);
} catch (Exception e) {

}
```
- 오류 코드를 반환한다는 것은 어디선가 `enum`으로 관리되고 있다는 것. 오류 코드 대신 예외를 사용하면 새 예외는 `Exception` 클래스에서 파생되므로 재컴파일/재배치 없이 새 예외 클래스를 추가할 수 있다

## 10 반복하지 마라

## 11
- `goto`는 큰 함수에서만 의미가 있으므로 피해라

## 12 함수 짜는 방법
- 막 만든다 -> 단위 테스트 케이스를 만들어 통과시킨다 -> 코드 다듬고 함수 만들고 이름 바꾸고 중복 제거하고 순서 바꾸고 클래스 쪼개고.. 하는 와중에도 테스트를 통과한다
