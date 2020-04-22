---
layout: post
title:  "기본 문법 공부(프로토콜(protocol) - 프로토콜 요구사항, 프로퍼티 요구, 메서드 요구)"
date:   2020-04-20
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Protocol Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-20-ProtocolExampleCode-1.playground)

- [Protocol Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-20-ProtocolExampleCode-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

- [기본 문법 공부(프로퍼티, 저장 프로퍼티)](https://vincentgeranium.github.io/ios,/swift/2020/03/01/basicSyntax.html)

- [기본 문법 공부(연산 프로퍼티)](https://vincentgeranium.github.io/ios,/swift/2020/03/13/basicSyntax.html)

- [기본 문법 공부(프로퍼티와 메서드 - 타입 메서드)](https://vincentgeranium.github.io/ios,/swift/2020/03/23/basicSyntax.html)

- - -

### 프로토콜 요구사항

- `프로토콜(Protocol)은 타입이 특정 기능을 실행하기 위해 '필요한 기능을 요구'한다.`

- `프로토콜이 자신을 채택(Adopted)한 타입에 '요구하는 사항'은 '프로퍼티나 메서드와 같은 기능들'이다.`

- - -

### 프로퍼티 요구

- `프로토콜은 자신을 채택한 타입이 '어떤 프로퍼티를 구현해야 하는지 요구'할 수 있다.`

    - `그렇지만 프로토콜은 그 프로퍼티의 종류(연산 프로퍼티, 저장 프로퍼티인지 등)는 따로 신경쓰지 않는다.`

- 프로토콜을 채택한 타입은 `프로토콜이 요구하는 프로퍼티의 이름과 타입만 맞도록 구현해주면 된다.`

    - 다만 `프로퍼티를 읽기 전용으로 할지 혹은 읽고 쓰기가 모두 가능하게 할지는 프로토콜이 정해야 한다.`
    
- 만약 `프로토콜이 '읽고 쓰기가 가능한 프로퍼티를 요구'한다면 '읽기만 가능한 상수 저장 프로퍼티 또는 읽기 전용 연산 프로퍼티를 구현할 수 없다.'`

- 만약 `프로토콜이 '읽기 가능한 프로퍼티를 요구'한다면 타입에 프로퍼티를 구현할 때 '상수 저장 프로퍼티나 읽기 전용 연산 프로퍼티를 포함해서 어떤 식으로든 프로퍼티를 구현할 수 있다.'`

- `쓰기만 가능한 프로퍼티는 없으니 타입에 구현해주는 프로퍼티는 무엇이 되어도 상관없다.`

- `프로토콜의 프로퍼티 요구사항은 항상 'var' 키워드를 사용한 변수 프로퍼티로 정의한다.`

    - `'읽기와 쓰기'가 모두 가능한 프로퍼티는 프로퍼티의 정의 뒤에 '{ get set }'이라고 명시한다.`
    
    - `'읽기 전용' 프로퍼티는 프로퍼티의 정의 뒤에 '{ get }'이라고 명시한다.`
  
<img width="1058" alt="ProtocolExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-1.png?raw=true">

- 위의 코드의 `SomeProtocol에 정의된 'settableProperty'는 '읽기와 쓰기 모두를 요구'했다.`

- `SomeProtocol에 정의된 'notNeedToBeSettableProperty'는 '읽기만 가능하다면 어떻게 구현되어도 상관없다는 요구사항'이다.`

- `타입 프로퍼티를 요구하려면 'static' 키워드를 사용한다.`

- `클래스의 '타입 프로퍼티'에는 '상속 가능한 타입 프로퍼티'인 'class 타입 프로퍼티'와 '상속 불가능한' 'static 타입 프로퍼티'가 있다.`

    - `이 두 타입(class, static) 프로퍼티를 따로 구분하지 않고 모두 'static' 키워드를 사용하여 타입 프로퍼티를 요구하면 된다.`
    
- `AnotherProtocol에 정의된 someTypeProperty와 anotherTypeProperty는 모두 '타입 프로퍼티'를 요구한다.`

<img width="1058" alt="ProtocolExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-2.png?raw=true">

- 위의 코드의 `Sendable 프로토콜`은 무언가의 전송을 가능하게 하기 위한 `프로퍼티인 from과 to를 요구`한다.

    - 그래서 `Sendable 프로토콜을 채택하여 준수`하는 `Message와 Mail 클래스`는 `모두 from과 to 프로퍼티를 갖는다.`

- 다만 `Message 클래스의 from 프로퍼티는 '읽기 전용 연산 프로퍼티'`라는 점이 `Mail 클래스의 from 프로퍼티와 다를 뿐이다.`

- `Sendable 프로토콜에서 요구한 프로퍼티는 '읽기 가능한 프로퍼티'였지만 실제로 프로토콜을 채택한 클래스에서 '구현할 때는 읽고 쓰기가 가능한 프로퍼티로 구현해도 문제가 없다.'`

- - -

### 메서드 요구

- `프로토콜은 특정 '인스턴스 메서드'나 '타입 메서드'를 '요구할 수도 있다.'`

- `프로토콜이 요구할 메서드는 프로토콜 정의에서 작성한다.`

- 다만 `메서드의 '실제 구현부인 중괄호({}) 부분은 제외'하고 '메서드의 이름, 매개변수, 반환 타입 등만 작성하며 가변 매개변수도 허용'한다.`

- `프로토콜의 메서드 요구에서는 '매개변수 기본값을 지정할 수 없다.'`

- `'타입 메서드를 요구'할 때는 타입 프로퍼티와 마찬가지로 앞에 'static' 키워드를 명시한다.`

- `'static' 키워드를 사용하여 '요구한 타입 메서드를 클래스에서 실제 구현할 때'는 'static' 키워드나 'class' 키워드 '어느 쪽을 사용해도 무방'하다.`

<img width="1254" alt="ProtocolExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-3.png?raw=true">

<img width="1254" alt="ProtocolExampleImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-4.png?raw=true">

<img width="1254" alt="ProtocolExampleImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-5.png?raw=true">

<img width="1254" alt="ProtocolExampleImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-6.png?raw=true">

- 위의 코드의 `Receiveable 프로토콜은 수신받을 수 있는 'received(data:from:) 메서드를 요구'한다.`

- `Sendable 프로토콜은 데이터를 발신할 수 있는 'Sendable 프로토콜 타입의 인스턴스를 할당할 수 있는 from 프로퍼티'와 데이터를 수신할 수 있는 'Receiveable 프로토콜 타입의 인스턴스를 할당할 수 있는 to 프로퍼티를 요구'한다.`

    - 또, `데이터를 발신하는 '메서드인 send(data:) 인스턴스 메서드를 요구'하며, 전달받은 인스턴스가 발신 가능한 상태인지를 확인하는 'isSendableInstance(_:) 타입 메서드를 요구'한다.`
    
- `Message와 Mail 클래스는 Sendable과 Receiveable 프로토콜을 준수한다.`

    - 그래서 `'두 프로토콜(Sendable과 Receiveable)'에서 '요구하는 프로퍼티와 메서드를 모두 구현'해야 한다.`
    
- `두 프로토콜(Sendable과 Receiveable)에서 '요구한 프로퍼티와 메서드 각각의 이름과 타입은 같지만 실제 클래스에서 구현해줄 때는 조금 다른 동작과 용도로 구현하기도 한다.'`

- `Mail과 Message 클래스의 'isSendableInstance(_:) 메서드'는 '각각 class와 static 타입 메서드로 구현'했다.`

- `'프로토콜에서 static 키워드를 통해 타입 메서드를 요구'했지만 '클래스에서 실제로 구현할 때 class 타입 메서드로 구현할지, static 타입 메서드로 구현할지는' 프로토콜을 채택하여 '사용하는 클래스의 특성에 따라 골라 사용해주면 된다.'`

- - -

### 타입으로서의 프로토콜

- `프로토콜은 요구만 하고 스스로 기능을 구현하지는 않는다. 그렇지만 '프로토콜은 코드에서 완전한 하나의 타입으로 사용되기에 여러 위치에서 프로토콜을 타입으로 사용할 수 있다.'`

    - `1) 함수, 메서드, 이니셜라이저에서 매개변수(Parameter) 타입이나 반환(Return) 타입으로 사용될 수 있다.`
    
    - `2) 프로퍼티, 변수, 상수 등의 타입으로 사용될 수 있다.`
    
    - `3) 배열, 딕셔너리 등 컨테이너 요소의 타입으로 사용될 수 있다.`
    
- 프로토콜은 스위프트의 다른 타입들과 마찬가지로 이름을 정할 때 `대문자 카멜케이스를 사용`한다.

- - -