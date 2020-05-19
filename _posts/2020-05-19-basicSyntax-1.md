---
layout: post
title:  "기본 문법 공부(타입 캐스팅(Type Casting) - 다운캐스팅(Downcasting))"
date:   2020-05-19s
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Type Casting Example Code - 6](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-19-TypeCastingExampleCode-6.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

- - -
- - -

### 다운캐스팅(Downcasting)

- 어떤 클래스 타입의 변수 또는 상수가 정말로 해당 클래스의 인스턴스를 참조하지 않을 수도 있다.

    - 예를 들어 Latte 클래스의 인스턴스가 Coffee 클래스의 인스턴스인양 Coffee 행세를 할 수 있다
    
<img width="1058" alt="TypeCastingExampleImg-9" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-9.png?raw=true" title="TypeCastingExampleImg-9">

- 위 코드의 actingConstant 상수는 Coffee 인스턴스를 참조하도록 선언했지만, 실제로는 Coffee 타입인 척 하는 Latte 타입의 인스턴스를 참조하고 있다.

- 이런 상황에서 actingConstant가 참조하는 인스턴스를 진짜 타입인 Latte 타입으로 사용해야 할 때가 있다.

    - 가령 Latte 타입에 정의되어 있는 메서드를 사용하거나 프로퍼티에 접근해야 할 때 Latte 타입으로 변수의 타입을 변환해주어야 한다.
    
    - 이를 스위프트에서 **다운캐스팅(Downcasting)**이라고 한다.
    
<img width="1058" alt="TypeCastingExampleImg-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-4.png?raw=true" title="TypeCastingExampleImg-4">

- 위의 그림은 Coffee, Latte, Americano 클래스 상속 모식도 이다.

- 클래스의 상속 모식도에서 자식클래스보다 더 상위에 있는 부모클래스의 타입을 자식클래스의 타입으로 캐스팅한다고 해서 다운캐스팅(Downcasting)이라고 부르는 것이다.

- 다운캐스팅이 클래스의 인스턴스에서만 사용하는 것은 아니다. Any 타입 등에서 다른 타입으로 캐스팅할 때도 다운캐스팅을 사용한다.

- **타입캐스트 연산자(Type Cast Operator)**에는 as?와 as! 두 가지가 있다.

    - 타입캐스트 연산자를 사용하여 자식클래스 타입으로 다운캐스팅할 수 있다.

- 다운캐스팅은 실패의 여지가 충분히 있기 때문에 ?가 붙은 연산자와 !가 붙은 연산자 두 종류가 있다.

- 다운캐스팅을 시도해보는 조건부 연산자인 as? 연산자는 다운캐스팅이 실패했을 경우 nil을 반환한다.

    - as? 연산자는 반환 타입이 옵셔널이다.

- 다운캐스팅을 강제하는 as! 연산자는 다운캐스팅에 실패할 경우 런타임 오류가 발생한다.

    - as! 연산자는 반환 타입이 옵셔널이 아니다.
    
- 다운캐스팅에 실패할 가능성이 있가면 조건부 연산자인 as?를 사용해야 한다.

    - 조건부 연산자 as?를 사용하면 다운캐스팅에 성공할 경우 옵셔널 타입으로 인스턴스를 반환하며, 실패할 경우 nil을 반환한다.
    
- 다운캐스팅이 무조건 성공할 것이라고 확신한다면, 즉 해당 변수 또는 상수가 참조하는 인스턴스가 다운캐스팅하고자 하는 타입이 확실하다면 강제 연산자인 as!를 사용할 수 있다.

    - as! 연산자를 사용하여 다운캐스팅이 성공할 경우 옵셔널이 아닌 인스턴스가 반환되며, 실패할 경우 런타임 오류가 발생한다.
    
<img width="1058" alt="TypeCastingExampleImg-10" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-10.png?raw=true" title="TypeCastingExampleImg-10">

- 위 코드에서는 as? 와 as!의 사용 방법을 살펴볼 수 있다.

- if let actingOne: Americano = coffee as? Americano만 놓고 보면 "만약 coffee가 참조하는 인스턴스가 Americano 타입의 인스턴스라면 actingOne이라는 임시 상수에 할당하라"로 해석할 수 있다.

- let castedAmericano: Americano = coffee as! Americano만 놓고 보면 "coffee가 참조하는 인스턴스를 Americano 타입으로 강제 변환하여 castedAmericano 상수에 할당하라. 뒷일은 책임지지 않는다."로 해석할 수 있다.

- 컴파일러가 다운캐스팅은 확신할 수 있는 경우에는 as? 나 as! 대신 as를 사용할 수도 있다.

- 항상 성공하는 것을 아는 경우는 캐스팅하려는 타입이 같은 타입이거나 부모클래스 타입이라는 것을 알 때이다.

<img width="1058" alt="TypeCastingExampleImg-11" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-11.png?raw=true" title="TypeCastingExampleImg-11">

- 타입캐스팅의 의미

    - 캐스팅은 실제로 인스턴스를 수정하거나 값을 변경하는 작업이 아니다. 인스턴스는 메모리에 똑같이 남아있을 뿐이다.
    
    - 다만 인스턴스를 사용할 때 어떤 타입으로 다루고 어떤 타입으로 접근해야 할지 판단할 수 있도록 컴퓨터에게 힌트를 주는 것뿐이다.
    
- - -
- - -