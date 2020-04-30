---
layout: post
title:  "기본 문법 공부(확장(expansion) - 제네릭(Generic))"
date:   2020-04-30
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Generic Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-30-GenericExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -

### 제네릭(Generic)

- 제네릭(Generic)은 스위프트의 강력한 기능중 하나이다.

- 제네릭을 이용해 코드를 구현하면 어떤 타입에도 유연하게 대응할 수 있다.

- 또한 제네릭으로 구현한 기능과 타입은 재사용하기도 쉽고, 코드의 중복을 줄일 수 있기에 깔금하고 추상적인 표현이 가능하다.

- 스위프트 표준 라이브러리 또한 수많은 제네릭 코드로 구성되어 있다.

- Array, Dictionary, Set 등의 타입은 모두 제네릭 컬렉션이다.

- Int나 String 타입을 요소로 갖는 배열을 만들거나 그 외의 어떤 타입도 배열을 요소로 가질 수 있었던건 모두 제네릭 덕분이다.

```swift
// 제네릭, 프로토콜, 서브스크립트 등 다양한 기능으로 구현된 Array 타입 선언부

public struct Array<Element> : RandomAccessCollection, MutableCollection {
    public typealias Index = Int
    public typealias Interator = IndexingInterator(<Element>)
    // 중략...
    public var startIndex: Int { get }
    public var endIndex: Int { get }
    // 중략...
    public subscript(index: Int) -> Element
    public subscript(bounds: Range<Int>) -> ArraySlice<Element>
    // 중략...
    public mutating func popLast() -> Element?
    // 중략...
    public func map<T>(_ transform: (Element) throws -> T) rethrows -> [T]
    // 중략...
    public var last: Element? { get }
    // 중략...
    public func reduce<Result>(_ initialResult: Result, _ nextPartialResult: (Result, Element) throws -> Result) rethrows -> 
    Result
}
```

- 제네릭을 사용하고자 할 때는 제네릭이 필요한 타입 또는 메서드의 이름 뒤의 홀화살괄호 기호 (<>) 사이에 제네릭을 위한 타입 매개변수를 써주어 제네릭을 사용할 것임을 표시한다.

```swift
제네릭을 사용하고자 하는 타입 이름 <타입 매개변수>
제네릭을 사용하고자 하는 함수 이름 <타입 매개변수> (함수의 매개변수...)
```

- 'Array 타입의 선언부 코드'를 보면 Array는 타입 매개변수 Element가 있으며, map 메서드는 타입 매개변수 T가 있다.

- Array는 제네릭을 사용하는 제네릭 타입이고, map 메서드는 제네릭을 사용하는 제네릭 함수이기 때문이다.

<img width="1058" alt="prefixImage" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-2.png?raw=true">

- 위 코드의 사용자정의 연산자 **는 조금 한정된 범위에서만 사용할 수 있다.

    - 즉, Int 타입에서만 사용자정의 연산자를 사용할 수 있다.
    
    - UInt 타입, 즉 부호가 없는 정수 타입에서는 Int 타입에 구현해준 사용자정의 연산자를 사용하지 못한다.
    
<img width="1058" alt="genericImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-1.png?raw=true">

- 위의 코드는 범용적으로 사용하기 위하여 '정수의 제곱을 구하는 연산자'를 구현.

- 프로토콜과 제네릭이라는 스위프트의 기능을 조합하여 정수 타입 프로토콜, 즉 BinaryInteger 프로토콜에 해당하는 값이면 해당 연산자를 사용할 수 있도록 (제네릭을 이용하여) 구현해줄 수 있다.
    
    - 그렇게 되면 UInt 타입에서도 해당 연산자를 사용할 수 있다.
    
<img width="1058" alt="genericImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-2.png?raw=true">

- 위 코드의 swapTwoInts(_:_:) 함수는 두 Int 타입의 변숫값을 교환하는 역활을 충분히 해낼 수 있다.

- 만약에 Int 타입이 아닌 Double이나 String 타입의 변숫값을 서로 교환하고 싶다면 별도의 함수를 구현해주어야 할 것이다.

<img width="1058" alt="genericImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-3.png?raw=true">

- 위 코드의 swapTwoStrings(_:_:) 함수는 두 String 타입의 변수끼리 값을 교환하는 역활은 충분히 해냈지만 이 함수도 마찬가지로 String 타입끼리의 교환만 허용할 뿐이다.

- Double 타입의 값 교환을 원한다면 또 다른 함수를 구현해야 한다. 그리고 타입마다 다른 함수를 써줘야 하는 불편함도 있다.

<img width="1058" alt="genericImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-4.png?raw=true">

- 위 코드의 swapTwoValues(_:_:) 함수는 inout 매개변수로 두 Any 타입의 값을 받는다.

    - Any 타입의 anyOne과 anyTwo 변수의 값을 교환하는 데는 무리가 없다.
    
        - 다만 Any 타입의 두 변수에 어떤 타입의 값이 들어있을지 모른다.
    
        - Int면 Int끼리, String이면 String끼리 교환하고 싶은데, 그런 제한을 줄 수 없다.
        
    - 또 다른 문제점도 있다. Any 타입의 inout 매개변수를 통해 전달될 전달인자의 타입은 Any로 전달되어야 한다.
    
        - 다른 타입인 String 타입의 변수(stringOne, stringTwo)를 전달인자로 전달할 수 없다.
        
        - 그래서 String 타입의 값을 Any 타입의 변수(anyOne, anyTwo)에 넣어 함수를 호출해야 하는데, 그 순간 값은 복사되어 할당한다. 즉, 새로운 변수로만 함수를 호출할 수 있는것이다.
        
        - 그렇게 되면 우리가 원했던 stringOne과 stringTwo의 값은 교환할 수 없다.
        
- - -
- - -