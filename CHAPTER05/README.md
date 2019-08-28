# CHAPTER 05 연산자

스위프트 연산자는 특정한 문자로 표현한 함수이고 특정 연산자의 역할을 커스텀 할 수 있음  
연산자는 연산 되는 `값의 수`와 `연산자의 위치`로 구분

|분류|설명|예|
|-|-|-|
|단항 연산자|피연산자가 1개인 연산자|!A|
|이상 연산자|피연산자가 2개인 연산자|A + B|
|삼항 연산자|피연산자가 3개인 연산자|A ? B : C|
|전위 연산자|연산자가 피연산자 앞에 위치|!A|
|중위 연산자|연산자가 피연산자 사이에 위치|A + B|
|후위 연산자|연산자가 피연산자 뒤에 위치|A!|

### NOTE_ 띄어쓰기 주의
```swift
스위프트에서 띄어쓰기에 따라 연산자의 의미가 달라진다.
A! == B와 A !== B는 다르다.
```
## 5.1 연산자의 종류

### 5.1.1 할당 연산자
값을 할당할 때 사용
|연산자|부호|설명|
|-|-|-|
|할당(대입) 연산자|A = B|A에 B의 값을 할당합니다. 데이터 타입이 맞지 않으면 에러 발생|
### 5.1.2 산술 연산자
수학에서 쓰이는 연산자와 같은 역할
|연산자|부호|설명|
|-|-|-|
|더하기 연산자|A + B|A와 B를 더한 값을 반환|
|빼기 연산자|A - B|A와 B를 뺀 값을 반환|
|곱하기 연산자|A * B|A와 B를 곱한 값을 반환|
|나누기 연산자|A / B|A와 B를 나눈 값을 반환|
|나머지 연산자|A % B|A와 B를 나눈 나머지 값을 반환|

### NOTE_ 부동소수점 나머지 연산
```swift
스위프트는 부동소수점 타입의 나머지 연산 지원
let number: Double = 5.0
var result: Double = number.truncatingRemainder(dividingBy: 1.5) // 0.5
result = 12.truncatingRemainder(dividingBy: 2.5) // 2.0
```
### NOTE_ 엄격한 데이터 타입
```swift
서로 다른 자료형끼리의 연산을 하려면 같은 타입으로 변환 후 연산해야 함
같은 정수 타입인 Int, UInt 도 같은 타입으로 변환 해야 함

let num1: Int = 4
let num2: UInt = 5
let num3 = num1 + num2
위 코드와 같이 다른 타입으로 진행 한다면 아래와 같은 에러 발생 
error: '+' is unavailable: Please use explicit type conversions or Strideable methods for mixed-type arithmetics.
```
### 5.1.3 비교 연산자
두 값을 비교할 때 사용  
Bool 값을 리턴
|연산자|부호|설명|
|-|-|-|
|값이 같다|A == B|같은 값인지 비교|
|값이 같지 않다|A != B|다른 값인지 비교|
|값이 크거나 같다|A >= B|크거나 같은 값인지 비교|
|값이 작거나 같다|A <= B|작거나 같은 값인지 비교|
|값이 크다|A > B|큰 값인지 비교|
|값이 작다|A < B|작은 값인지 비교|
|참조가 같다|A === B|인스턴스가 같은지 비교|
|참조가 같지 않다|A !== B|인스턴스가 다른지 비교|
|[패턴 매치](https://zeddios.tistory.com/274)|A ~= B|패턴이 매치되는지 확인|
### NOTE_ 참조 비교 연산자
기본 데이터 타입은 모두 구조체로 구현되어있고 값 타입이기 때문에 값의 비교 연산자인 `==`를 사용하고 클래스의 인스턴스인 경우에만 `===`를 사용
```swift
let valueA: Int = 3
let valueB: Int = 5
let valueC: Int = 5

let isSameValueAB: Bool = valueA == valueB // false
let isSameValueBC: Bool = valueB == valueC // true

class SomeClass {}

let referenceA: SomeClass = SomeClass()
let referenceB: SomeClass = SomeClass()
let referenceC: SomeClass = referenceB

let isSameReferenceAB: Bool = referenceA === referenceB // false
let isSameReferenceBC: Bool = referenceB === referenceC // true
```
### 5.1.4 삼항 조건 연산자
피연산자가 3개인 연산자
|연산자|부호|설명|
|-|-|-|
|삼항 조건 연산자|Question ? A : B|Question(Bool)값이 참이면 A, 거짓이면 B를 리턴|
```swift
var valueA: Int = 3
var valueB: Int = 5
var biggerValue: Int = valueA > valueB ? valueA : valueB // 5
```
### 5.1.5 범위 연산자
값(수)의 범위를 나타낼 때 사용
|연산자|부호|설명
|-|-|-|
|폐쇄 범위 연산자|A...B|A이상 B이하의 범위|
|반폐쇄 범위 연산자|A..<B|A이상 B미만의 범위|
|단방향 범위 연산자-1|A...|A이상의 수|
|단방향 범위 연산자-2|...A|A이하의 수|
|단방향 범위 연산자-3|..<A|A 미만의 수|
>__초과는 없다__
### 5.1.6 부울 연산자

### 5.1.7 비트 연산자

### 5.1.8 복합 할당 연산자

### 5.1.9 오버플로 연산자

### 5.1.10 기타 연산자

## 5.2 연산자 우선순위와 결합방향

## 5.3 사용자정의 연산자

### 5.3.1 전위 연산자 정의와 구현

### 5.3.2 후위 연산자 정의와 구현

### 5.3.3 중위 연산자 정의와 구현