# Chapter 2 의미있는 이름

## 2
- 변수 / 클래스 이름: 존재 이유? 수행 기능? 사용 방법?

## 3
- 컨테이너가 실제로 `List`가 아닌 경우 `somthingList`라고 이름짓지 않는다
- 비슷한 이름을 사용하지 않는다
- 변수 이름 `l`, `O` 는 끔찍하다

## 4
- 읽는 사람이 차이를 알도록 이름짓기 (`Customer` 과 `CustomerObject`에는 차이가 없다)

## 5
- 발음하기 쉬운 이름 (의미없는 축약X)

## 6
- 변수 / 상수를 코드 여러 곳에서 사용한다면 검색하기 쉬운 이름으로 (변수 이름이 `e`라면?)

## 7
- 헝가리식 표기법, 접두어(`m_`) 등등은 이제 필요없다.
- 인터페이스, 구현 클래스의 이름도 적절하게 짓기
    - 저자의 경우 클래스가 인터페이스라는 사실을 알릴 필요가 없다고 생각해 `ShapeFactory`, `CShapeFactory`/`ShapeFactoryImp`

## 8
- 일반적으로 사용하지 않는 이름은 피하기
- 루프 반복 횟수 변수는 전통적으로 한 글자를 사용했지만 (`i`, `j`, `k`은 괜찮지만 `l`은 절대안됨) 보통 문자 하나를 사용하는 변수 이름은 문제가 있다

## 9 클래스 이름
- 클래스, 객체 이름은 명사나 명사구 (`Customer`, `Account`, `AddressParser`)
- `Manager`, `Processor` 등은 피하고 동사는 사용하지 않는다

## 10 메소드 이름
- 동사나 동사구 (`deletePayment`)
- 접근자Accessor, 변경자Mutator, 조건자Predicate는 javabean표준에 따라 값 앞에 `get`, `set`, `is`를 붙인다
- constructor을 overload할때는 정적 팩토리 메소드를 사용하며, 메소드는 인수를 설명하는 이름.
```
Complex fulcrumPoint = Complex.FromRealNumber(23.0) //better
Complex fulcrumPoint = new Complex(23.0)
```

## 11
- 기발한, 재미있는 이름보다 명확한 이름을 정한다. (`kill()` 대신 `whack()`이라고 쓰지 않는다)

## 12 개념 하나에 단어 하나를 사용
- 똑같은 메소드를 클래스마다 `fetch`, `retrieve`, `get` 이라고 제각각 부르지 않는다
- 동일한 코드 기반에 `controller`, `manager`, `driver`을 섞어쓰지 않는다
- 일관성

## 13
- 한 단어를 두가지 목적으로 사용하지 않는다 (ex. 두개를 더하는 경우 `add`, 추가하는 경우 `insert` 또는 `append`)

## 14 해법 영역에서 사용하는 이름
- 기술적인 개념에는 기술적인 이름

## 15
- 문제 영역 개념과 관련이 깊다면 문제 영역과 관련있는 이름

## 16 의미 있는 맥락
- `zipCode`, `state`, `street`, `country` .. 에서의 `state`와, 단순한 변수 `state`는 다르게 느껴진다.
- `zipCode`, `state`, `street`, `country`를 `class Address` 에 넣는다면 전체적인 의미가 더욱 분명해진다.

## 17 불필요한 맥락 없애기
- `Address`는 클래스 이름으로 적합하다.
- `accountAddress`와 `customerAddress`는 `Address` 클래스 인스턴스로는 괜찮으나 클래스 이름으로는 부적합
