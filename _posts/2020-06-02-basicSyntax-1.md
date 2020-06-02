---
layout: post
title:  "기본 문법 공부(확장(expansion) - 제네릭 타입 확장(Extending a Generic Type))"
date:   2020-06-02
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Extending a Generic Type Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-03-ExtendingAGenericTypesExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -
- - -

### 제네릭 타입 확장(Extending a Generic Type)

- 만약 익스텐션을 통해 제네릭을 사용하는 타입에 기능을 추가하고자 한다면 익스텐션 정의에 타입 매개변수를 명시하지 않는다.

    - 대신 원래 제네릭 정의에 명시한 타입 매개변수를 익스텐션에서 사용할 수 있다.
    
<img width="1058" alt="extendingAgenericTypeImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/extendingAgenericTypeImage-1.png?raw=true" title="extendingAgenericTypeImage-1">

- 위의 코드는 Stack 구조체를 확장한 것이다.

    - Stack은 제네릭 타입이지만 익스텐션의 정의에는 따로 타입 매개변수를 명시해주지 않았다.
    
    - 대신 기존의 제네릭 타입에 정의되어 있는 Element라는 타입을 사용할 수 있다.