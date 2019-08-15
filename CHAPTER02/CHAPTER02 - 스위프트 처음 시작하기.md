
## 2.3 주석

###  2.3.2 마크업 문법을 활용한 문서화 주석

마크업 문법을 활용해 주석을 작성하면 Xcode의 퀵헬프 기능을 통해 볼 수 있습니다. 문서화를 위한 한 줄 주석은 슬래시 세 개(`///`), 여러 줄 주석은 별표 두 개(`/**`, `*/`)를 사용합니다. 다음은 마크업 문법에 대한 간단한 설명입니다.

* 주석 첫 번째 줄에 작성되는 텍스트는 Description 부분에 표기됩니다.

  > :exclamation: 스위프트 5, Xcode 10을 기준으로는 Summary로 표시됩니다.

  > :star: 스위프트의 [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)에 따르면, 이 Summary와 Declaration을 통해서 API의 기능이 완전히 이해될 수 있도록 작성하는 것이 좋다고 합니다!

* `-`, `+`, `*`를 사용하여 원형 글머리 기호를 사용할 수 있고, 번호로 글머리 기호를 매길 수 있습니다.

* 기타 일반적인 마크다운 문법을 이용해 텍스트를 강조하거나, 코드 블록을 만들거나, 제목을 표시할 수 있습니다.

* 다음 키워드들을 통해 적절한 정보를 제공할 수 있습니다.

  <img src="./img/image1_keywords.png" width="500">

  각 delimeter에 관한 더 자세한 사항은 [Markup Functionality]()를 참조하세요.



마크업 문법을 따른 간단한 주석 예시입니다.

```swift
/**
 Errors thrown by fakeArray.
 
 *Values*
 
 `NegativeCount` The count is less than 0.
 
 `EmptyString1` The first string argument is empty.
 
 `EmptyString2` The second string argument is empty.
 
 - Author:
 Newbie
 - Version:
 0.1
 */

enum FakeArrayError: ErrorType {...
```



위 주석을 퀵헬프를 통해 확인하면 다음과 같이 나타납니다(스위프트 5, Xcode 10 기준).

  <img src="./img/image4_quickhelp_example.png" width="500">



이처럼 마크업 문법을 따라 작성된 주석은 다음 항목들에서 확인할 수 있습니다.

* Symbol Completion(자동완성) 제안 시 해당 항목에 대한 Description

  <img src="./img/image2_code_completion.png" width="500">

* Quick Help Inspector 및 Quick Help Popover

  <img src="./img/image3_quickhelp.png" width="500">

## 2.4 변수와 상수

### 2.4.1 변수



### 2.4.2 상수



---

이미지 출처
[API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
[Markup Formatting Reference](https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref/index.html#//apple_ref/doc/uid/TP40016497-CH2-SW1)