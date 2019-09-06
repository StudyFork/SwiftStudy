# CHAPTER 07 함수

## 7.1 함수와 메서드

## 7.2 함수의 정의와 호출

### 7.2.1 기본적인 함수의 정의와 호출

### 7.2.2 매개변수

### 7.2.3 반환 타입

### 7.2.4 데이터 타입으로서의 함수

## 7.3 중첩 함수

스위프트는 데이터 타입의 중첩이 자유롭다.  
열거형 안에 또 하나의 열겨형이 들어갈 수 있고 클래스 안에 또 다른 클래스가 들어올 수 있다.  

- 중첩 함수의 의미는 **함수 안의 함수**를 구현된 것을 의미한다.
- 중첩 함수는 **외부에서 사용**이 불가능하다.
- 아예 외부에서 사용이 불가능 하기보단 **함수를 반환타입**으로 둬 외부에서도 활용이 가능하다.

### 예제 그림

다음 조건을 해당 하는 중첩 함수를 구현.

|...|-3|-2|-1|0|1|2|3|...|
|-|-|-|-|-|-|-|-|-|

- 0은 원점
- 좌로 음수
- 우로 양수
- 특정 위치에서 원점으로 이동
  
### 기존 함수 

```swift
typealias MoveFunc = (Int) -> Int

func goRight(_ currentPosition: Int) -> Int {
    return currentPosition + 1
}

func goLeft(_ currentPosition: Int) -> Int {
    return currentPosition - 1
}

func functionForMove(_ shouldGoLeft: Bool) -> MoveFunc {
    return shouldGoLeft ? goLeft : goRight
}

var position = 3
let moveToZero: MoveFunc = functionForMove(position > 0)

while position != 0 {
    print("\(position)...")
    position = moveToZero(position)
}
print("원점 도착!")
print(goRight(-1)) // 0
print(goLeft(1)) // 0
// 3...
// 2...
// 1...
// 원점 도착!
```

### 중첩 함수

```swift
typealias MoveFunc = (Int) -> Int

func functionForMove(_ shouldGoLeft: Bool) -> MoveFunc {
    func goRight(_ currentPosition: Int) -> Int {
        return currentPosition + 1
    }
    
    func goLeft(_ currentPosition: Int) -> Int {
        return currentPosition - 1
    }
    return shouldGoLeft ? goLeft : goRight
}

var position = -4
let moveToZero: MoveFunc = functionForMove(position > 0)

while position != 0 {
    print("\(position)...")
    position = moveToZero(position)
}
print("원점 도착!")
// print(goRight(-1)) // 함수 내부에 선언 되어 있기 때문에 사용 불가
// print(goLeft(1)) // 함수 내부에 선언 되어 있기 때문에 사용 불가
// -4...
// -3...
// -2...
// -1...
// 원점 도착!
```

## 7.4 종료되지 않는 함수

## 7.5 반환 값을 무시할 수 있는 함수
