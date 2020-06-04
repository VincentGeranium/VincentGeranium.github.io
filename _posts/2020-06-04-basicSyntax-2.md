---
layout: post
title:  "기본 문법 공부(확장(expansion) - 제네릭 서브스크립트(Generic Subscripts))"
date:   2020-06-04
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Generic Subscripts Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-04-GenericSubscriptsExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -
- - -

### 제네릭 서브스크립트(Generic Subscripts)

- 제네릭 함수(메서드)를 구현할 수 있었던 것처럼 **서브스크립트도 제네릭을 활용하여 타입에 큰 제한 없이 유연하게 구현할 수 있다.**

- **물론 타입 제약을 사용하여 제네릭을 활용하는 타입에 제약을 줄 수도 있다.**

<img width="1058" alt="GenericSubscriptsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/GenericSubscriptsImage-1.png?raw=true" title="GenericSubscriptsImage-1">

- 위의 코드에서 Stack 구조체의 익스텐션으로 서브스크립트를 추가했다.

    - **서브스크립트는 Indices라는 플레이스홀더를 사용하여 매개변수를 제네릭하게 받아들일 수 있다.**
    
        - Indices는 Sequence 프로토콜을 준수하는 타입으로 제약이 추가되어 있다.
    
        - 또, Indices 타입 Iterator의 타입이 Int 타입이어야 하는 제약이 추가되었다.
        
        - 서브스크립트는 이 Indices 타입의 indices라는 매개변수로 인덱스 값을 받을 수 있다.
    
        - 그 결과 indices 시퀀스의 인덱스 값에 해당하는 스택 요소의 값을 배열로 반환한다.

- - -
- - -