---
layout: post
title:  "기본 문법 공부(접근제어 - 접근제어 구현, 참고사항)"
date:   2020-03-29
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Access Level Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-29-AccessControlExample.playground)

- [Access Level Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-29-AccessControlExample-2.playground)

- [Access Level Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-29-AccessControlExample-3.playground)

- [Access Level Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-29-AccessControlExample-4.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)

- [Access Level Summary](https://vincentgeranium.github.io/ios,/swift/2020/03/28/basicSyntax-2.html)

- - -

### 접근제어 구현

- `접근제어(Access Control)은 접근수준(Access Level)을 지정해서 구현할 수 있다.`

- `각각의 접근수준을 요소 앞에 지정해주기만 하면 된다.`

- `internal(내부 접근수준)은 기본 접근수준`이므로 굳이 `표기해주지 않아도 된다.`

![AccessControlExampleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AccessControlExampleImage-1.png?raw=true)

- - -

### 접근제어 구현 참고사항

- `모든 타입에 적용되는 접근수준의 규칙은 '상위 요소보다 하위 요소가 더 높은 접근수준을 가질 수 없다'이다.`

![SwiftAccessControlImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/SwiftAccessControl.png?raw=true)

- 위의 그림에서 보이는 것처럼 `비공개 접근수준(Private)으로 정의한 구조체 내부의 프로퍼티로 내부 접근수준(Internal)이나 공개 접근수준(Public)을 갖는 프로퍼티를 정의할 수 없다.`

- 또, `함수의 매개변수(Parameter)로 특정 접근수준이 부여된 타입이 전달되거나 반환된다면, 그 타입의 접근수준보다 함수의 접근수준이 높게 설정될 수 없다.`

- - -

### 잘못된 접근수준 부여

![CannotBeDeclaredAccessLevelImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CannotBeDeclaredAccessLevelImage-1.png?raw=true)

- - -

### 튜플의 접근수준 부여

![CannotBeDeclaredAccessLevelImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CannotBeDeclaredAccessLevelImage-2.png?raw=true)

- `함수뿐만 아니라 튜플의 내부 요소 타입 또한 튜플의 접근수준보다 같거나 높아야 한다.`

- - -

### 접근수준에 따른 접근 결과

```swift
// AClass.swift 파일과 Common.swift 파일이 같은 모듈에 속해 있을 경우

// AClass.swift 파일
class AClass {
    func internalMethod() {}
    fileprivate func fileprivateMethod() {}
    var internalProperty = 0
    fileprivate var filePrivateProperty = 0
}

// Common.swift 파일
let aInstance: AClass = AClass()
aInstance.internalMethod() // 같은 모듈이므로 호출 가능
aInstance.filePrivateMethod() // 다른 파일이므로 호출 불가 - 오류
aInstance.internalProperty = 1 // 같은 모듈이므로 호출 가능
aInstance.filePrivateProperty = 1 // 다른 파일이므로 접근 불가 - 오류
```

- 위의 코드처럼 `접근수준에 따라 접근이 불가능한 경우가 생긴다.`

    - `때문에 프레임워크를 만들 때는 다른 모듈에서 특정 기능에 접근할 수 있도록 API로 사용할 기능을 공개 접근수준(Public)으로 지정해주어야 한다.`
    
    - `그 외의 요소는 내부 접근수준 또는 비공개 접근수준으로 적절히 설정하면 된다.`
    
- - -

### 열거형의 접근수준

![CannotBeDeclaredAccessLevelImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CannotBeDeclaredAccessLevelImage-3.png?raw=true)

- `열거형의 접근수준을 구현할 때 열거형 내부의 각 case별로 따로 접근수준을 부여할 수는 없다.`

- `각 case의 접근수준은 열거형 자체의 접근수준을 따른다.`

- `열거형의 원시 값(rawValue) 타입으로 열거형의 접근수준보다 낮은 접근수준의 타입이 올 수는 없다.`

    - `연관 값의 타입 또한 마찬가지이다.`