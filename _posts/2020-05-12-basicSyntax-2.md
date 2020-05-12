---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 서브스크립트 재정의(Overriding Subscript))"
date:   2020-05-12
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 7](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-12-InheritanceExampleCode-7.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 서브스크립트 재정의 (Overriding Subscript)

- 서브스크립트도 메서드와 마찬가지로 재정의가 가능하다.

- 서브스크립트도 매개변수와 반환 타입이 다르면 다른 서브스크립트로 취급하므로, 자식클래스에서 재정의하려는 서브스크립트라면 부모클래스 서브스크립트의 매개변수와 반환 타입이 같아야 한다.

<img width="1058" alt="inheritanceImage-10" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-10.png?raw=true" title="inheritanceImage-10">
<img width="1058" alt="inheritanceImage-11" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-11.png?raw=true" title="inheritanceImage-11">

- - -
- - -
