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
* 기존 프로그래밍 언어의 반복문과 크게 다르지 않지만 전통적인 C언어 스타일의 for문은 사라졌습니다.
* do-while 문 > repeat-while 문으로 구현됩니다.

### 6.2.1 for-in 구문
```swift
for 임시 상수 in 시퀀스 아이템 {
실행 코드
}

for i in 0...2 {
    print(i)
}
// 0
// 1
// 2

for i in 0..<2 {
    print(i)
}
// 0
// 1
```
```java
public class HelloWorld{

    public static void main(String []args){
        int[] d = new int[5];

        for(int i = 0 ; i< d.length; i++ ){
            d[i] = i;
            // System.out.println(d[i]);
        }

        for(int i =0; i< d.length; i+=2 ){
            System.out.println(d[i]);
        }
    }
}
// 0
// 2
// 4
```
```swift
let swift: String = "Swift"
for i in swift.characters {
    print(i)
}

//시퀀스에 해당하는 갑이 필요 없다면 와일드 카드 식별자(_)를 사용하면 됩니다.
for _ in 0..<3 {
    result *= 10
}
print("result : \(result)")
// result : 1000

let arrays: [String] = ["정석준","박채완","김수용","이재성","김태성","윤자경"]
for f in arrays {
    print(f)
}
// 정석준
// 박채완
// 김수용
// 이재성
// 김태성
// 윤자경

let info: [String: String] = ["이름" : "윤자경", "생년월일": "96.11.11"]
for i in info {
    print(info)
} 
// ("이름", "윤자경")
// ("생년월일", "96.11.11")

for (key, value) in info {
    print("\(key) \(value)")
}
// 이름 윤자경
// 생년월일 96.11.11

let setSet: Set<Int> = [1, 2, 3, 4]
for s in setSet {
    print(s)
}
// 1
// 2
// 3
// 4
```
### 6.2.2 while 구문
* 특정 조건(Bool)이 성립하는 한 블록 내부의 코드를 반복해서 실행합니다.

```swift
var phones: [String] = ["Note10", "iphoneXS", "iphone7", "v30"]

while phones.isEmpty == false {
    print("\(phones.removeFirst())")
}
// Note10
// iphoneXS
// iphone7
// v30
```
### 6.2.3 repeat-while 구문
* do while와 같은 역할을 합니다.
* repeat 블록의 코드를 최초 1회 실행한 후, while 다음의 조건이 성립하면 블록 내부의 코드를 반복 실행합니다.
```swift
var phones: [String] = ["Note10", "iphoneXS", "iphone7", "v30"]

repeat {
    print("\(phones.removeFirst())")
} while phones.isEmpty == false
// Note10
// iphoneXS
// iphone7
// v30
```
## 6.3 구문 이름표
* 이때 반복문을 제어하는 키워드(break, continue 등)가 어떤 범위에 적용되어야 하는지 애매하거나 큰 범위의 반복문을 종료하고 싶은데 작은 범위의 반복문만 종료되는 등 예상치 못한 실수를 할 수도 있습니다.
* 반복문 앞에 이름과 함께 콜론을 붙여 구문의 이름을 지정해주는 구문 이름표를 사용하면 좋습니다. 
* 이름이 지정된 구문을 제어하고자 할 때는 키워드와 구문 이름을 함께 써주면 됩니다.

```swift
var numbers: [Int] = [3, 2342, 6, 3252]

numbersLoop : for num in numbers {
    if num > 5 || num < 1 {
        continue numbersLoop
    }
    var count: Int = 0
    
    printLoop: while true {
        print(num)
        count += 1
        
        if count == num {
            break printLoop
        }
    }
    
    removeLoop : while true {
        if numbers.first != num {
            break numbersLoop
        }
        
        numbers.removeFirest()
    }
}
// 3
// 3
// 3
// numbers에는 [2342, 6, 3252]가 남습니다.
```
