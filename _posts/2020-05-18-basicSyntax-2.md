---
layout: post
title:  "기본 문법 공부(타입 캐스팅(Type Casting) - 기존 언어의 타입 변환과 스위프트의 타입 변환)"
date:   2020-05-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Type Casting Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-TypeCastingExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

- - -
- - -

### 기존 언어의 타입 변환과 스위프트의 타입 변환

- 스위프트는 데이터 타입 안전을 위하여 각기 다은 타입끼리의 값 교환을 엄격히 제한한다.

    - 또, 다른 프로그래밍 언어에서 대부분 지원하는 암시적 데이터 타입 변환(Implicit Type Conversion)은 지원하지 않는다.
    
- C 언어의 경우 데이터 타입 변환을 통해 손쉽게 다른 데이터 타입으로 변환해줄 수 있었다.

    - 예를 들어 int num = (int)2.3f; 과 같이 표현하거나 int num = 2.3f; 처럼 표현하여 데이터 타입을 변환할 수 있었다.
    
- 스위프트에서 Int(2.3)처럼 부동소수 타입을 정수 타입의 값으로 변환해주는 형태와 C 언어의 데이터 타입 변환의 형태는 크게 다를 것 없어 보이지만 사실은 사뭇 다르다.

```swift
// C 언어와 스위프트의 데이터 타입 변환 비교

// C
double value = 3.3
int convertedValue = (int)value
convertedValue = 5.5 // double -> int 암시적 데이터 타입 변환

// Swift
var value: Doule = 3.3
var convertedValue: Int = Int(value)
convertedValue = 5.5 // Error !!

```

- C 언어 코드를 살펴보면 부동소수 타입인 double에서 정수 타입인 int로 데이터 타입을 변경했다.

    - C 언어에서는 이를 타입 변환이라고 말한다.
    
- 그러나 스위프트 코드를 보면 Int(value)라는 형태로 데이터 타입의 형태를 변경해주는데, 이는 이니셜라이저(Initializer)이다.

    - 즉, 기존 값을 전달인자로 받는 이니셜라이저를 통해 새로운 Int 구조체의 인스턴스를 생성하는 것이다.
    
    - 스위프트에서는 이를 타입 변환 혹은 타입 캐스팅이라고 칭하지 않는다.
    
        - 다만 이니셜라이저를 통해 새로운 인스턴스를 생성하는 과정이다.
        
    - 그래서 Int 구조체의 정의를 들여다보면 다양한 이니셜라이저가 정의되어 있음을 확인할 수 있다.
    
<img width="1058" alt="TypeCastingExampleImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-1.png?raw=true" title="TypeCastingExampleImg-1">

- 위의 그림은 Int 구조체의 다양한 이니셜라이저 정의를 나타내고 있다. (위의 그림은 Int의 이니셜라이저 정의의 전체가 아니고 맨 앞부분만 발췌해 낸 것이다.)

- Int의 이니셜라이저는 대부분 실패하지 않는 이니셜라이저로 정의되어 있다.

    - 그러나 좀 더 살펴보면 실패 가능한 이니셜라이저도 포함되어 있다.
    
    - StringProtocol 타입을 매개변수로 받는 public convenience init?<S>(_ text: S, radix: Int = default) where S : StringProtocol가 실패 가능한 이니셜라이저이다.
    
        - StringProtocol 타입의 데이터 text를 Int 타입으로 변경할 때, 적절하지 못한 매개변수가 전달된다면 새로운 인스턴스가 생성되지 않을 수 있다는 뜻이다.
        
<img width="1058" alt="TypeCastingExampleImg-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-2.png?raw=true" title="TypeCastingExampleImg-2">