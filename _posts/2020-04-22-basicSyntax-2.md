---
layout: post
title:  "기본 문법 공부(프로토콜(protocol) - 프로토콜의 선택적 요구, 프로토콜 변수와 상수, 위임을 위한 프로토콜)"
date:   2020-04-22
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Protocol Example Code - 6](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-22-ProtocolExampleCode-6.playground)

- [Protocol Example Code - 7](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-23-ProtocolExampleCode-7.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

- - -

### 프로토콜의 선택적 요구

- `프로토콜의 요구사항 중 일부를 선택적 요구사항으로 지정할 수 있다.`

- 다만 `먼저 고려해야 할 사항이 있다.`

    - `선택적 요구사항을 정의하고 싶은 프로토콜은 '@objc' 속성이 부여된 프로토콜이어야 한다.`
    
        - `'@objc' 속성은 해당 프로토콜을 'Objective-C' 코드에서 사용할 수 있도록 만드는 역활을 한다.`
    
    - `해당 프로토콜을 'Objective-C' 코드와 공유하고 싶지 않더라도, 혹은 프로젝트를 'Objective-C' 코드와 공유하지 않더라도 '@objc' 속성이 부여되어야만 선택적 요구사항을 정의할 수 있다.`

- 여기서 더 생각해보아야 할 것은 `'@objc' 속성이 부여되는 프로토콜은 'Objective-C' 클래스를 상속받은 클래스에서만 채택할 수 있다는 것이다.`

    - 즉, `열거형이나 구조체 등에서는 '@objc' 속성이 부여된 프로토콜은 아예 채택할 수 없다.`
    
- `'@objc' 속성을 사용하려면 애플의 'Foundation 프레임워크 모듈'을 import 해야 한다.`

- `선택적 요구를 하면 프로토콜을 준수하는 타입에 해당 요구사항을 필수로 구현할 필요가 없다.`

- `선택적 요구사항은 'optional' 식별자를 요구사항의 정의 앞에 붙여주면 된다.`

- 만약 `메서드나 프로퍼티를 선택적 요구사항으로 요구하게 되면 그 요구사항의 타입은 자동적으로 옵셔널이 된다.`

    - `예를 들어 (Int) -> String 타입의 메서드는 ((Int) -> String)? 타입이 된다.`
    
    - `메서드의 매개변수나 반환 타입이 옵셔널이 된 것이 아니라 메서드(함수) 자체의 타입이 옵셔널이 된 것이다.`
    
- `'선택적 요구사항'은 그 프로토콜을 준수하는 타입에 '구현되어 있지 않을 수 있기 때문'에 '옵셔널 체이닝을 통해 호출할 수 있다.'`

    - `프로퍼티뿐만 아니라 메서드도 마찬가지이다.`

<img width="1058" alt="protocolExampleImage-18" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-18.png?raw=true">

- 위 코드의 `Moveable 프로토콜은 '선택적 요구사항인 fly() 메서드'를 '포함'하므로 '@objc 속성을 부여'했다.`

- `@objc 속성의 프로토콜을 사용하기 위해 Tiger와 Bird는 각각 Objective-C 클래스인 NSObject를 상속받았다.`

- `Tiger`는 날 수 없으므로 `fly() 메서드를 구현하지 않았다.`

- `Bird`는 날 수 있으므로 `fly() 메서드를 구현했다.`

- `'각 클래스의 인스턴스를 구현하여 사용'할 때는 '타입에 메서드가 구현되어 있는지 확인할 수 있지만,'` `'Moveable 프로토콜 타입 변수에 할당되었을 때'는 '인스턴스의 타입에 실제로 fly() 메서드가 구현되어 있는지 알 수 없으므로' '옵셔널 체인을 이용하여 fly() 메서드 호출을 시도'한다.`

    - `옵셔널 체인을 사용할 때는 메서드 이름 뒤에 물음표를 붙여 표현한다.`
    
- - -

### 프로토콜 변수와 상수

- `프로토콜 이름을 타입으로 갖는 변수 또는 상수에는 그 프로토콜을 준수하는 타입의 어떤 인스턴스라도 할당할 수 있다.`

<img width="1058" alt="protocolExampleImage-12" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-12.png?raw=true">

<img width="1058" alt="protocolExampleImage-19" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-19.png?raw=true">

- `프로토콜은 프로토콜 이름만으로 자기 스스로 인스턴스를 생성하고 초기화할 수는 없다.`

- 그렇지만 `위의 코드와 같이 프로토콜 변수나 상수를 생성하여 특정 프로토콜을 준수하는 타입의 인스턴스를 할당할 수는 있다.`

- `위의 코드에서 구현한 Pet, Person, School 타입은 모두 Named 프로토콜을 준수한다.`

    - `때문에 Named 프로토콜을 타입으로 갖는 변수 someNamed에 Pet, Person, School 타입의 인스턴스가 할당될 수 있다.`

- - -

### 위임을 위한 프로토콜

- `위임(Delegation)은 클래스나 구조체가 자신의 책임이나 임무를 다른 타입의 인스턴스에게 위임하는 디자인 패턴이다.`

- `책무를 위임하기 위해 정의한 프로토콜을 준수하는 타입은 자신에게 위임될 일정 책무를 할 수 있다는 것을 보장한다.`

- 그렇기 `때문에 다른 인스턴스에게 자신이 해야할 일을 믿고 맡길 수 있다.`

- `위임은 사용자의 특정 행동에 반응하기 위해 사용되기도 하며, 비동기 처리에 많이 사용한다.`

- `위임 패턴(Delegation Pattern)은 애플의 프레임워크에서 사용하는 주요한 패턴 중 하나이다.`

- 언어 자체로 기능이 아닌 `하나의 디자인 패턴`이지만 `애플의 프레임워크에서 중요하게 사용`되는 만큼, 개`념을 알아두면 앞으로 애플 플랫폼의 애플리케이션을 만들 때 도움이 된다.`

<img width="1058" alt="protocolExampleImage-20" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/protocolExampleImage-20.png?raw=true">

- `애플의 프레임워크에 사용하는 위임 패턴을 위해 다양한 프로토콜이 'OOOODelagate'라는 식의 이름으로 정의되어 있다.`

    - `예를 들어 UITableView 타입의 인스턴스가 해야 하는 일을 위임받아 처리하는 인스턴스는 UITableViewDelegate 프로토콜을 준수하면 된다.`
    
    - `위임받은 인스턴스, 즉 UITableViewDelegate 프로토콜을 준수하는 인스턴스는 UITableView의 인스턴스가 해야 하는 일을 대신 처리해줄 수 있다.`
    
- - -    