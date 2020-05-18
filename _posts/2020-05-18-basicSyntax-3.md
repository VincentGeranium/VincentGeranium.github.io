---
layout: post
title:  "기본 문법 공부(타입 캐스팅(Type Casting) - 스위프트 타입 캐스팅(Type Casting of Swift))"
date:   2020-05-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Type Casting Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-TypeCastingExampleCode-2.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

- - -
- - -

### 스위프트 타입 캐스팅 (Type Casting of Swift)

- 스위프트에서는 다른 언어의 타입 변환 혹은 타입 캐스팅을 이니셜라이저(Initializer)로 단순화했다.

- 스위프트의 타입 캐스팅은 조금 다른 의미로 사용한다.

    - 스위프트의 타입 캐스팅은 인스턴스의 타입을 확인하거나 자신을 다른 타입의 인스턴스인양 행세할 수 있는 방법으로 사용할 수 있다.
    
- 스위프트의 타입 캐스팅은 is 와 as 연산자로 구현했다.

    - 이 두 연산자로 값의 타입을 확인하거나 다른 타입으로 전환(Cast)할 수 있다.
    
    - 또한 타입 캐스팅을 통해 프로토콜(Protocol)을 준수하는지도 확인해볼 수 있다.
    
- 스위프트의 타입 캐스팅은 실제로 참조 타입(Reference Type)에서 주로 사용된다.

<img width="1058" alt="TypeCastingExampleImg-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-3.png?raw=true" title="TypeCastingExampleImg-3">

- 위의 코드는 Coffee 클래스와 Coffee 클래스를 상속받은 Latte와 Americano 클래스이다.

<img width="1058" alt="TypeCastingExampleImg-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-4.png?raw=true" title="TypeCastingExampleImg-4">

- 위 그림은 Coffee, Latte, Americano의 클래스 상속도이다.

<img width="1058" alt="TypeCastingExampleImg-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-5.png?raw=true" title="TypeCastingExampleImg-5">

- 위 그림은 Coffee, Latte, Americano의 클래스 포함도이다.

    - 위 그림 중 클래스 상속도를 보면 Latte와 Americano 클래스는 Coffee 클래스를 상속받은 것을 확인할 수 있다.
    
    - 위 그림 중 클래스 포함도를 보면 Coffee 클래스가 갖는 특성들을 Latte나 Americano가 모두 포함한다는 사실도 알 수 있다.
    
    - 다시 말하면 Coffee는 Latte나 Americano인 척할 수 없지만, Latte나 Americano는 Coffee인 척할 수 있다는 뜻이다.
    
        - 왜냐하면 Latte나 Americano는 Coffee가 갖는 특성을 모두 갖기 때문이다. 이를 이해하는 것이 스위프트의 타입 캐스팅을 이해하고 활용하는 시작점이다.