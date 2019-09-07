# CHAPTER 08 옵셔널 

옵셔널의 개념은 다음과 같다.

* '변수나 상수 등에 꼭 값이 있다는 것을 보장할 수 없다, 즉 변수 또는 상수의 값이 nil일 수도 있다'는 것을 의미

* 또한 'Optional이 아닌 변수나 상수는 값이 반드시 있다는 것을 보장한다'는 의미

* 어떤 함수의 전달인자로 NULL이 전달되어도 되는지를 문서에 명시하지 않아도 문법적 표현만으로 이를 표현할 수 있다는 장점

  <img src="./img/dictionary_index.png" width="500">

  위 이미지는 Dictionary에서 키를 이용해 인덱스를 찾는 메서드의 API 문서이다. key 매개변수를 통해 전달되는 인자는 nil이어서는 안되고, 리턴값은 nil일 수도 있음을 직관적으로 알려준다.

* **옵셔널과 옵셔널이 아닌 값은 다른 타입으로 인식**하기 때문에 컴파일할 때 바로 오류를 걸러낼 수도 있음

> NULL을 스위프트에서는 nil로 표기한다.



## 8.1 옵셔널 사용

변수 또는 상수에 값이 없을 때 nil로 표현하며, 옵셔널 변수 또는 상수에만 nil을 할당할 수 있다.

값이 없는 옵셔널 변수 또는 상수에 접근하려 하면 런타임 오류가 발생한다.

```swift
var myName: String = "Chaewan"
myName = nil // 오류 발생
```

데이터 타입 뒤에 물음표 `?`를 붙여 옵셔널 변수 또는 상수를 선언한다.

```swift
var myName: String? = "Chaewan"
myName = nil
```

옵셔널은 다음과 같은 상황에서 사용한다.

- 함수 내부에서 제대로 처리하지 못했음을 nil을 반환하여 오류 표현
- 매개변수를 굳이 넘기지 않아도 된다는 뜻으로 매개변수의 타입을 옵셔널로 정의

옵셔널은 제네릭이 적용된 열거형으로 구현되어 있으며, ExpressibleByNilLiteral 프로토콜을 따른다. 또한 옵셔널은 값을 갖는 케이스와 그렇지 못한 케이스 두 가지로 정의되어 있으며, 값이 nil일 때는 none 케이스가 되고, 값이 있는 경우는 some 케이스가 되면서 연관 값인 Wrapped에 값이 할당된다.

```
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
		case none
		case some(Wrapped)

		public init(_ some: Wrapped)
		/// 중략...
}
```

이처럼 옵셔널 타입은, 다음 그림과 같이 실제 값이 옵셔널이라는 열거형의 방패막에 보호되어 래핑되어 있는 형태이다.

<img src="./img/optional_box.png" width="500">

옵셔널은 열거형이기 때문에 switch 구문을 통해 값이 있고 없음을 확인할 수도 있다.

```swift
func checkOptionalValue(value optionalValue: Any?) {
    switch optionalValue {
    case .none:
        print("This Optional variable is nil")
    case .some(let value):
        print("Value is \(value)")
    }
}
```


## 8.2 옵셔널 추출

### 8.2.1 강제 추출

### 8.2.2 옵셔널 바인딩

### 8.2.3 암시적 추출 옵셔널