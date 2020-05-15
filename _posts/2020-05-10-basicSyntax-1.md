---
layout: post
title:  "기본 문법 공부(확장(expansion) - 익스텐션(Extensions)으로 추가할 수 있는 기능 - 메서드)"
date:   2020-05-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Extension Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-10-ExtensionExampleCode-2.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html)

- - -
- - -

### 익스텐션(Extension)으로 추가할 수 있는 기능 - 메서드(Method)

- `익스텐션은 통해 타입에 메서드(Method)를 추가할 수 있다.`

<img width="1058" alt="extensionExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/extensionExampleImage-2.png?raw=true" title="extensionExampleImage-2">
<img width="1058" alt="extensionExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/extensionExampleImage-3.png?raw=true" title="extensionExampleImage-3">
<img width="1058" alt="extensionExampleImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/extensionExampleImage-4.png?raw=true" title="extensionExampleImage-4">

- 위의 코드에서는 `익스텐션을 통해 Int 타입에 여러 종류의 메서드를 추가했다.`

- `인스턴스 메서드인 multiply(by:) 메서드, 가변 메서드인 multiplySelf(by:) 메서드, 타입 메서드인 isIntTypeInstance(_:) 메서드를 추가했다.`

- 또, `익스텐션을 통해 Position 구조체 타입에 사용할 연산자(타입 메서드)를 추가해줄 수도 있다.`

- `Position의 익스텐션처럼 여러 기능을 여러 익스텐션 블록으로 나눠서 구현해도 전혀 문제가 없다.`

    - `관련 기능별로 하나의 익스텐션 블록에 묶어주는 것도 좋다.`
    
- - -
- - -