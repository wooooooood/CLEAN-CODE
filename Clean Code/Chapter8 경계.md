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
