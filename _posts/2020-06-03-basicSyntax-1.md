---
layout: post
title:  "기본 문법 공부(확장(expansion) - 타입 제약(Type Constraints))"
date:   2020-06-02
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -
- - -

### 타입 제약(Type Constraints)

- 제네릭 기능의 타입 매개변수는 실제 사용 시 타입의 제약 없이 사용할 수 있다.

- **그러나 종종 제네릭 함수가 처리해야 할 기능이 특정 타입에 한정되어야만 처리할 수 있다던가, 제네릭 타입을 특정 프로토콜을 따르는 타입만 사용할 수 있도록 제약을 두어야 하는 상황이 발생할 수 있다.**

    - **타입 제약은 타입 매개변수가 가져야 할 제약사항을 지정할 수 있는 방법이다.**
    
        - 예를 들어 타입 매개변수 자리에 사용할 실제 타입이 특정 클래스를 상속 받는 타입이어야 한다든지, 특정 프로토콜을 준수하는 타입이어야 한다는 등의 제약을 줄 수 있다는 뜻이다.
        
    - **타입 제약(Type Constraints)은 클래스 타입 또는 프로토콜로만 줄 수 있다.**
    
        - 즉, 열거형, 구조체 등의 타입은 타입 제약의 타입으로 사용할 수 없다.
        
        - 예를 들어 자주 사용하는 제네릭 타입인 Dictionary의 키는 Hashable 프로토콜을 준수하는 타입만 사용할 수 있다.
        
        ```swift
        // Dictionary Type 정의
        
        public struct Dictionary<Key: Hashable, Value> : Collection, 
            ExpressibleByDictionaryLiteral { /*...*?}
        ```
        
- Dictionary Type 정의 코드를 살펴보면 Dictionary의 두 타입 매개변수는 Key 와 Value 이다.

    - 그런데 Key 뒤에 콜론(:)을 붙인 다음에 Hashable이라고 명시되어 있다.
    
        - **이는 타입 매개변수인 Key 타입은 Hashable 프로토콜을 준수해야 한다는 뜻이다.**
        
        - 즉, Key로 사용할 수 있는 타입 Hashable 프로토콜을 준수하는 타입이어야 한다는 것이다.
        
        - Hashable은 스위프트 표준 라이브러리에 정의되어 있는 프로토콜이며 스위프트의 기본 타입(String, Int, Bool 등등)은 모두 Hashable 프로토콜을 준수한다.
        
- **제네릭 타입에 제약을 주고 싶으면 타입 매개변수 뒤에 콜론을 붙인 후 원하는 클래스 타입 또는 프로토콜을 명시하면 된다.**

```swift
// 제네릭 타입 제약

func swapTwoValuse<T: BinaryInteger>(_ a: inout T, _ b: inout T) {
    // 함수 구현
}

func Stack<Element: Hashable> {
    // 구조체 구현
}    
```

- 위 코드는 기존(확장 시리즈 중 제네릭 관련 post 참고)에 타입 제약 없이 구현해보았던 swapTwoValues(_:_:) 함수와 Stack 구조체에 타입 제약을 준 것이다.

    - **코드에서 보다시피 타입 매개변수 뒤에 콜론을 붙이고 제약조건으로 주어질 타입을 명시해주면 된다.**
    
    - 여러 제약을 추가하고 싶다면 콤마로 구분해주는 것이 아니라 **where 절**을 사용할 수 있다.
    
    - Stack 구조체의 Element 타입 매개변수의 타입을 Hashable 프로토콜을 준수하는 타입으로 제약을 준다면, Any 타입은 Hashable 프로토콜을 준수하지 않기 때문에 기존에 사용했던(확장 시리즈 중 제네릭 관련 example code 참고) Any 타입은 사용할 수 없다.
    
```swift
// 제네릭 타입 제약 추가

func swapTwoValues<T: BinaryInteger>(_ a: inout T, _ b: inout T) where 
    T: FloatingPoint, T: Equatable {
    // 함수 구현
}    
```

- 위의 코드는 현재 Post에서 설명하는 내용들의 의도와는 조금 다른 내용이다.

- 상식적으로 생각한다면 T는 정수도, 실수도 들어올 수 있게 구현하고 싶지만, 그렇게 하려면 함수를 중복 정의해주어야 한다.

    - 다만 where를 사용하여 제약을 추가할 수는 있다.
    
- 즉, 위 코드의 T는 BinaryInterger 프로토콜을 준수하고, FloatingPoint 프로토콜도 준수하며 Equatable 프로토콜도 준수하는 타입만 사용할 수 있다.

    - 개발자가 특별히 사용자정의 타입을 만들어 구현하지 않는 한, 저 조건에 맞는 기본 타입은 없다.
    
```swift
// substractTwoValue 함수의 잘못된 구현

func substractTwoValue<T>(_ a: T, _ b: T) -> T {
    return a - b
}
```

- 위의 substractTwoValue(_:_:) 함수는 T라는 타입 매개변수가 있는 간단한 제네릭 함수이다.

     - 그런데 이 함수에는 중대한 실수가 있는데, 뺄셈을 하려면 뺄셈 연산자를 사용할 수 있는 타입이여야 연산이 가능하다는 한계이다.
     
     - **즉, T가 실제로 받아들일 수 있는 타입은 뺄셈 연산자를 사용할 수 있는 타입이어야 한다.**
     
```swift
// substractTwoValue 함수의 구현

func substractTwoValue<T: Binary Integer>(_ a: T, _ b: T) -> T {
    return a - b
}
```

- **위의 코드에서 타입 매개변수인 T의 타입을 BinaryInteger 프로토콜을 준수하는 타입으로 한정해두니 뺄셈 연산이 가능하게 되었다.**

    - 이처럼 **타입 제약은 함수 내부에서 실행해야 할 연산에 따라 적절한 타입을 전달받을 수 있도록 제약을 둘 수 있다.**
    
```swift

// 프로토콜과 제네릭을 이용한 전위 연산자 구현과 사용

prefix operator **

prefix func **<T: BinaryInteger> (value: T) -> T {
    return value * value
}
```

- 위 코드의 ** 연산자를 보면 타입 매개변수(T)가 BinaryInteger라는 특정 프로토콜을 준수할 때 제네릭 함수인 연산자를 사용할 수 있도록 타입을 제약해 주었다.

```swift
// makeDictionaryWithTwoValue 함수의 구현

func makeDictionaryWithTwoValue<Key: Hashable, Value>(key: Key, value: 
    Value) -> Dictionary<Key, Value> {
    let dictionary: Dictionary<Key, Value> = [key:value]
    return dictionary
}
```

- 위 코드의 makeDictionaryWithTwoValue(_:_:) 함수는 **Key와 Value라는 타입 매개변수가 있다.**

    - **두 타입 매개변수의 제약조건이 다르다는 것을 알 수 있다.**
    
    - **이처럼 타입 매개변수마다 제약조건을 달리해서 구현해줄 수도 있다.**
    
- - -
- - -