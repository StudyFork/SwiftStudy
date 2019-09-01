# CHAPTER 05 연산자 

## 5.1 연산자의 종류

### 5.1.1 할당 연산자

### 5.1.2 산술 연산자

### 5.1.3 비교 연산자

### 5.1.4 삼항 조건 연산자

### 5.1.5 범위 연산자

### 5.1.6 부울 연산자

### 5.1.7 비트 연산자

### 5.1.8 복합 할당 연산자

### 5.1.9 오버플로 연산자

### 5.1.10 기타 연산자

## 5.2 연산자 우선순위와 결합방향

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
  return value * 10
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

### 클래스 및 구조체이 비교 연산자 구현

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