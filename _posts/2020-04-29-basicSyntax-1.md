---
layout: post
title:  "기본 문법 공부(확장(expansion) - 복수 서브스크립트, 서브스크립트 마무리(Subscript))"
date:   2020-04-29
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Subscript Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-29-SubscriptExampleCode-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Subscripts.html)

- - -

### 복수 서브스크립트

- **하나의 타입이 여러 개의 서브스크립트를 가질 수도 있다.**

    - **다양한 매개변수 타입을 사용하여 서브스크립트를 구현하면 여러 용도로 서브스크립트를 사용할 수 있다는 뜻이다.**
    
<img width="1058" alt="subscriptImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/subscriptImage-2.png?raw=true">
<img width="1058" alt="subscriptImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/subscriptImage-3.png?raw=true">

- `위의 코드의 School 클래스에 총 3개의 스크립트를 정의했다.`

    - **두 개의 읽고 쓰기 가능한 서브스크립트와 하나의 읽기 전용 서브스크립트고 각각의 서브스크립트는 매개변수 타입과 개수, 반환 타입이 모두 다르다.**
    
        - `첫 번째 서브스크립트는 학생의 번호를 전달받아 해당하는 학생이 있다면 Student 인스턴스를 반환하거나 특정 번호에 학생을 할당하는 서브스크립트이다.`
        
        - `두 번째 서브스크립트는 학생의 이름을 전달받아 해당하는 학생이 있다면 번호를 반환하거나 특정 이름의 학생을 해당 번호에 할당하는 서브스크립트이다.`
        
        - `세 번째 서브스크립트는 이름과 번호를 전달받아 해당하는 학생이 있다면 해당하는 학생을 찾아서 Student 인스턴스를 반환한다.`
        
- - -

### 서브스크립트 마무리

- **서브스크립트 Summary 시리즈에 나오는 모든 예시들처럼 서브스크립트는 메서드인듯 아닌듯, 연산 프로퍼티인듯 아닌듯 중간 형태를 띠며 인스턴스 이름 뒤에 대괄호만 써서 편리하게 내부 값에 접근하고 설정해줄 수 있다. 또, 다양한 목적으로 구현하는데 용이하다.**

- - -
- - -