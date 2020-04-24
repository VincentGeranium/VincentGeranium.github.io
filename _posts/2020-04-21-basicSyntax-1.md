---
layout: post
title:  "기본 문법 공부(프로토콜(protocol) - 가변 메서드 요구, 이니셜라이져 요구)"
date:   2020-04-21
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Protocol Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-21-ProtocolExampleCode-3.playground)

- [Protocol Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-21-ProtocolExampleCode-4.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

- [데이터 타입 고급 - 열거형(Enumeration)](https://vincentgeranium.github.io/ios,/swift/2020/03/17/basicSyntax.html)

- [기본 문법 공부(구조체와 클래스의 차이)](https://vincentgeranium.github.io/ios,/swift/2020/02/28/basicSyntax.html)

- [기본 문법 공부(값 타입과 참조 타입)](https://vincentgeranium.github.io/ios,/swift/2020/02/29/basicSyntax.html)

- [기본 문법 공부(프로퍼티와 메서드 - 메서드, 인스턴스 메서드)](https://vincentgeranium.github.io/ios,/swift/2020/03/22/basicSyntax.html)

- [기본 문법 공부(인스턴스 생성 및 소멸 - 초기화 위임, 실패 가능한 이니셜라이저)](https://vincentgeranium.github.io/ios,/swift/2020/03/25/basicSyntax.html)

- - -

### 가변 메서드 요구 (Mutating Method Requirements)

- `값 타입(구조체, 열거형)의 인스턴스 메서드에서 자신 내부의 값을 변경하고자 할 때는 메서드의 'func' 키워드 앞에 'mutating' 키워드를 적어 메서드에서 인스턴스 내부의 값을 변경한다는 것을 확실히 해준다.`

- `프로토콜이 어떤 타입이든 간에 인스턴스 내부의 값을 변경해야 하는 메서드를 요구하려면 프로토콜의 메서드 정의 앞에 'mutating' 키워드를 명시해야 한다.`

- `참조 타입인 클래스의 메서드 앞에는 'mutating' 키워드를 명시하지 않아도 인스턴스 내부 값을 바꾸는 데 문제가 없다.`

- `값 타입인 구조체와 열거형의 메서드 앞에는 'mutating' 키워드를 붙인 가변 메서드 요구(Mutating Method Requirements)가 필요하다.`

- `프로토콜에 'mutating' 키워드를 사용한 메서드 요구가 있다고 하더라도 클래스 구현에서는 'mutating' 키워드를 써주지 않아도 된다.`

<img width="1058" alt="protocolExampleImage-7" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-7.png?raw=true">

- `Resettable 프로토콜`은 `reset()이라는 가변 메서드를 요구`한다.

- `Resettable 프로토콜을 채택한 Person 클래스`에는 `'mutating' 키워드를 제외하고 'reset()' 메서드를 구현`했다.

- `Resettable 프로토콜을 채택한 값 타입인 Point 구조체와 Direction 열거형`은 `'mutating' 키워드를 포함하여 구현`했다.

- `'만약 Resettable 프로토콜에서 가변 메서드를 요구하지 않는다면, 값 타입의 인스턴스 내부 값을 변경하는 mutating 메서드는 구현이 불가능하다'`

- - -

### 이니셜라이저 요구

- `프로토콜은 프로퍼티, 메서드 등과 마찬가지로 특정한 이니셜라이저를 요구할 수도 있다.`

- `프로토콜에서 이니셜라이저를 요구하려면 메서드 요구와 마찬가지로 이니셜라이저를 정의하지만 구현은 하지 않는다.`

    - `즉, 이니셜라이저의 매개변수를 지정하기만 할 뿐, 중괄호를 포함한 이니셜라이저 구현은 하지 않는다.`
    
<img width="1058" alt="protocolExampleImage-8" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-8.png?raw=true">

- 위 코드의 `Pet 구조체는 Named 프로토콜을 채택`하여 `요구 프로퍼티와 이니셜라이저를 모두 구현`했다.

<img width="1058" alt="protocolExampleImage-9" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-9.png?raw=true">

- `구조체는 상속할 수 없기 때문에 이니셜라이저 요구에 대해 크게 신경쓸 필요가 없지만 클래스의 경우라면 조금 다르다.`

- `클래스 타입에서 프로토콜의 이니셜라이저의 요구에 부합하는 이니셜라이저를 구현할 때는 이니셜라이저가 지정 이니셜라이저인지 편의 이니셜라이저인지는 중요하지 않다.`

    - 그러나 `이니셜라이저 요구에 부합하는 이니셜라이저를 구현할 때는 'required' 식별자를 붙인 '요구 이니셜라이저'로 구현해야 한다.`

- 위의 코드의 `Person 클래스를 상속받는 모든 클래스는 'Named' 프로토콜을 준수해야 하며, 이는 곧 상속받는 클래스에 해당 이니셜라이저를 모두 구현해야 한다는 뜻이다.`

    - 그렇기 `때문에 Named에서 요구하는 init(name:) 이니셜라이저를 'required' 식별자를 붙인 '요청 이니셜라이저'로 구현해야 한다.`

<img width="1058" alt="protocolExampleImage-10" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-10.png?raw=true">

- 만약에 `'클래스 자체가 상속받을 수 없는 final 클래스'라면 'required' 식별자를 붙여줄 필요가 없다.`

    - `상속할 수 없는 클래스와 요청 이니셜라이저 구현은 무의미하기 때문이다.`

<img width="1058" alt="protocolExampleImage-11" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-11.png?raw=true">

- `만약 특정 클래스에 프로토콜이 요구하는 이니셜라이저가 이미 구현되어 있는 상황에서 그 클래스를 상속받은 클래스가 있다면, 'required'와 'override' 식별자를 모두 명시하여 프로토콜에서 요구하는 이니셜라이저를 구현해주어야 한다.`

- 위의 코드에서 `School 클래스는 Named 프로토콜을 채택하지 않았지만 Named 프로토콜이 요구하는 이니셜라이저가 이미 있는 상태이다.`

    - 그런데 `MiddleSchool 클래스는 School 클래스를 상속받았으며, Named 프로토콜을 채택했다.`

    - 그래서 `School 클래스에서 상속받은 init(name:) 이니셜라이저를 재정의`해야 하며 `동시에 Named 프로토콜의 이니셜라이저 요구도 충족시켜주어야 한다.`

    - 그래서 `'override'와 'required' 식별자를 모두 표기해야 한다.`

    - `두 식별자 중 어떤 것이 먼저 위치해도 상관 없다. 즉, 식별자의 표기 순서는 상관 없다는 뜻이다.`
    
- - -

### 실패 가능한 이니셜라이저 요구
    
<img width="1058" alt="protocolExampleImage-12re" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-12.png?raw=true">

- `프로토콜은 일반 이니셜라이저 외에도 '실패 가능한 이니셜라이저'를 요구할 수도 있다.`

- `실패 가능한 이니셜라이저를 요구하는 프로토콜을 준수하는 타입은 해당 이니셜라이저를 구현할 때 실패 가능한 이니셜라이저로 구현해도, 일반적인 이니셜라이저로 구현해도 무방하다.`
