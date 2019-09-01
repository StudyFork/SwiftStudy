# CHAPTER 06 흐름 제어 
스위프트의 흐름 제어 구문에서 소괄호()를 대부분 생략 가능하고 중괄호{}는 생략 할 수 없다.
## 6.1 조건문

### 6.1.1 if 구문
if 구문은 Bool 타입이어야 한다.  
소괄호()를 생략하고 사용이 가능하다.
```swift
let first: Int = 5
let second: Int = 7

if first > second {
    print("first > second")
} else if first < second {
    print("first < second")
} else {
    print("first == second")
}
```
### 6.1.2 switch 구문
소괄호()를 생략하고 사용이 가능하다.  
특정 case에만 동작하고 종료되기 때문에 break를 사용하지 않아도 된다.  
조건은 다양한 값이 들어갈 수 있지만 데이터 타입이 같아야 한다.  
조건에 들어가는 값이 열거형(enum)이 아니라면 default 처리를 해줘야 한다.  
case에는 범위 연산자나 where 절을 사용하여 조건을 확장 할 수 있다.  

#### switch 구문 기본 구현
```swift
let integerValue: Int = 5

switch integerValue {
case 0:
    print("Value == zero")
case 1...10:
    print("Value == 1~10")
    fallthrough // switch를 종료하지 않고 다른 케이스도 검사
case Int.min..<0, 101..<Int.max:
    print("Value < 0 or Value > 100")
    break // switch를 종료, 사용하지 않아도 됨
default:
    print("10 < Value <= 100")
}
```
#### 부동소수 타입의 범위 연산
```swift
let doubleValue: Double = 3.0

switch doubleValue {
case 0:
    print("Value == zero")
case 1.5...10.5:
    print("1.5 <= Value <= 10.5")
default:
    print("Value == \(doubleValue)")
}
```
#### 문자열 switch case 구성
```swift
let stringValue: String = "Liam Neeson"

switch stringValue {
case "yagom":
    print("He is yagom")
case "Jay":
    print("He is Jay")
case "Jenny", "Joker", "Nova":
    print("He or She is \(stringValue)")
default:
    print("\(stringValue) said 'I don't know who you are'")
}
```
case 다음에는 꼭 실행 가능한 코드가 나와야한다.  
만약 오류 없이 사용하고 싶다면 fallthrough를 사용해야한다
```swift
...
case "Jenny": // 오류발생
case "Joker":
    fallthrough // fallthrough로 오류 발생하지 않음
case "Nova":
    print("He or She is \(stringValue)")
...
```
#### 튜플 switch 구성
```swift
typealias NameAge = (name: String, age: Int)

let tupleValue: NameAge = ("yagom", 99)
switch tupleValue {
case ("yagom", 99):
    print("정확히 맞췄습니다!")
case ("yagom", _):
    print("이름만 맞췄습니다. 나이는 \(tupleValue.age)입니다.")
case (let name, 99):
    print("나이만 맞췄습니다. 이름는 \(name)입니다.")
default:
    print("누구를 찾나요?")
}
```
와일드카드(_)를 사용하면 다양한 케이스를 처리 할 수 있습니다.  
와일드카드 대신에 값 바인딩을 할 수 있습니다.
#### where 사용
```swift
let 직급: String = "사원"
let 연차: Int = 1
let 인턴인가: Bool = false

switch 직급 {
case "사원" where 인턴인가 == true:
    print("인턴입니다.")
case "사원" where 연차 < 2 && 인턴인가 == false:
    print("신입사원입니다.")
case "사원" where 연차 > 5:
    print("연식 좀 된 사원입니다.")
case "사원":
    print("사원입니다.")
case "대리":
    print("대리입니다.")
default:
    print("사장입니까?")
}
```
#### enum 조건
```swift
enum School {
    case primary, elementary, middle, high, colleage, university, graduate
}

let 최종학력: School = School.university

switch 최종학력{
case .primary:
    print("최종학력은 유치원입니다.")
case .elementary:
    print("최종학력은 초등학교입니다.")
case .middle:
    print("최종학력은 중학교입니다.")
case .high:
    print("최종학력은 고등학교입니다.")
case .colleage, .university:
    print("최종학력은 대학(교)입니다.")
case .graduate:
    print("최종학력은 대학원입니다.")
}
```
## 6.2 반복문

### 6.2.1 for-in 구문

### 6.2.2 while 구문

### 6.2.3 repeat-while 구문

## 6.3 구문 이름표