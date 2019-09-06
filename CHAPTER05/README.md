# CHAPTER 05 연산자 

스위프트 연산자는 특정한 문자로 표현한 함수이고 특정 연산자의 역할을 커스텀 할 수 있음  
연산자는 연산 되는 `값의 수`와 `연산자의 위치`로 구분

|분류|설명|예|
|-|-|-|
|단항 연산자|피연산자가 1개인 연산자|!A|
|이항 연산자|피연산자가 2개인 연산자|A + B|
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

|연산자|부호|설명|
|-|-|-|
|폐쇄 범위 연산자|A...B|A이상 B이하의 범위|
|반폐쇄 범위 연산자|A..<B|A이상 B미만의 범위|
|단방향 범위 연산자-1|A...|A이상의 수|
|단방향 범위 연산자-2|...A|A이하의 수|
|단방향 범위 연산자-3|..<A|A 미만의 수|

>__초과는 없다__
### 5.1.6 부울 연산자
Bool 연산 할 때 사용

|연산자|부호|설명|
|-|-|-|
|NOT 부울 연산자|!B|Bool 값을 반전|
|AND 부울 연산자|A && B|AND 논리 연산|
|OR 부울 연산자|A \|\| B|OR 논리 연산|

### 5.1.7 비트 연산자
값의 비트 논리 연산 할 때 사용

|연산자|부호|설명|
|-|-|-|
|NOT 비트 연산자|~A|A의 비트를 반전|
|AND 비트 연산자|A & B|A와 B의 비트를 AND 논리 연산|
|OR 비트 연산자|A \| B|A와 B의 비트를 OR 논리 연산|
|XOR 비트 연산자|A ^ B|A와 B의 비트를 XOR 논리 연산|
|시프트 연산자|A >> B / A << B|A의 비트를 B만큼 시프트 연산|

### 5.1.8 복합 할당 연산자
다른연산자와 할당 연산자가 결합 된 연산자

|표현|설명|같은 표현|
|-|-|-|
|A += B|A와 B의 합을 A에 할당합니다|A = A + B|
|A -= B|A와 B의 차를 A에 할당합니다|A = A - B|
|A *= B|A와 B의 곱을 A에 할당합니다|A = A * B|
|A /= B|A와 B의 몫을 A에 할당합니다|A = A / B|
|A %= B|A와 B의 나머지를 A에 할당합니다|A = A % B|
|A <<= N|A를 N만큼 왼쪽 비트 시프트 한 값을 A에 할당합니다|A = A << B|
|A >>= N|A를 N만큼 오른쪽 비트 시프트 한 값을 A에 할당합니다|A = A >> B|
|A &= B|A와 B의 AND 비트 연산 결과를 A에 할당합니다|A = A & B|
|A \|= B|A와 B의 OR 비트 연산 결과를 A에 할당합니다|A = A \| B|
|A ^= B|A와 B의 XOR 비트 연산 결과를 A에 할당합니다|A = A ^ B|

### 5.1.9 오버플로 연산자
기본 연산자로 값의 범위를 벗어나면 아래와 같은 에러가 발생
```swift
error: arithmetic operation '2147483647 + 1' (on type 'Int32') results in an overflow
var num = Int32.max + 1
```
에러가 발생하지않고 오버플로가 될 수 있게 하는 연산자

|연산자|부호|설명|
|-|-|-|
|오버플로 더하기 연산|&+|오버플로에 대비한 덧셈 연산|
|오버플로 빼기 연산|&-|오버플로에 대비한 빼기 연산|
|오버플로 곱하기 연산|&*|오버플로에 대비한 곱하기 연산|

```swift
var unsignedInteger: UInt8 = 0
let errorUnderflowResult: UInt8 = unsignedInteger - 1 // 런타임 오류
let underflowedValue: UInt8 = unsignedInteger &- 1 // 255

unsignedInteger = UInt8.max
let errorOverflowResult: UInt8 = unsignedInteger + 1 // 런타임 오류
let overflowedValue: UInt8 = unsignedInteger &+ 1 // 0
```
### 5.1.10 기타 연산자

|연산자|부호|설명|
|-|-|-|
|nil 병합 연산자|A ?? B|A가 nil이 아니면 A를, A가 nil이면 B를 리턴|
|부호변경 연산자|-A|A(수)의 부호를 변경|
|옵셔널 강제 추출 연산자|A!|A(옵셔널 객체)의 값을 강제로 추출
|옵셔널 연산자|A?|A(옵셔널 값)를 안전하게 추출하거나 A(데이터 타입)가 옵셔널임을 표현|

```swift
let optionalInt: Int? = nil
let valueInt1: Int = optionalInt != nil ? optionalInt! : 0
let valueInt2: Int = optionalInt ?? 0
valueInt1과 valueInt2의 식이 동일한 효과를 가진다
```
## 5.2 연산자 우선순위와 결합방향
스위프트는 연산자 **우선순위**를 따로 지정 해놓았기 때문에 코딩하다가 헷갈리는 경우 확인하면 된다.  
우선순위가 높은 연산자는 자신에 비해 낮은 우선순위가 낮은 연산자보다 먼저 실행된다.  
**사용자정의 연산자** 또한 이 규칙에 따라 실행 순서가 결정 된다.  

**결합방향**도 따로 지정되어 있다.  
같은 우선순위에 있는 연산자끼리 나열 되었을 때 어느 방향으로 그룹지을 것인지 나타낸다.
### 예시
`1 + 2 + 3 + 4` +의 결합방향은 왼쪽이기 때문에 `(((1 + 2) + 3) + 4)`와 같이 왼쪽부터 그룹이 묶인다.

기본 연산자들의 우선도와 결합방향을 알아보려면 다음 **[표준 라이브러리 문서](https://developer.apple.com/documentation/swift/swift_standard_library/operator_declarations)** 를 참고.

연산자 우선순위 그룹은 절대치가 아닌 **상대적인 수치**이다.

### 우선순위 그룹(우선순위 높은 순)
|연산자 우선순위 그룹 이름|결합 방향|할당 방향 사용|
|-|-|-|
|DefaultPrecedence|none|false|
|BitwiseShiftPrecedence|none|false|
|MultiplicationPrecedence|left|false|
|AdditionPrecedence|left|false|
|RangeFormationPrecedence|none|false|
|CastingPrecedence|none|false|
|NilCoalescingPrecedence|right|false|
|ComparisonPrecedence|none|false|
|LogicalConjunctionPrecedence|left|false|
|LogicalDisjunctionPrecedence|left|false|
|TernaryPrecedence|right|false|
|AssignmentPrecedence|right|true|
|FunctionArrowPrecedence|right|false|

### 예제

```swift
let intValue: Int = 1
let resultValue1: Int = intValue << 3 + 5 // 8 + 5 => 13
let resultValue2: Int = 1 * 3 + 5         // 3 + 5 => 8
```
- `<<`은 **BitwiseShiftPrecedence** 연산자 우선순위 그룹을 가진다.
- `+`은 **AdditionPrecedence** 연산자 우선순위 그룹을 가진다.
- `*`은 **MultiplicationPrecedence** 연산자 우선순위 그룹을 가진다.


## 5.3 사용자정의 연산자
스위프트에서는 프로그래머의 입맛에 맞게 연산자 역할을 부여할 수 있음  
존재 하지 않던 연산자 기호를 만들어 추가할 수도 있다.  
역할을 부여하기 전에 기존 연산자가 **전위 연산자**, **중위 연산자**, **후위 연산자** 인지 알아야 합니다.  

- 전위 연산자, 피연산자 앞에 위치하는 연산자를 뜻함. 예로 **부정논리연산(NOT) 연산자(!)** 가 있다.
  - **예) !A**
- 중위 연산자, 피연산자 사이에 위치하는 연산자를 뜻함. 예로 **더하기 연산자(+)** 가 있다. 
  - **예) A + B**
- 후위 연산자, 피연산자 뒤에 위치하는 연산자를 뜻함. 예로 [옵셔널](./../CHAPTER08/README.md) 강제 추출 연산자 등이 있다.
  - **예) 0!**
- 선수개념
  - [함수](./../CHAPTER07/README.md)
  - [클래스](./../CHAPTER09/README.md)
  - [메서드](./../CHAPTER10/README.md)


### NOTE_ = 과 ?:
```swift
할당 연산자(=)와 삼항 연산자(?:)는 사용자정의 역할을 부여할 수 없습니다.
```

연산자의 위치를 정의하는 키워드로 `prefix`, `infix`, `postfix`를 사용한다.

|키워드|설명|
|-|-|
|prefix|연산자를 전위 연산자로 정의|
|infix|연산자를 중위 연산자로 정의|
|postfix|연산자를 후위 연산자로 정의|


### 연산자로 사용가능한 문자
사용자정의 연산자는 [아스키(ASCII)](http://www.asciitable.com/) 문자를 이용하여 결합해서 사용한다.
```swift
\ = - + ! * % < > & | ^ ? ~ .
```

### 주의
- **마침표(.)** 맨 처음 문자가 마침표 일때만 연산자에 포함된 마침표가 연산자로 인식한다.
  - 가능한 예) `.+.`
  - 불가능한 예) `+.+`
    - `+`와 `.+`나눠서 인식한다.
- **물음표(?)** 홀로 쓸 수 없으며 결합해서 사용가능.
  - 가능한 예) `^?` 
    - 섞어서 사용
  - 불가능한 예) `?`
    - 홀로 사용
- **느낌표(!)** 후위 연산자는 아예 재정의가 불가능하며, 전위 연산자로 이미 예약된 연산은 재정의가 불가능.
  - 가능한 예) Bool가 아닌 타입을 전위 연산자 사용자 정의
  - 불가능한 예) 후위 연산자로 재정의
- **기타 불가능 사항** 스위프트에서 예약한 상태이기 때문에 재정의 불가하고 사용자 정의 또한 불가능.
  - 토큰으로 사용되는 예) `=`,`=>`,`//`,`/*`,`*/`,`.`
  - 전위 연산자 예) `<`, `&`, `?`
  - 중위 연산자 예) `?`
  - 후위 연산자 예) `>`, `!`, `?`
### 5.3.1 전위 연산자 정의와 구현
기존에 없는 전위 연산자를 만들고 싶다면 연산자 정의를 먼저 해주어야 한다.  
정의된 연산자는 모듈 전역에서 사용가능하다.  

### 정의
**prefix**, operator, 정의할 연산자순으로 구성.

```swift
prefix operator **
```

### 구현
함수 구현 앞에 **prefix**라는 키워드를 붙여 내용을 구현.

```swift
prefix operator **

prefix func **(value: Int) -> Int {
  return value * value
} 

let minusFive = -5
let sqrtMinusFive = **minusFive

print(sqrtMinusFive) // 25
```

### 중복 정의
스위프트 표준 라이브러리에 존재하는 연산자에 기능을 추가할 때는 따로 연산자를 정의 하지 않고 함수만 중복 정의(**overload**)하면 된다.  
전위 연산자 느낌표(!)는 이미 정의가 되어있기 때문에 중복 정의(**overload**)를 합니다.

```swift
prefix func !(value: String) -> Bool {
  return value.isEmpty
}

var stringValue: String = "yagom"
var isEmptyString: Bool = !stringValue

print(isEmptySTring) // false

stringValue = ""
isEmptyString = !stringValue

print(isEmptyString) // true
```
***
```swift
prefix operator **

prefix func **(value: Int) -> Int {
  return value * value
} 

let minusFive = -5
let sqrtMinusFive = **minusFive

print(sqrtMinusFive) // 25

prefix func **(value: String) -> String {
  return value + " " + value
}

let resultString: String = **"rebirthlee"

print(resultString) // rebirthlee rebirthlee
```

### MORE_ 
- **중복 정의(overload)** 및 **재정의(override)** 는 [메서드](./../CHAPTER10/README.md)에서 자세히 다룬다.
- 재정의가 불가능 하기 때문에 **기존 연산자의 우선순위, 결합방향**을 바꾸지 못한다.
  

### 5.3.2 후위 연산자 정의와 구현
전위 연산자와 차이는 없으며 prefix키워드 대신 **postfix**키워드로 대체 된다.

### 정의 및 구현

```swift
postfix operator ** // 정의

postfix func **(value: Int) -> Int { // 구현
  return value + 10
}

let five: Int = 5
let fivePlusTen: Int = five**

print(fivePlusTen) // 15
```

### 전위 연산자와 동시 사용
전위 연산자와 후위 연산자를 동시에 사용하면 후위 연산을 먼저 실행.
```swift
prefix operator **
postfix operator **

prefix func **(value: Int) -> Int {
  return value * value
}

postfix func **(value: Int) -> Int {
  return value + 10
}

let five: Int = 5
let sqrtFivePlusTen: Int = **five**

print(sqrtFivePlusTen) // (10 + 5) * (10 + 5) == 225
```

### 5.3.3 중위 연산자 정의와 구현
전위 연산자와 후위 연산자와 크게 다르지 않으나 우선순위 그룹을 명시해줄 수 있습니다.  
중위 연산자를 정의할 때 우선순위 그룹을 명시해주지 않으면 **DefaultPrecedence**그룹을 우선순위 그룹으로 갖는다.
### 우선순위 그룹 정의

```swift
precedencegroup SqurePrecedence {
    higherThan: MultiplicationPrecedence // 더 낮은 우선순위 그룹
    lowerThan: BitwiseShiftPrecedence // 더 높은 우선순위 그룹
    associativity: right // 결합방향(left / right / none)
    assignment: false // 할당방향 사용(true / false)
}
```

|키워드|설명|
|-|-|
|higherThan|더 낮은순위의 그룹을 정의 할때 사용|
|lowerThan|더 높은순위의 그룹을 정의 할때 사용|
|associativity|결합 우선 방향을 정하는 것|
|assignment|할당방향을 사용([옵셔널 체이닝](./../CHAPTER08/README.md)과 관련사항)|


### 중위 연산자 정의

```swift
precedencegroup SqurePrecedence {
    higherThan: MultiplicationPrecedence // 더 낮은 우선순위 그룹
    lowerThan: BitwiseShiftPrecedence // 더 높은 우선순위 그룹
    associativity: right // 결합방향(left / right / none)
    assignment: false // 할당방향 사용(true / false)
}

infix operator **: SqurePrecedence // SqurePrecedence를 적지 않으면 DefaultPrecedence를 갖는다.
```

### 중위 연산자 구현과 사용
```swift
precedencegroup SqurePrecedence {
    higherThan: MultiplicationPrecedence // 더 낮은 우선순위 그룹
    lowerThan: BitwiseShiftPrecedence // 더 높은 우선순위 그룹
    associativity: right // 결합방향(left / right / none)
    assignment: false // 할당방향 사용(true / false)
}

infix operator **: SqurePrecedence // SqurePrecedence를 적지 않으면 DefaultPrecedence를 갖는다.

func **(lhs: Int, rhs: Int) -> Int {
    var ret: Int = 1;
    if rhs > 0 {
        for _ in 1 ... rhs {
            ret *= lhs
        }
    } else if rhs < 0 {
        // 마이너스 지수에 대한 계산
    }
    
    return ret;
}

print(3 ** 2 ** 3) // 6561, 3^(2^3)
print(3 ** 8) // 6561, 3^8
print(2 ** 3) // 8,  2^3
print(9 ** 3) // 729, 9^3
```

### 클래스 및 구조체의 비교 연산자 구현

```swift
class Human {
  var socialNumber: String? // 주민등록번호
  var name: String? // 이름
}

struct SmartPhone {
  var company: String? // 제조사
  var model: String? // 모델
}

// Human 클래스의 인스턴스끼리 == 연산했을 때 socialNumber가 같다면 true를 반환
func ==(lhs: Human, rhs: Human) -> Bool {
  return lhs.socialNumber == rhs.socialNumber
}

// SmartPhone 구조체의 인스턴스끼리 == 연산했을 때 model이 같다면 true를 반환
func ==(lhs: SmartPhone, rhs: SmartPhone) -> Bool {
  return lhs.model == rhs.model
}

let me = Human()
me.socialNumber = "960xxxx-1..."

let you = Human()
you.socialNumber = "980xxxx-1..."

var myPhone = SmartPhone()
myPhone.model = "GalaxyS10"

var youPhone = SmartPhone()
youPhone.model = "GalaxyS10"

print(me == you) // false
print(myPhone == youPhone) // true
```

전역함수로 구현했으나 특정 타입에 국한된 연산자 함수라면 그 타입 내부에 구현되는 것이 읽고 이해하기 더욱 좋다.

### 비교 연산자 클래스 및 구조체 내부에 구현

```swift
class Human {
  var socialNumber: String? // 주민등록번호
  var name: String? // 이름
  
  // Human 클래스의 인스턴스끼리 == 연산했을 때 socialNumber가 같다면 true를 반환
  static func ==(lhs: Human, rhs: Human) -> Bool {
    return lhs.socialNumber == rhs.socialNumber
  }
}

struct SmartPhone {
  var company: String? // 제조사
  var model: String? // 모델

  // SmartPhone 구조체의 인스턴스끼리 == 연산했을 때 model이 같다면 true를 반환
  static func ==(lhs: SmartPhone, rhs: SmartPhone) -> Bool {
    return lhs.model == rhs.model
  }
}
```
타입 메서드로 구현한 사용자정의 연산자는 각 타입의 익스텐션으로 구현해도 된다.  
익스텐션을 통해 타입 메서드로 구현한 사용자 정의 메서드는 [익스텐션으로 추가할 수 있는 기능](./../CHAPTER21/README.md)에서 확인 가능하다.