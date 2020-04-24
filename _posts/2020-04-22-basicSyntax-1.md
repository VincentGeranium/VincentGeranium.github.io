---
layout: post
title:  "기본 문법 공부(프로토콜(protocol) - 프로토콜의 상속과 클래스 전용 프로토콜, 프로토콜 조합과 프로토콜 준수 확인, 프로토콜 캐스팅)"
date:   2020-04-22
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Protocol Example Code - 5](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-22-ProtocolExampleCode-5.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

- - -

### 프로토콜의 상속과 클래스 전용 프로토콜

- `프로토콜은 하나 이상의 프로토콜을 상속받아 기존 프로토콜의 요구사항보다 더 많은 요구사항을 추가할 수 있다.`

- `프로토콜 상속 문법은 클래스의 상속 문법과 유사하다.`

<img width="1058" alt="ProtocolExampleImage-13" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-13.png?raw=true">

- ReadSpeakable 프로토콜은 Readable 프로토콜을 상속받았다.

- ReadWriteSpeakable 프로토콜은 Readable과 Writeable 프로토콜을 상속받았다.

- ReadWriteSpeakable 프로토콜을 채택(Adopted)한 SomeClass는 세 프로토콜(Readable, Writeable, ReadWriteSpeakable)이 요구하는 read(), write(), speak() 메서드를 모두 구현해야 한다.

<img width="1058" alt="ProtocolExampleImage-14" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-14.png?raw=true">

- 프로토콜 상속 리스트에 'class' 키워드를 추가해 프로토콜이 클래스 타입에만 채택될 수 있도록 제한할 수도 있다.

- 클래스 전용 프로토콜로 제한을 주기 위해서는 '프로토콜의 상속 리스트 맨 처음에 class 키워드'가 위치해야 한다.

- - -

### 프로토콜 조합과 프로토콜 준수 확인

<img width="1058" alt="ProtocolExampleImage-15" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-15.png?raw=true">
<img width="1058" alt="ProtocolExampleImage-16" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-16.png?raw=true">

- 하나의 매개변수(Parameter)가 여러 프로토콜을 모두 준수하는 타입이어야 한다면 하나의 매개변수에 여러 프로토콜을 한 번에 조합(Composition)하여 요구할 수 있다.

    - 프로토콜을 조합하여 요구할 때는 'SomeProtocol & AnotherProtocol'과 같이 표현한다

- 하나의 매개변수가 프로토콜을 둘 이상 요구할 수도 있다.

    - 이때도 마찬가지로 앰퍼샌드(&)를 여러 프로토콜 이름 사이에 써주면 된다.
    
- 더불어 특정 클래스의 인스턴스 역활을 할 수 있는지 함께 확인할 수 있다.

    - 구조체나 열거형 타입은 조합할 수 없다.
    
    - 조합 중 클래스 타입은 한 타입만 조합할 수 있다.
    
- - -

### 프로토콜 캐스팅

<img width="1058" alt="ProtocolExampleImage-17" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ProtocolExampleImage-17.png?raw=true">

- 타입캐스팅에 사용하던 'is와 as 연산자'를 통해 대상이 프로토콜을 준수하는지 확인할 수도 있고, 특정 프로토콜로 캐스팅할 수도 있다.

- 프로토콜을 준수하는지 확인하거나 다른 프로토콜로 캐스팅하는 방법은 타입캐스팅 방법과 똑같다.

    - is 연산자를 통해 해당 인스턴스가 특정 프로토콜을 준수하는지 확인할 수 있다.
    
    - as? 다운캐스팅 연산자를 통해 다른 프로토콜로 다운캐스팅을 시도해볼 수 있다.
    
    - as! 다운캐스팅 연산자를 통해 다른 프로콜로로 강제 다운캐스팅을 할 수 있다.
    
- '프로토콜 조합과 프로토콜 준수 확인'의 코드에 이어 '프로토콜 캐스팅'의 코드를 작성해보면 데이터 타입의 타입캐스팅과 똑같다는 것을 확인할 수 있다.

    - 프로토콜도 하나의 타입이므로 당연하다.
    
- - -    