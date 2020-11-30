# Chapter 8 경계
- 오픈 소스, 패키지 등의 외부 코드와의 경계를 깔끔하게 처리하는 기법과 기교

## 1 외부 코드 사용
- 아래 코드는 Map이 반환하는 Object를 올바른 유형으로 변환할 책임이 클라이언트에게 있다.
```java
Map sensors = new HashMap();
Sensor s = (Sensor)sensors.get(sensorID);
```
- Generic을 사용하여 코드 가독성은 높였으나, `Map<Sensor>`는 사용자에게 필요하지 않은 기능까지 제공한다.
```java
Map<Sensor> sensors = new HashMap<Sensor>();
Sensor s = (Sensor)sensors.get(sensorID);
```
- 경계 인터페이스인 `Map`은 `Sensors`안으로 숨겨, `Map` 인터페이스가 변하더라도 나머지 프로그램에 영향을 미치지 않으며 제네릭 사용 여부는 `Sensors`안에서 결정한다.
```java
public class Sensors {
    private Map sensors = new HashMap();
    public Sensor getByID(String id) {
        return (Sensor) sensors.get(id);
    }
}
```

## 2 경계 살피고 익히기
- 학습 테스트`BeckTDD`로 간단한 테스트 케이스를 작성해 외부 코드를 익힌다

## 3 log4j 익히기
- `log4j`: 아파치의 로깅 기능

## 4 학습 테스트는 공짜 이상
- 이해가 높아짐
- 예상대로 도는지 검증, 새 버전이 호환되는지 확인 -> 새 패키지로 업데이트하기 쉬움

## 6 클린 경계
- 우수한 소프트웨어 설계는 변경을 위해 많은 투자와 재작업이 필요하지 않다
- 경계에 위치하는 코드는 분리하며, 기대치를 정의하는 테스트 케이스도 작성한다.
- 외부 패키지를 호출하는 코드를 가능한 줄여 경계를 관리하자.
    - 새로운 클래스로 경계를 감싸거나
    - 어댑터 패턴을 사용한다
