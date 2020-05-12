---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 프로퍼티 감시자 재정의(Overriding Property Observers))"
date:   2020-05-12
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 6](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-12-InheritanceExampleCode-6.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 프로퍼티 감시자 재정의 (Overriding Property Observers)

- 프로퍼티 감시자(Property Observers)도 프로퍼티의 접근자(Getter)와 설정자(Setter)처럼 재정의(Override)할 수 있다.

    - 조상클래스에 정의한 프로퍼티가 연산 프로퍼티인지 저장 프로퍼티인지는 상관 없다.
    
- 상수 저장 프로퍼티(Constant Stored Property)나 읽기 전용 연산 프로퍼티(Read-Only Computed Property)는 프로퍼티 감시자(Property Observer)를 재정의 할 수 없다

    - 상수 저장 프로퍼티나 읽기 전용 연산 프로퍼티는 값을 설정할 수 없으므로 willSet이나 didSet 메서드를 사용한 프로퍼티 감시자를 원천적으로 사용할 수 없기 때문이다.
    
- 프로퍼티 감시자를 재정의하더라도 조상클래스에 정의한 프로퍼티 감시자도 동작한다.

- 프로퍼티의 접근자와 프로퍼티 감시자는 동시에 재정의할 수 없다.

    - 만약 둘 다 동작하길 원한다면 재정의하는 접근자에 프로퍼티 감시자의 역활을 구현해야 한다.
    
<img width="1058" alt="inheritanceImage-8" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-8.png?raw=true" title="inheritanceImage-8">
<img width="1058" alt="inheritanceImage-9" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-9.png?raw=true" title="inheritanceImage-9">

- 위 코드의 Student 클래스에서는 Person 클래스의 age라는 저장 프로퍼티의 프로퍼티 감시자를 재정의해주었다.

- 위 코드의 Student 클래스에서는 Person 클래스의 koreanAge와 fullName이라는 연산 프로퍼티의 프로퍼티 감시자를 재정의해주었다.

- Person 클래스의 age라는 저장 프로퍼티에 이미 프로퍼티 감시자를 정의했으므로 ron의 age 프로퍼티의 값을 할당할 때는 Person에 정의한 프로퍼티 감시자와 Student에 정의한 프로퍼티 감시자가 모두 동작한다.

- 기존에 연산 프로퍼티로 정의했던 fullName 프로퍼티에도 프로퍼티 감시자를 정의했다.

- 그러나 koreanAge 프로퍼티에는 프로퍼티 감시자와 프로퍼티 설정자를 동시에 정의할 수 없다, 위 코드의 Error Messege를 보면 알 수 있다.