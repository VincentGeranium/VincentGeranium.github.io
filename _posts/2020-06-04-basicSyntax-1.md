---
layout: post
title:  "기본 문법 공부(확장(expansion) - 프로토콜의 연관 타입(Using a Protocol in Its Associated Type’s Constraints))"
date:   2020-06-04
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Using a Protocol in Its Associated Type's Constraints Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-04-AssociatedTypeExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -
- - -

### 프로토콜의 연관 타입(Using a Protocol in Its Associated Type's Constraints)

- 프로토콜을 정의할 때 연관타입(Associated Type)을 함께 정의하면 유용할 때가 있다.

- **연관 타입은 프로토콜에서 사용할 수 있는 플레이스홀더 이름이다.**

- 즉, 제네릭에서는 어떤 타입이 들어올지 모를 때, 타입 매개변수를 통해 '종류는 알 수 없지만, 어떤 타입이 여기에 쓰일 것이다.'라고 표현해주었다면 **연관 타입은 타입 매개변수의 그 역활을 프로토콜에서 실행할 수 있도록 만들어진 기능이다.**

<img width="1058" alt="associatedTypeImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/associatedTypeImage-1.png?raw=true" title="associatedTypeImage-1">

- 위 코드의 Container 프로토콜은 존재하지 않는 타입인 ItemType을 **연관 타입으로 정의**하여 프로토콜 정의에서 **타입 이름으로 활용**한다.

    - **이는 제네릭의 타입 매개변수와 유사한 기능으로, 프로토콜 정의 내부에서 사용할 타입이 '그 어떤 것이어도 상관없지만, 하나의 타입임은 분명하다.'라는 의미이다.**
    
- Container 프로토콜을 준수하는 타입이 꼭 구현해야 할 기능은 아래와 같다.

    - 1) 컨테이너의 새로운 아이템을 append(_:) 메서드를 통해 추가할 수 있어야 한다.
    
    - 2) 아이템 개수를 확인할 수 있도록 Int 타입 값을 갖는 count 프로퍼티를 구현해야 한다.
    
    - 3) Int 타입의 인덱스 값으로 특정 인덱스에 해당하는 아이템을 가져올 수 있는 서브스크립트를 구현해야 한다.
    
- 위 세 가지 조건을 충족한다면 Container 프로토콜을 준수하는 타입이 될 수 있다.

    - 그런데 컨테이너가 어떤 타입의 아이템을 저장해야 할지에 대해서 언급하지 않았다.
    
<img width="1058" alt="associatedTypeImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/associatedTypeImage-2.png?raw=true" title="associatedTypeImage-2">

- 위 코드의 MyContainer 클래스는 Container 프로토콜을 준수하기 위해서 필요한 것을 모두 갖추었다.

    - **연관 타입인 ItemType 대신에 실제 타입인 Int 타입으로 구현해주었고, 이는 프로토콜의 요구사항을 모두 충족하므로 큰 문제가 없다.**
    
        - 그 이유는 프로토콜에서 ItemType이라는 연관 타입만 정의했을 뿐, 특정 타입을 지정하지 않았기 때문이다.
        
        - **실제 프로토콜 정의를 준수하기 위해 구현할 때는 ItemType을 하나의 타입으로 일관성 있게 구현하면 된다.**
        
<img width="1058" alt="associatedTypeImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/associatedTypeImage-3.png?raw=true" title="associatedTypeImage-3">   

- 위 코드의 IntStack 구조체는 Container 프로토콜을 채택했고, 해당 프로토콜을 준수하기 위해 append(_:) 메서드, count 프로퍼티, 서브스크립트를 구현했다.

    - **다만 ItemType 대신 Int 타입을 사용하여 구현했을 뿐이다.**
    
<img width="1058" alt="associatedTypeImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/associatedTypeImage-4.png?raw=true" title="associatedTypeImage-4">

- **만약 ItemType을 어떤 타입으로 사용할지 조금 더 명확히 해주고 싶다면 IntStack 구조체 구현부에 typealias ItemType = Int 라고 타입 별칭을 지정해줄 수 있다.**

<img width="1058" alt="associatedTypeImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/associatedTypeImage-5.png?raw=true" title="associatedTypeImage-5">

- 프로토콜의 연관 타입에 대응하여 실제 타입을 사용할 수도 있지만, **제네릭 타입에서는 연관 타입과 타입 매개변수를 대응시킬 수도 있다.**

- 위 코드를 보면 **Container 프로토콜을 준수하기 위해 Stack 구조체에서 ItemType이라는 연관 타입 대신에 Element라는 타입 매개변수를 사용했음을 볼 수 있다.**

    - 그럼에도 Stack 구조체는 Container 프로토콜을 완벽히 준수한다.

- - -
- - -