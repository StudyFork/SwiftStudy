# CHAPTER 06 흐름 제어

## 6.1 조건문

### 6.1.1 if 구문

### 6.1.2 switch 구문

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
for i in info{
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
for s in setSet{
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
