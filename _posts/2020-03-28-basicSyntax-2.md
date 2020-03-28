---
layout: post
title:  "기본 문법 공부(접근제어 - 접근수준, public, open 등)"
date:   2020-03-28
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)

- [Access Control Summary - 1](https://vincentgeranium.github.io/ios,/swift/2020/03/28/basicSyntax.html)

- - -

### 접근수준 (Access Level)

- 접근제어(Access Control)는 접근수준(Access Level) 키워드를 통해 구현할 수 있다.

- 각 타입(클래스, 구조체, 열거형등)에 특정 접근수준을 지정할 수 있고, 타입 내부의 프로퍼티, 메서드, 이니셜라이저, 서브스크립트 각각에도 접근수준을 지정할 수 있다.

- 접근수준(Access Level)을 명시할 수 있는 키워드는 open, public, internal, fileprivate, private 다섯 가지가 있다.

- 스위프트의 접근수준은 기본적으로 모듈과 소스파일에 따라 구분한다.

![AccessLevelImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/SwiftAccessControl.png?raw=true)

- - -

### 공개 접근수준, public

- public 키워드로 접근수준이 지정된 요소는 어디서든 쓰일 수 있다.

- 자신이 구현된 소스파일은 물론, 그 소스파일이 속해 있는 모듈, 그 모듈을 가져다 쓰는 모듈 등 모든 곳에서 사용 할 수 있다.

- 공개(Public) 접근수준은 주로 프레임워크(Framework)에서 외부와 연결될 인터페이스(Interface)를 구현하는데 많이 쓰인다.

- 스위프트의 기본 요소는 모두 공개 접근수준으로 구현되어 있다고 생각하면 된다.

```swift
/// A value type whose instances are either 'true' or 'false'
public struct Bool {
    /// Default-initialize Boolean value to 'false'
    public init()
}
```

- - -

### 개방 접근수준, open

- open 키워드로 지정할 수 있는 개방(Open) 접근수준은 공개(Public) 접근수준 이상으로 높은 접근수준이며, 클래스와 클래스의 멤버에서만 사용할 수 있다.

- 기본적으로 공개 접근수준과 비슷하지만 아래와 같은 차이점이 있다.

    - 개방 접근수준(open)을 제외한 다른 모든 접근수준(public, internal, fileprivate, private)의 클래스는 그 클래스가 정의된 모듈 안에서만 상속할 수 있다.
    
    - 개방 접근수준(open)을 제외한 다른 모든 접근수준(public, internal, fileprivate, private)의 클래스 멤버는 해당 멤버가 정의된 모듈 안에서만 재정의할 수 있다.
    
    - 개방 접근수준(open)의 클래스는 그 클래스가 정의된 모듈 밖의 다른 모듈에서도 상속할 수 있다.
    
    - 개방 접근수준(open)의 클래스 멤버는 해당 멤버가 정의된 모듈 밖의 다른 모듈에서도 재정의할 수 있다.
    
- 클래스를 개방 접근수준으로 명시하는 것은 그 클래스를 다른 모듈에서도 부모클래스로 사용하겠다는 목적으로 클래스를 설계하고 코드를 작성했음을 의미한다.

```swift
// Foundation 프레임워크에 정의되어 있는 개방 접근수준의 NSString 클래스

open class NSString: NSObject, NSCopying, NSMutableCopying, NSSecureCoding {
    open var length: Int { get }
    open func character(at index: Int) -> unichar
    public init()
    public init?(coder aDecoder: NSCoder)
}
```

- - -

### 내부 접근수준, internal

- internal 키워드로 지정하는 내부(Internal) 접근수준은 기본적으로 모든 요소에 암묵적으로 지정하는 기본 접근수준이다.

- 내부 접근수준으로 지정된 요소는 소스파일이 속해 있는 모듈 어디에서든 쓰일 수 있다.

- 다만 그 모듈을 가져다 쓰는 외부 모듈에서는 접근할 수 없다.

- 보통 외부에서 사용할 클래스나 구조체가 아니며, 모듈 내부에서 광역적으로 사용할 경우 내부 접근 수준을 지정한다.

- - -

### 파일외부비공개 접근수준, fileprivate

- 파일외부비공개(File-private) 접근수준으로 지정된 요소는 그 요소가 구현된 소스파일 내부에서만 사용할 수 있다.

- 해당 소스파일 외부에서 값이 변경되거나 함수를 호출하면 부작용이 생길 수 있는 경우에 사용하면 좋다.

- - -

### 비공개 접근수준, private

- 비공개(private) 접근수준은 가장 한정적인 범위이다.

- 비공개 접근수준으로 지정된 요소는 그 기능을 정의하고 구현한 범위 내에서만 사용할 수 있다.

- 비공객 접근수준으로 지정한 기능은 심지어 같은 소스파일 안에 구현한 다른 타입이나 기능에서도 사용할 수 없다.

- - -