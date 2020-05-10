---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 상속, 기반클래스(Base Class), 자식클래스(SubClass - Child Class), 부모클래스(Superclass - Parents Class))"
date:   2020-05-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-10-InheritanceExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 상속 (Inheritance)

- 클래스는 메서드나 프로퍼티 등을 다른 클래스로부터 상속(Inheritance)받을 수 있다.

- 어떤 클래스로부터 상속을 받으면 상속받은 클래스는 그 어떤 클래스의 자식클래스(SubClass, Child - Class)라고 표현한다.

- 자식클래스에게 자신의 특성을 물려준 클래스를 부모클래스(Superclass, Parents - Class)라고 표현한다.

- 상속은 스위프트의 다른 타입과 클래스를 구별 짓는 클래스만의 특징이다.

- 스위프트의 클래스는 부모클래스로부터 물려받은 메서드를 호출할 수 있고 프로퍼티에 접근할 수 있으며 서브스크립트도 사용할 수 있다.

    - 부모클래스로부터 물려받은 메서드, 프로퍼티, 서브스크립트 등을 자신만의 내용으로 재정의할 수도 있다.
    
- 스위프트는 부모클래스의 요소를 자식클래스애서 정의할 때 자식클래스가 부모클래스의 오소들을 재정의한다는 것을 명확히 확인해 줘야 한다.   

- 상속받은 프로퍼티에 프로퍼티의 값이 변경되었을 때 알려주는 프로퍼티 감시자도 구현할 수 있다.

- 연산 프로퍼티를 정의해준 클래스에서는 연산 프로퍼티에 프로퍼티 감시자를 구현 할 수 없지만, 부모클래스에서 연산 프로퍼티로 정의한 프로퍼티든 저장 프로퍼티로 정의한 프로퍼티든 자식클래스에서는 프로퍼티 감시자를 구현할 수 있다.

- 다른 클래스로부터 상속을 받지 않은 클래스를 기반클래스(Base Class)라고 부른다.

    - 어떤 클래스로부터 상속받지 않고 생성한 대부분의 클래스를 기반클래스로 생각해도 무방하다.
    
<img width="1058" alt="inheritanceImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-1.png?raw=true" title="inheritanceImage-1">

- - -
- - -