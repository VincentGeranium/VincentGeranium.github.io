---
layout: post
title:  "기본 문법 공부(프로토콜(protocol) - 프로토콜이란, 정의)"
date:   2020-04-20
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

- - -

### 프로토콜이란

- 프로토콜(Protocol)은 특정 역활을 하기 위한 메서드, 프로퍼티, 기타 요구사항등의 청사진을 정의한다.

- 구조체, 클래스, 열거형은 프로토콜을 채택(Adopted)해서 특정 기능을 실행하기 위한 프로토콜의 요구사항을 실제로 구현할 수 있다.

- 어떤 프로토콜의 요구사항을 모두 따르는 타입은 '해당 프로토콜을 준수한다(Conform)'고 표현한다.

- 타입에서 프로토콜의 요구사항을 충족시키려면 프로토콜이 제시하는 청사진의 기능을 모두 구현해야 한다.

- 즉, 프로토콜은 정의를 하고 제시를 할 뿐 이지 스스로 기능을 구현하지는 않는다.

- - -

### 프로토콜 정의

```swift
protocol 프로토콜 이름 {
    프로토콜 정의
}
```

- 프로토콜은 구조체, 클래스, 열거형의 모양과 비슷하게 정의할 수 있으며 'protocol' 키워드를 사용한다.

```swift
// 타입의 프로토콜 채택

struct SomeStruct: AProtocol, AnotherProtocol {
    // 구조체 정의
}

class SomeClass: AProtocol, AnotherProtocol {
    // 클래스 정의
}

enum SomeEnum: AProtocol, AnotherProtocol {
    // 열거형 정의
}
```

- 구조체, 클래스, 열거형 등에서 프로토콜을 채택(Adopted)하려면 타입 이름 뒤에 콜론(:)을 붙여준 후 채택할 프로토콜 이름을 쉼표(,)로 구분하여 명시해준다.

- 위의 타입의 프로토콜 채택 코드의 각 타입은 AProtocol과 AnotherProtocol을 채택한 것이다.

```swift
// Super Class를 상속받는 클래스의 프로토콜 채택
class SomeClass: SuperClass, AProtocol, AnotherProtocol {
    // 클래스 정의
}
```

- 클래스가 다른 클래스를 상속받는다면 상속받을 클래스의 이름 다음에 채택할 프로토콜을 나열해준다.

- SomeClass는 SuperClass를 상속받았으며 동시에 AProtocol과 AnotherProtocol 프로토콜을 채택(Adopted)한 클래스이다.

- - -