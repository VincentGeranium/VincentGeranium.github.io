---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 프로퍼티 재정의(Overriding Properties))"
date:   2020-05-11
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 5](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-11-InheritanceExampleCode-5.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 프로퍼티 재정의 (Overriding Properties)

- `메서드와 마찬가지로 부모클래스로부터 상속받은 인스턴스 프로퍼티(Instance Property)나 타입 프로퍼티(Type Property)를 자식클래스에서 용도에 맞게 재정의(Override)할 수 있다.`

- `프로퍼티를 재정의할 때는 저장 프로퍼티(Stored Property)로 재정의할 수는 없다.`

- `프로퍼티를 재정의한다는 것은 프로퍼티 자체가 아니라 프로퍼티의 접근자(Getter), 설정자(Setter), 프로퍼티 감시자(Property Observer)등을 재정의하는 것을 의미한다.`

- `조상클래스에서 저장 프로퍼티(Stored Property)로 정의한 프로퍼티는 물론이고 연산 프로퍼티(Computed Property)로 정의한 프로퍼티도 접근자(Getter)와 설정자(Setter)를 재정의할 수 있다.`

    - **프로퍼티를 상속받은 자식클래스에서는 조상클래스의 프로퍼티 종류(저장, 연산 등)는 알지 못하고 단지 이름과 타입만을 알기 때문이다.**
    
- `재정의하려는 프로퍼티는 조상클래스 프로퍼티의 이름과 타입이 일치해야 한다.`

    - **만약 조상클래스에 없는 프로퍼티를 재정의하려고 한다면 메서드와 마찬가지로 컴파일 오류가 발생한다.**
    
- `조상클래스에서 읽기 전용(read-only, get only) 프로퍼티였다라도 자식클래스에서 읽고 쓰기(read-write, get-set)가 가능한 프로퍼티로 재정의해줄 수도 있다.`

    - **그러나, 읽기 쓰기(read-write, get-set) 모두 가능했던 프로퍼티를 읽기 전용(read-only, get only)으로 재정의해줄 수는 없다.**
    
- `읽기 쓰기가 모두 가능한 프로퍼티를 재정의할 때 설정자(Setter)만 따로 재정의할 수는 없다.`

    - **즉, 접근자(Getter)와 설정자(Setter)를 모두 재정의해야 한다.**
    
- `만약 접근자(Getter)에 따로 기능 변경이 필요 없다면 super.someProperty와 같은 식으로 부모클래스의 접근자(Getter)를 사용하여 값을 받아와 반환해주면 된다.`

<img width="1058" alt="inheritanceImage-7" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-7.png?raw=true" title="inheritanceImage-7">

- `위 코드의 Student 클래스에서는 Person 클래스에서 상속받은 introduction과 koreanAge라는 연산 프로퍼티(Computed Property)를 재정의했다.`

    - `읽기 전용(read-only, get only)이었던 koreanAge 프로퍼티는 읽기와 쓰기(read-write, get-set)가 모두 가능하도록 재정의했다.`
    
    - `introduction은 학생의 학점 정보를 추가하도록 재정의했다.`