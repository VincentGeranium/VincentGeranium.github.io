---
layout: post
title:  "기본 문법 공부(확장(expansion) - 익스텐션(Extensions)으로 추가할 수 있는 기능 - 연산 프로퍼티)"
date:   2020-05-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Extension Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-06-ExtensionExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html)

- - -
- - -

### 익스텐션(Extension)으로 추가할 수 있는 기능 - 연산 프로퍼티(Computed Property)

- `익스텐션을 통해서 타입에 연산 프로퍼티를 추가할 수 있다.`

<img width="1058" alt="extensionExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/extensionExampleImage-1.png?raw=true" title="extensionExampleImage-1">

- `위 코드의 익스텐션은 Int 타입에 두 개의 연산 프로퍼티를 추가한 것이다.`

    - Int 타입의 인스턴스가 홀수인지 짝수인지 판별하여 Bool 타입으로 알려주는 연산 프로퍼티이다.
    
- `익스텐션으로 Int 타입에 추가해준 연산 프로퍼티는 Int 타입의 어떤 인스턴스에도 사용이 가능하다.`

- `위의 코드처럼 인스턴스 연산 프로퍼티(Instance Computed Property)를 추가할 수도 있으며, static 키워드를 사용하여 타입 연산 프로퍼티(Type Computed Property)도 추가할 수 있다.`

- `익스텐션(Extension)으로 연산 프로퍼티(Computed Property)를 추가할 수는 있지만, 저장 프로퍼티(Stored Property)는 추가할 수 없다. 또, 타입에 정의되어 있는 기존 프로퍼티에 프로퍼티 감시자(Property Observer)를 추가할 수 없다.`

- - -
- - -