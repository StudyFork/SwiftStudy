## Chapter 4. 데이터 타입 고급
## 4.1 데이터 타입 안심
* 서로 다른 타입끼리의 데이터 교환은 꼭 **타입캐스팅**을 거쳐야 합니다.
	* 스위프트에서 값 타입의 데이터 교환은 엄밀히 말하면 타입캐스팅이 아닌 **새로운 인스턴스를 생성**하여 할당하는 것입니다. 

### 4.1.1 데이터 타입 안심이란
* 스위프트는 **타입 안심(type-safe)**언어입니다.
	* 예를 들어 Int 타입 변수에 할당 하려는 값이 character 타입이라면 컴파일 오류가 발생합니다.
* 이렇게 스위프트가 컴파일 시 타입을 확인하는 것을 **타입 확인**이라고 합니다.
* 런타임 에러가 아닌 컴파일 에러로 알려주므로 서로 다른 타입의 값을 할당하는 실수를 줄일 수 있습니다.

### 4.1.2 타입 추론
* 스위프트에서는 변수나 상수를 선언할 때 특정 타입을 명시하지 않아도 컴파일러가 **할당된 값을 기준으로 변수나 상수의 타입을 결정**합니다.

```swift
CODE_ 타입 안심과 타입 추론

//타입을 지정하지 않았으나 타입 추론을 통하여 name은 String 타입으로 선언됩니다.
var name = "Kwanhee"

//String 타입 변수로 지정되었기 때문에 정수를 할당하려고 시도하면 오류가 발생합니다.
name = 100
```

## 4.2 타입 별칭
* 기본으로 제공하는 데이터 타입이든, 사용자가 임의로 만든 데이터 타입이든 이미 존재하는 데이터 타입에 임의로 다른 이름(별칭)을 부여할 수 있습니다.
* 그런다음 기본 타입 이름과 이후에 추가한 별칭을 모두 사용할 수 있습니다.

```swift
CODE_ 타입 별칭

typealias MyInt = Int
typealias YourInt = Int
typealias MyDouble = Double

let age: MyInt = 100	// MyInt는 Int의 또 다른 이름입니다.
var year: YourInt = 2080	// YourInt도 Int의 또 다른 이름입니다.

//MyInt도, YourInt도 Int이기 때문에 같은 타입으로 취급합니다.
year = age
let month: Int = 7	// 물론 기존의 Int도 사용 가능합니다.
let percentage: MyDouble = 99.9	//Int 외에 다른 자료형도 모두 별칭 사용이 가능합니다.

```

## 4.3 튜플

* 튜플(Tuple)은 타입의 이름이 따로 지정되어 있지 않은, 프로그래머 마음대로 만드는 타입입니다.
* **'지정된 데이터의 묶음'**이라고 표현할 수 있습니다.
* 튜플은 타입 이름이 따로 없으므로 일정 타입의 나열만으로 튜플 타입을 생성해줄 수 있습니다.
* 튜플에 포함될 **데이터의 개수는 자유롭게** 정할 수 있습니다.

```swift
CODE_ 튜플 기본

// String, Int, Double 타입을 갖는 튜플
var person: (String, Int, Double) = ("yagom", 100, 182.5)

// 인덱스를 통해서 값을 빼 올 수 있습니다.
print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

person.1 = 99		// 인덱스를 통해 값을 할당할 수 있습니다.
person.2 = 178.5 

print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

```
* 튜플의 각 요소를 이름 대신 숫자로 표현하기 때문에 코드를 볼 때 각 요소가 어떤 의미가 있는지 유추하기가 어렵습니다. 
* 그래서 **튜플의 요소마다 이름**을 붙여줄 수도 있습니다.



```swift
CODE_ 튜플 요소 이름 지정

// String, Int, Double 타입을 갖는 튜플
var person: (name: String, age: Int, height: Double) = ("yagom", 100, 182.5)

// 요소 이름을 통해서 값을 빼 올 수 있습니다.
print("이름: \(person.name), 나이: \(person.age), 신장: \(person.height)")

```
* 또, 튜플에는 타입 이름에 해당하는 키워드가 따로 없다 보니 사용에 불편함을 겪기도 합니다.
* 이럴 때는 타입 별칭을 사용하여 조금 더 깔끔하고 안전하게 코드를 작성할 수 있습니다.


```swift
CODE_ 튜플 별칭 지정

typealias PersonTuple = (name: String, age: Int, height: Double)

let yagom: PersonTuple = ("yagom", 100, 178.5)
let eric: PersonTuple = ("eric", 150, 183.5)

print("이름: \(yagom.name), 나이: \(yagom.age), 신장: \(yagom.height)")
print("이름: \(eric.name), 나이: \(eric.age), 신장: \(eric.height)")

```

## 4.4 컬렉션 타입
* 튜플 외에도 많은 수의 데이터를 묶어서 저장하고 관리할 수 있는 컬렉션 타입을 제공합니다.
* 컬렉션 타입에는 배열(Array), 딕셔너리(Dictionary), 세트(Set)등이 있습니다.

### 4.4.1 배열
* 같은 타입의 데이터를 일렬로 나열한 후 순서대로 저장하는 형태의 컬렉션 타입입니다.
* 각기 다른 위치에 같은 값이 들어갈 수도 있습니다.
* let 키워드를 사용하면 변경 불가능한 배열, var 키워드를 사용하면 변경가능한 배열이 됩니다.
* isEmpty(배열이 비어있는지 확인)와 count(배열의 요소 갯수를 확인)프로퍼티가 존재합니다.
* **필요에 따라 자동으로 버퍼의 크기를 조절**해주므로 요소의 삽입 및 삭제가 자유롭습니다.


```swift
CODE_ 배열의 선언과 생성

// 대괄호를 사용하여 배열임을 표현합니다.
var names: Array<String> = [ "yagom", "chulsoo", "younghee", "yagom"]

// 위 선언과 정확히 동일한 표현입니다. [String]은 Array<String>의 축약표현입니다.
var names: [String] = [ "yagom", "chulsoo", "younghee", "yagom"]

var emptyArray: [Any] = [Any]()	//Any 데이터를 요소로 갖는 빈 배열을 생성합니다.
var emptyArray: [Any] = Array<Any>()		//위 선언과 정확히 같은 동작을 하는 코드입니다.

// 배열의 타입을 정확히 명시해줬다면 []만으로도 빈 배열을 생성할 수 있습니다.
var emptyArray: [Any] = []
print(emptyArray.isEmpty)	//	true
print(names.count)	//	4


```

* 배열은 각 요소에 인덱스를 통해 접근할 수 있으며, 인덱스는 **0 부터 시작**합니다.
* 잘못된 인덱스로 접근하려고 하면 **익셉션 오류(Exception Error)**가 발생합니다.
* **first와 last** 프로퍼티를 통해 맨 처음과 맨 마지막 요소를 가져올 수 있습니다.
* **index(of:)** 메서드를 사용하면 해당 요소의 인덱스를 알아낼 수도 있습니다. 만약 중복된 요소가 있다면 제일 먼저 발견된 요소의 인덱스를 반환합니다.
* **append(_:)** 메서드를 사용하여 맨 뒤에 요소를 추가합니다.
* **insert(_:at:)** 메서드를 사용하여 중간에 요소를 삽입합니다.
* **remove(_:)**메서드를 사용하면 요소가 삭제되고, 삭제된 요소가 삭제된 후 반환됩니다.


### 4.4.2 딕셔너리
* 요소들이 순서 없이 **키와 값의 쌍**으로 구성되는 컬렉션 타입입니다.
* 딕셔너리 안에는 키가 하나이거나 여러개일 수 있으나, 하나의 딕셔너리 안의 키는 같은 이름을 중복해서 사용할 수 없습니다.
* 딕셔너리는 Dictionary라는 키워드와 키의 타입과 값의 타입 이름의 조합으로 써줍니다.
* let 키워드를 쓰면 변경 불가능한 딕셔너리가 되고, var 키워드를 사용하면 변경 가능한 딕셔너리가 됩니다.
* isEmpty(배열이 비어있는지 확인)와 count(배열의 요소 갯수를 확인)프로퍼티가 존재합니다.


```swift
CODE_ 딕셔너리의 선언과 생성

// typealias를 통해 조금 더 단순하게 표현해볼 수 있습니다.
typealias StringInt Dictionary = [String: Int]

// 키는 String, 값은 Int 타입인 빈 딕셔너리를 생성합니다.
var numberForName: Dictionary<String, Int> = Dictionary<String, Int>()

// 위 선언과 같은 표현입니다. [String: Int]는 Dictionary<String, Int>의 축약 표현입니다.
var numberForName: [String: Int] = [String: Int]()

// 위 코드와 같은 동작을 합니다.
var numberForName: StringIntDictionary = StringIntDicionary()

// 딕셔너리의 키와 값 타입을 정확히 명시해줬다면 [:]만으로도 빈 딕셔너리를 생성할 수 있습니다.
var numberForName: [String: Int] = [:]

// 초기값을 주어 생성해줄 수도 있습니다.
var numberForName: [String: Int] = ["yagom": 100, "chulsoo": 200, "jenny": 300]

print(numberForName.isEmpty)	//false
print(numberForName.count)		// 3


```

* 딕셔너리는 각 값에 **키로 접근**할 수 있습니다.
* 딕셔너리 내부에서 **키는 유일**해야 하며, 값은 유일하지 않습니다.
* 딕셔너리 내부에 없는 키로 접근해도 오류가 발생하지 않습니다. 다만 **nil을 반환**합니다.
* **removeValue(forKey:)** 메서드는 특정 키에 해당하는 값을 제거합니다.

```swift
CODE_ 딕셔너리의 사용

print(numberForName["chulsoo"])	// 200
print(numberForName["minji"])	// nil

numberForName["chulsoo"] = 150
print(numberForName["chulsoo"])	// 150

numberForName["max"] = 999		// max라는 키로 999라는 값을 추가해줍니다.
print(numberForName["max"])	// 999

print(numberForName.removeValue(forkey: "yagom"))	// 100

// 위에서 yagom 키에 해당하는 값이 이미 삭제되었으므로 nil값이 반환됩니다.
// 키에 해당하는 값이 없으면 기본값을 돌려주도록 할 수도 있습니다.
print(numberForName.removeValue(forkey: "yagom"))

// yagom 키에 해당하는 값이 없으면 기본으로 0이 반환됩니다.
print(numberForName["yagom", default: 0])	//0


```


순서가 중요하지 않거나 각 요소가 유일한 값이어야 하는 경우에 사용한다. 다음은 세트의 특징을 나열한 것이다.

- 세트 내의 값은 모두 유일한 값이며 중복된 값이 존재하지 않는다.

- `Set<타입 이름>`으로 사용 가능하며, 배열과 달리 축약형이 없다.

- 리터럴 표기법 이용시에는 대괄호로 표현하되 Set 타입임을 명시해야 한다.(배열도 대괄호로 표현하기 때문에 명시하지 않을 경우 컴파일러가 Array로 타입을 지정한다.)

  ```swift
  // 리터럴 표기법 이용시에는 대괄호를 사용하되 Set 타입임을 명시해야 한다.
  var names: Set<String> = ["yagom", "chulsoo", "yonghee", "yagom"]
  ```

- `isEmpty` 프로퍼티를 통해 비어있는 세트인지 확인 가능

- `count` 프로퍼티를 통해 세트에 몇 개의 요소가 존재하는지 확인 가능

- `insert(_:)`, `remove(_:)` 메서드를 이용해 세트에 요소 추가 및 삭제

- 세트 내부의 값들이 모두 유일함을 보장하므로 집합 연산에 최적화되어있다.

- 교집합, 합집합, 차집합 등 집합 연산을 할 수 있는 메서드가 구현되어 있다.

## 4.5 열거형
연관된 항목을 그룹으로 묶어서 표현할 수 있는 타입이며, 프로그래머가 정의해 준 항목 값만 가질 수 있어서 제한된 선택지를 주고 싶을 때 유용하다. 또한 스위프트의 열거형은 각 항목이 그 자체로 고유의 값을 가지기 때문에 다른 언어에 비해 안전하다는 장점이 있다.

예를 들어, C 언어의 열거형은 각 항목이 순차적인 정수값을 가진다.

```c
// C 언어의 열거형
enum day
{
  mon, tue, wed, thr, fri, sat, sun
};

enum school
{
  primary = 0,
  elementary = 1,
  middle = 2
};

if (mon == primary)
{
  printf("Same Value\n"); // 모두 같은 정수값 0이므로 같다.
}
```

이렇게 모든 열거형의 데이터 타입을 같은 타입으로 취급하기 때문에 여러 열거형을 사용할 때 실수로 인한 버그가 생길 수도 있다. 스위프트의 열거형은 C 언어와 달리 각 열거형이 고유의 타입으로 구분되기 때문에 실수로 버그가 일어날 가능성이 원천 봉쇄된다.

열거형의 각 항목이 원시 값(Raw Value)이라는 형태로 실제 값을 가질 수도 있으며, 연관 값을 사용하여 값의 묶음도 구현할 수 있다. `switch` 구문과도 함께 활용할 수 있다.



### 4.5.1 기본 열거형

`enum` 키워드로 선언한다.

```swift
enum School {
    case primary        // 유치원
    case elementary     // 초등
    case middle         // 중등
    case high           // 고등
    case college        // 대학
    case university     // 대학교
    case graduate       // 대학원
}

var highestEducationLevel: School = School.university
var highestEducationLevel: School = .university         // 위 코드와 정확히 같은 표현입니다.
```

`highestEducationLevel` 변수는 열거형 School 타입 내부의 항목으로만 변경될 수 있다.



### 4.5.2 원시 값

열거형 이름 오른쪽에 타입을 명시하면 각 항목이 해당 타입의 원시 값(Raw Value)을 가질 수 있다. 아래 코드처럼 일부 항목만 원시 값을 가질 수도 있다.

```swift
enum School: String {
    case primary = "유치원"
    case elementary = "초등학교"
    case middle = "중학교"
    case high = "고등학교"
    case college
    case university
    case graduate
}
```

원시 값은 rawValue라는 프로퍼티를 이용해 가져올 수 있다.

```swift
print(School.elementary.rawValue)   // 초등학교
```

일부 항목만 원시 값을 지정했을 때, 문자열 형식의 원시 값을 지정해줬다면 각 항목 이름을 그대로 원시 값으로 갖게 되고, 정수 타입이라면 첫 항목을 기준으로 0부터 1씩 늘어난 값을 갖게 된다.

```swift
print(School.college.rawValue) // college
```

원시 값을 갖는 열거형의 경우 원시 값을 통해 열거형 생성이 가능하다. 해당 값이 없으면 nil을 반환한다.

```swift
let primary = School(rawValue: "유치원")  // primary
let graduate = School(rawValue: "석박사")  // nil
```



### 4.5.3 연관 값

열거형 내의 일부 항목이 자신과 연관된 값을 가질 수 있다. 연관 값은 열거형일수도 있고, 기본 데이터 타입일 수도 있다.

```swift
enum MainDish {
    case pasta(taste: String)
}

var dinner: MainDish = MainDish.pasta(taste: "크림")  // 크림 파스타
```



### 4.5.4 순환 열거형

열거형 항목의 연관 값이 열거형 자신의 값이고자 할 때 `indirect` 키워드를 사용하여 순환 열거형임을 명시한다.



### 열거형 활용: Error 표현

스위프트의 열거형은 간단한 에러들을 나타내기에 적합하다. 다음은 실제 코드에서 활용할 수 있는 열거형을 이용한 에러 표현의 예시들이다.

```swift
enum IntParsingError: Error {
    case overflow
    case invalidInput(Character)
}
```

String을 Int로 파싱하다가 발생할 수 있는 Error 표현이다. 연관 값을 이용해 추가 정보를 포함할 수 있다.

```swift
struct XMLParsingError: Error {
    enum ErrorKind {
        case invalidCharacter
        case mismatchedTag
        case internalError
    }

    let line: Int
    let column: Int
    let kind: ErrorKind
}

func parse(_ source: String) throws -> XMLDoc {
    // ...
    throw XMLParsingError(line: 19, column: 5, kind: .mismatchedTag)
    // ...
}
```

XML document를 파싱하다가 발생할 수 있는 에러를 표현하였다. 이와 같이 에러 표현을 위해 구조체를 선언하고 에러 종류를 나타내는 열거형과 함께 에러가 발생한 위치에 대한 정보를 포함시킬 수도 있다.

출처: [Error - Swift Standard Library | Apple Developer Documentation](https://developer.apple.com/documentation/swift/error)











