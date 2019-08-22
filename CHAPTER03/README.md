# Chapter 03. 데이터 타입 기본

## 3.1 Int와 UInt

## 3.2 Bool

## 3.3 Float과 Double

## 3.4 Character

## 3.5 String

### 3.5.1 특수문자
제어문자라고도 불리는 특수문자는 모두 `\`에 특정한 문자를 조합하여 사용한다.  
|특수문자|설명|
|-|-|
|\\n|줄바꿈 문자|
|\\\\|문자열 내에서 백슬래시를 표현하고자 할 때 사용|
|\\"|문자열 내에서 큰따옴표를 표현하고자 할 때 사용|
|\\t|탭 문자. 키보드의 탭키를 눌렀을 때와 같은 효과|
|\\0|문자열이 끝났음을 알리는 null 문자|

## 3.6 Any, AnyObject와 nil
- Any
  - 스위프트 모든 데이터 타입
- AnyObject
  - Any와 비슷하지만 클래스의 인스턴스만 할당 가능

```swift
var someVar: Any = "yagom"
someVar = 50
someVar = 100.1
someVar = 10.0
```
```
Any나 AnyObject는 타입을 확인하고 변환하는 작업을 해야하고 예상하지 못한 오류를 발생 할 수 있으니 사용하지 않는게 좋다.
```
- nil
  - 값이 없음을 나타냄
  - nil인 상태에서 접근 하면 Null Point Exception이 발생