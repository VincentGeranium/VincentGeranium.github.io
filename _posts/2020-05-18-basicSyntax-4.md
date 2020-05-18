---
layout: post
title:  "기본 문법 공부(타입 캐스팅(Type Casting) - 데이터 타입 확인(Checking Type))"
date:   2020-05-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Type Casting Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-TypeCastingExampleCode-3.playground)

- [Type Casting Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-TypeCastingExampleCode-4.playground)

- [Type Casting Example Code - 5](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-TypeCastingExampleCode-5.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

- - -
- - -

### 데이터 타입 확인 (Checking Type)

- 타입 확인 연산자인 is를 사용하여 인스턴스가 어떤 클래스(혹은 어떤 클래스의 자식클래스)의 인스턴스인지 타입을 확인해볼 수 있다.

- 타입 확인 연산자는 인스턴스가 해당 클래스의 인스턴스이거나 그 자식클래스의 인스턴스라면 true를 반환하고, 그렇지 않다면 false를 반환한다.

- is 연산자는 클래스의 인스턴스뿐만 아니라 모든 데이터 타입에 사용할 수 있다.

<img width="1058" alt="TypeCastingExampleImg-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-6.png?raw=true" title="TypeCastingExampleImg-6">

- 위의 코드에서 보는 coffee 인스턴스는 Coffee 타입이다. 따라서 coffee는 Latte 타입이나 Americano 타입이 될 수 없다.

    - 그러나 myCoffee는 Americano 타입이며, yourCoffee는 Latte 타입이므로 myCoffee와 yourCoffee는 Coffee 타입인지 확인했을 때 true를 반환받는다.
    
    - 하지만 myCoffee와 yourCoffee는 서로 특성이 다르며 부모와 자식클래스의 관계가 아니기 때문에 서로 다른 타입이다.
    
- is 연산자 외에도 타입을 확인해볼 수 있는 방법이 있다. 메타 타입(Meta Type) 타입을 이용하는 것이다.

- **메타 타입(Meta Type) 타입**은 **타입의 타입**을 뜻한다.

    - 클래스 타입, 구조체 타입, 열거형 타입, 프로토콜 타입등의 타입의 타입이다.
    
        - 즉, 타입 자체가 하나의 타입으로 또 표현될 수 있다는 것이다.
        
- 클래스, 구조체, 열거형의 이름은 타입의 이름이다. 그 타입의 이름 뒤에 .Type를 붙이면 이는 메타 타입(Meta Type)을 나타낸다.

    - 프로토콜 타입의 메타 타입은 .Protocol이라고 붙여주면 된다.
    
        - 예를 들어 SomeClass라는 클래스의 메타 타입은 SomeClass.Type라고 표현하며, SomeProtocol의 메타 타입은 SomeProtocol의 메타 타입은 SomeProtocol.Protocol 이라고 표현한다.
        
- 또, self를 사용해서 타입을 값처럼 표현할 수 있다.

    - 예를 들어 SomeClass.self 라고 표현하면 SomeClass의 인스턴스가 아니라 SomeClass 타입을 값으로 표현한 값을 반환하다.
    
    - 그리고 SomeProtocol.self 라고 표현하면 SomeProtocol을 준수하는 타입의 인스턴스가 아니라 SomeProtocol 프로토콜을 값으로 표현한 값을 반환한다.
    
<img width="1058" alt="TypeCastingExampleImg-7" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-7.png?raw=true" title="TypeCastingExampleImg-7">

- 위의 코드에 정의된 SomeProtocol, SomeClass 등의 메타 타입이 하나의 값으로 취급되어 someType 변수에 할당될 수 있음을 확인할 수 있다.

- 또, Int, String도 스위프트에서 구조체로 구현한 타입이므로 메타 타입을 값으로 취급해 할당될 수 있으믈 확인할 수 있다.

- 만약 프로그램 실행 중에 인스턴스의 타입을 표현한 값을 알아보고자 한다면 type(of:) 함수를 사용한다.

    - 그래서 type(of: someInstance).self라고 표현하면 someInstance의 타입을 값으로 표현한 값을 반환한다.
    
- 인스턴스 self와 타입 self의 의미

    - .self 표현을 값 뒤에 써주면 그 값 자신을 표현하는 값을 반환한다.
    
    - .self 표현을 타입 이름 뒤에 써주면 타입을 표현하는 값을 반환한다.
    
        - "stringValue".self는 "stringValue" 그 자체를 나타내는 값.
        
        - String.self는 String 타입을 나타내는 값.

<img width="1058" alt="TypeCastingExampleImg-8" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-8.png?raw=true" title="TypeCastingExampleImg-8">