# CHAPTER 07 함수

함수가 도대체 뭔데?!
* 함수란 프로그램 소스 코드에서 **일정한 동작을 수행** 하는 코드 집합체 이다.
* Swift에서의 함수는 **1급 객체(first class citizen)** 이기 때문에 하나의 값으로도 사용할 수 있습니다.

다음 조건을 모두 충족하는 객체를 **1급 객체(first class citizen)** 라고 한다
* 변수에 담을 수 있다.
* 파라미터로 전달할 수 있다.
* 변환값으로 사용할 수 있다.

## 7.1 함수와 메서드
> 함수와 메서드는 기본적으로 같지만, 상황이나 위치에 따라 다른 용어로 부르는것이다. 구조체, 클래스, 열거형 등 **특정 타입에 연관되어 사용하는 함수**를 **메서드**, **모듈 전체에서 전역**으로 사용할 수 있는 함수를 그냥 **함수**라고 부릅니다.

```Swift
func someFunction() {
    print("Hello, Call me the \'Function\'")
}

class someClass {
    func someMethod() {
        print("Hello, Call me the \'Method\'")
    }
}
```

## 7.2 함수의 정의와 호출
* 함수와 메서드는 정의하는 위치와 호출되는 범위만 다를 뿐 정의하는 키워드와 구현 방법은 동일하다.
* 조건문이나 반복문 같은 Swift의 다른 문법과 달리 함수에서는 소괄호 **()** 생략이 불가하다.
* 재정의(override)와 중복 정의(overload)를 모두 지원 한다.

### 7.2.1 기본적인 함수의 정의와 호출
함수의 기본 형태
* 함수를 정의하는 키워드는 **func** 이다.
* 함수 이름을 지정후 매개변수는 소괄호 **()** 로 감싼다.
* 변환 타입을 명시하기 전에는 **->** 를 사용하여 어떤 타입인지 명시를 한다.
* 반환을 위한 키워드는 다른 언어처럼 **return** 입니다.

```Swift
func 함수이름(매개변수...) -> 반환 타입 {
    실행 구문
    return 변환 타입
}
```

기본 형태의 함수 정의와 사용 예제

```Swift
func askHello(who: String) -> String {
    return "Hey \(who), How are you today?"
}

print(askHello(who: "cat")) // Hey cat, How are you today?
```

### 7.2.2 매개변수
잠깐! 매개변수와 전달 인자가 뭐야?
* **매개변수**란 함수의 정의부분에 나열되어 있는 **변수(variable)** 들을 의미한다.
* **전달인자**는 함수를 호출할때 전달되는 **실제 값(value)** 을 의미한다.

#### 매개변수가 없는 함수와 매개변수가 여러 개인 함수
오호 그러면 매개변수가 필요 없는 경우에는 어떻게 구현하지?
> 함수에 매개변수가 필요 없다면 매개변수 위치를 공란으로 바꿔라!

```Swift
func getMotto() -> String {
    return "I'll be a full stack developer!"
}

print(getMotto()) // I'll be a full stack developer!
```

그러면 매개변수를 여러 개 넘겨야 할 때는 어떻게 구현 하지?
> 매개변수가 여러 개 필요한 함수를 정의할 때는 **쉼표(,)** 로 구분하여 정의하면 된다. 이때 주의할 점은 함수를 호출할 때, 매개변수 이름을 붙여주고 **콜론(:)** 을 적어준 후 전달인자를 적어준다.

```Swift
func makePromise(time: String, who: String) -> String {
    return "Will you meet at \(time), \(who)?"
}

print(makePromise(time: "10:30", who: "taesung")) // Will you meet at 10:30, taesung?
```

#### 매개변수 이름과 전달인자 레이블
전달인자의 레이블도 변경이 가능할까?
> 보통 함수를 정의할 때 매개변수를 정의하면 매개변수 이름과 전달인자 레이블을 같은 이름으로 사용할 수 있지만 전달인자 레이블을 별도로 지정하면 함수 외부에서 매개변수의 역활을 좀 더 명확히 할 수 있다. 전달인자 레이블을 사용하려면 함수 정의에서 매개변수 이름 앞에 한칸을 띄운 후 전달 인자 레이블을 작성하면 됩니다.
```Swift
func seyHello(from myName: String,to name: String) -> String {
    return "Hello \(name)! I'm \(myName)"
}

print(seyHello(from: "taesung", "cat")) // Hello cat! I'm taesung
```


나는 함수를 호출할때마다 매개변수명을 적는게 너무 귀찮아 무슨 방법 없을까?
> 함수의 매개변수명 앞에 **언더바(_)** 를 적으면 호출할때 **생략 할 수 있다.**

```Swift
func makePromise(_ time: String,_ who: String) -> String {
    return "Will you meet at \(time), \(who)?"
}

print(makePromise("10:30", "taesung")) // Will you meet at 10:30, taesung?
```

>전달인자 레이블을 변경하면 함수의 이름 자체가 변경됩니다. 그렇기 때문에 전달인자 레이블만 다르게 써주더라도 함수 증복 정의(오버로드)로 동작할 수 있다.

```Swift
func askHello(to who: String, _ times: Int) -> String {
    return String(repeating: "Hey \(who), How are you today?", count: times)
}

func askHello(to who: String, repeat times: Int) -> String {
    return String(repeating: "Hey \(who), How are you today?", count: times)
}

print(askHello(to: "cat", 2)) // Hey cat, How are you today?Hey cat, How are you today?
print(askHello(to: "cat", repeat: 2)) // Hey cat, How are you today?Hey cat, How are you today?
```

#### 매개변수 기본값
스위프트의 함수에서는 매개변수마다 기본값을 지정할 수 없을까?
> 위에 적힌 askHello 함수에서 times 매개변수에 기본값을 3을 주면 매개변수를 넘겨주지 않아도 times 값을 3으로 설정하여 함수가 동작하게 된다.

```Swift
func askHello(to who: String, _ times: Int = 3) -> String {
    return String(repeating: "Hey \(who), How are you today?", count: times)
}

print(askHello(to: "cat", 2)) // Hey cat, How are you today?Hey cat, How are you today?
print(askHello(to: "cat")) // Hey cat, How are you today?Hey cat, How are you today?today?Hey cat, How are you today?
```

> 기본값이 없는 매개변수는 기본값이 있는 매개변수 앞에 사용하는것이 좋다. 보통 기본값이 없는 매개변수는 대체로 함수를 사용함에 있어 중요한 값을 전달할 가능성이 높기 때문입니다.

#### 가변 매개변수와 입출력 매개변수
매개변수로 몇 개의 값이 들어오지 모를 때, 가변 매개변수를 사용할 수 있습니다. 가변 매개변수는 0개 이상(0개 포함)의 값을 받아올 수 있으며, 가변 매개변수로 들어온 인자 값은 배열처럼 사용이 가능합니다. 주의할점은 함수마다 가변 매개변수는 하나만 가질 수 있습니다.

```Swift
func sayHelloToFriends(me: String, friends names: String...) -> String {
    var result: String = ""
    
    for friend in names {
        result += "Hello \(friend)! "
    }

    result += "I'm \(me)!"
}

print(sayHelloToFriends(me: "taesung", friends: "C++", "Java", "Swift"))
// Hellow C++! Hellow Java! Hellow Swift! I'm taesung
```
> 함수의 **전달인자로 값을 전달할 때는 보통 값을 복사해서 전달합니다.** 값이 아닌 **참조 포인터(*)를 전달하려면 입출력 매개변수를 사용합니다.** 값 타입 데이터의 참조를 전달인자로 보내면 함수 내부에서 참조하여 원래 값을 변경합니다. 하지만 이 방법은 **함수 외부의 값에 어떤 영향을 줄지 모르기 때문에** 함수형 프로그래밍 패러다임에서는 **지양하는 패턴이다.**

입출력 매개변수의 전달 순서는 다음과 같다
1. 함수를 호출할 때, 전달인자의 값을 복사한다.
2. 해당 전달인자의 값을 변경하면 1에서 복사한 것을 내부에서 변경한다.
3. 함수를 반환하는 시점에 2에서 변경된 값을 원래의 매개변수에 할당한다.
> 주의할점은 연산 프로퍼티 또는 감시자가 있는 프로퍼티가 입출력 매개변수로 전달된다면 함수 호출 시점에 그 프로퍼티 접근자가 호출되고 반환시점에 프로퍼티의 설정자가 호출된다.

```Swift
var numbers: [Int] = [1, 2, 3]

func nonReferenceParameter(_ arr: [Int]) {
    var copiedArr: [Int] = arr
    copiedArr[1] = 1
}

func referenceParameter(_ arr: inout [Int]) {
    arr[1] = 1
}

nonReferenceParameter(numbers)
print(numbers[1])                   // 2

referenceParameter(&numbers)        // 참조를 표현하기 위해 &를 붙여줍니다.
print(numbers[1])                   // 1

class Person {
    var height: Float = 0.0
    var weight: Float = 0.0
}

var taesung: Person = Person()

// 참조 타입의 inout 매개변수 사용은 더욱 중의해야 합니다.
// C 언어의 이중 포인터와 유사하게 동작합니다.
func reference(_ person: inout Person) {
    person.height = 183    // 이렇게 사용하면 기존 참조 매개변수처럼 동작하지만
    print(person.height)   // 183.0
    person = Person()      // 이렇게 다른 인스턴스를 할당하면 참조 자체가 변경되어버립니다.
}

reference(&taesung)
print(taesung.height) // 0.0 함수 안에서 새로운 인스턴스가 할당되었기 때문에 위 taesung과 다른 참조를 갖습니다.
```
> 입출력 매개변수는 매개변수 기본값을 가질 수 없으며, 가변 매개변수로 사용될 수 없습니다. 또한 상수는 변경될 수 없으므로 입출력 매개변수의 전달인자로 사용될 수 없습니다.

### 7.2.3 반환 타입
함수가 반환이 없는 경우에는 어떻게 구현 할까?
> 함수는 특정 연산을 수행한 후 결괏값을 반환합니다. 그러나 **값의 반환이 굳이 필요하지 않은 함수**도 있습니다. 그럴 때는 반환 값이 없는 함수를 만들 수 있는데, **반환 타입을 생략하거나 없음을 의미하는 (Void)로 표기**할 수 있습니다.

```Swift
func askHello(who: String) {
    print("Hey \(who), How are you today?")
}

func getMotto() -> Void {
    print("I'll be a full stack developer!")
}

askHello(who: "cat")     // Hey cat, How are you today?
getMotto()               // I'll be a full stack developer!
```

### 7.2.4 데이터 타입으로서의 함수

## 7.3 중첩 함수

## 7.4 종료되지 않는 함수

## 7.5 반환 값을 무시할 수 있는 함수
