# Chapter 11 시스템
### 1 도시를 세운다면?
- 적절한 추상화와 모듈화가 필요
- 높은 추상화 수준, 즉 시스템 수준에서도 깨끗함을 유지하자

### 2 시스템 제작과 시스템 사용을 분리하라
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

**팩토리**
- 때로는 객체가 생성되는 시점을 응용이 결정할 필요도 생긴다. 이때는 추상 팩토리 패턴을 사용한다.

**의존성 주입 Dependency Injection (DI)**
- 사용과 제작을 분리
- 제어 역전(Inversion of Control)기법을 의존성 관리에 적용한 것이며, 제어 역전에서는 한 객체가 맡은 보조 책임을 새로운 객체에게 전적으로 떠넘긴다. 새로운 객체는 넘겨받은 책임만 맡으므로 `단일 책임 원칙 (Single Responsibility Principle)`을 지키게 된다.

### 3 확장
- 반복적이고 점진적인 애자일 방식의 핵심은: 오늘 주어진 사용자 스토리에 맞춰 시스템을 구현하고 내일은 새로운 스토리에 맞춰 시스템을 조정하고 확장한다.
- TDD, 리팩토링을 통한 클린 코드는 코드 수준에서 시스템을 조정하고 확장하기 쉽게 만든다.
- 관심사를 적절히 분리해서 관리한다면 소프트웨어 아키텍처는 점진적으로 발전할 수 있다.
- 비즈니스 논리가 큰 컨테이너와 밀접하게 연결되면 독자적인 단위 테스트가 어렵다.

**횡단 관심사**  
- 영속성과 같은 관심사는 응용 프로그램의 자연스러운 객체 경계를 넘나드는 경향이 있다.
- 모든 객체가 전반적으로 동일한 방식을 이용하게 해야 한다. (DBMS, 명명 관례 등)

`관점 지향 프로그래밍 Aspect-Oriented Programming (AOP)`: 횡단 관심사에 대처해 모듈성을 확보하는 일반적인 방법론. 관점(Aspect)이라는 모듈 구성 개념은 "특정 관심사를 지원하려면 시스템에서 특정 지점들이 동작하는 방식을 일관적으로 바꿔야 한다"고 명시한다.

### 4 자바 프록시
- 단순한 상황에 적합

### 5 순수 자바 AOP 프레임워크

### 6 AspectJ 관점
- 언어 차원에서 관점을 모듈화 수단으로 지원하는 자바 언어 확장

### 7 시스템 아키텍처 시운전
최선의 시스템 구조는 각기 다른 POJO(Plain-Old Java Object)객체로 구현되는 모듈화된 관심사 영역(도메인)으로 구성된다. 이 서로 다른 영역은 해당 영역 코드에 최소한의 영향을 미치는 관점이나 유사한 도구를 사용해 통합된다. 이런 구조는 해당 코드 자체처럼 동일하게 시운전이 가능해진다.

### 8 의사 결정을 최적화하라
- 가장 적합한 사람에게 책임을 맡긴다.
- 때로는 최대한의 정보를 모아 최선의 결정을 내리기 위해 가능한 마지막 순간까지 결정을 미룰 수 있다.

### 9 명백한 가치가 있을 때 표준을 현명하게 사용하라
- 때로는 표준을 만드는 시간이 너무 오래 걸리거나 표준을 제정한 목적을 잊기도 한다.

### 10 시스템은 도메인 특화 언어가 필요하다
- 좋은 `DSL(Domain-Specific Language)`은 도메인 개념과 그 개념을 구현한 코드 사이의 의사소통 간극을 줄여준다.

### 11 결론
- 시스템 역시 깨끗해야 한다.
- 모든 추상화 단계에서 의도는 명확히 표현한다.
