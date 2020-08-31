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
