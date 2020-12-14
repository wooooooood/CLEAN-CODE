# Chapter 11 시스템
## 1 도시를 세운다면?
- 적절한 추상화와 모듈화가 필요
- 높은 추상화 수준, 즉 시스템 수준에서도 깨끗함을 유지하자

## 2 시스템 제작과 시스템 사용을 분리하라
- 소프트웨어 시스템은 (응용 프로그램 객체를 제작하고 의존성을 서로 '연결'하는) 시작 단계와 (시작 단계 이후에 이어지는) 실행 단계를 분리해야 한다.
- 시작 단계라는 관심사를 분리하자.
  - Ex. `초기화 지연`(Lay Initialization) / `계산 지연`(Lazy Evaluation)
    - 장점: 실제로 필요할 때까지 객체를 생성하지 않으므로 불필요한 부하가 걸리지 않아 응용 프로그램을 시작하는 시간이 그만큼 빨라진다, 어떤 경우에도 null포인터를 반환하지 않는다.
    - 단점: getService()가 MyServiceImpl()에 의존한다, 단일 책임 원칙(SRP)을 깬다(테스트가 어렵다), MyServiceImpl()이 모든 상황에 적합한 객체인지 알 수 없다.
```java
public Service getService(){
  if (service == null)
    service = new MyServiceImpl();
  return service;
}
```
- 설정 논리는 일반 실행 논리와 분리해야 모듈성이 높아진다.
