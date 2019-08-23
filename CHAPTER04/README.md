# Chapter 04. 데이터 타입 기본

## 4.1 데이터 타입 안심
### 4.1.1 데이터 타입 안심이란
### 4.1.2 타입 추론

## 4.2 타입 별칭

## 4.3 튜플

## 4.4 컬렉션 타입
### 4.4.1 배열
### 4.4.2 딕셔너리
### 4.4.3 세트

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











