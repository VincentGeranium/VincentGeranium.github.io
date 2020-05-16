---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 이니셜라이저 자동 상속(Automatic Initializer Inheritance))"
date:   2020-05-16
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Automatic Initializer Inheritance Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-16-AutomaticInitializerInheritanceExampleCode-1.playground)

- [Automatic Initializer Inheritance Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-16-AutomaticInitializerInheritanceExampleCode-2.playground)

- [Automatic Initializer Inheritance Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-16-AutomaticInitializerInheritanceExampleCode-3.playground)

- [Automatic Initializer Inheritance Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-16-AutomaticInitializerInheritanceExampleCode-4.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -
- - -

### 이니셜라이저 자동 상속 (Automatic Initializer Inheritance)

- 기본적으로 스위프트의 이니셜라이저는 부모클래스의 이니셜라이저를 상속(Inheritance)받지 않는다.

    - 그러나 특정 조건에 부합한다면 부모클래스의 이니셜라이저가 자동으로 상속된다.
    
- 사실, 대부분의 경우 자식클래스에서 이니셜라이저를 재정의(Override)해줄 필요가 없다.

- 자식클래스에서 프로퍼티 기본값을 모두 제공한다고 가정할 때, 다음 두 가지 규칙에 따라 이니셜라이저가 자동으로 상속된다.

    - 규칙 1. 자식클래스에서 별도의 지정 이니셜라이저(Designated Initializer)를 구현하지 않는다면, 부모클래스의 지정 이니셜라이저가 자동으로 상속된다.
    
    - 규직 2. 만약 규칙 1에 따라 자식클래스에서 부모클래스의 지정 이니셜라이저를 자동으로 상속받은 경우 또는 부모클래스의 지정 이니셜라이저를 모두 재정의하여 부모클래스와 동일한 지정 이니셜라이저를 모두 사용할 수 있는 상황이라면 부모클래스의 편의 이니셜라이저(Convenience Initializer)가 모두 자동으로 상속된다.

<img width="1058" alt="AutomaticInitializerInheritanceImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AutomaticInitializerInheritanceImg-1.png?raw=true" title="AutomaticInitializerInheritanceImg-1">

- 위의 코드를 살펴보면 Student의 major 프로퍼티에 기본값(Property Default Value)이 있으며, 따로 지정 이니셜라이저(Designated Initializer)를 구현해주지 않았으므로 부모클래스인 Person 클래스의 지정 이니셜라이저가 자동으로 상속된다.

    - 이는 규칙 1에 부합한다.
    
- 부모클래스의 지정이니셜라이저를 모두 자동으로 상속받았으므로 편의 이니셜라이저(Convenience Initializer)도 자동으로 상속되었다.    

<img width="1058" alt="AutomaticInitializerInheritanceImg-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AutomaticInitializerInheritanceImg-2.png?raw=true" title="AutomaticInitializerInheritanceImg-2">

- 위의 코드를 보면 Student 클래스의 major 프로퍼티에 기본값이 없더라도 이니셜라이저에 적절히 초기화했고, 부모클래스의 지정 이니셜라이저를 모두 재정의하여 부모클래스의 지정 이니셜라이저와 동일한 이니셜라이저를 모두 사용할 수 있는 상황이므로 규칙 1에 부합한다.

    - 따라서 부모클래스의 편의 이니셜라이저가 자동으로 상속되었다.
    
- 자동 상속 규칙은 자식클래스에 편의 이니셜라이저를 추가한다고 하더라도 유효하다.

    - 또, 부모클래스의 지정 이니셜라이저를 자식클래스의 편의 이니셜라이저로 구현하더라도 규칙 2를 충족한다.
    
<img width="1058" alt="AutomaticInitializerInheritanceImg-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AutomaticInitializerInheritanceImg-3.png?raw=true" title="AutomaticInitializerInheritanceImg-3">    

- 위의 코드에서는 Student 클래스에서 부모클래스 Person의 지정 이니셜라이저인 init(name:)을 편의 이니셜라이저로 재정의했지만 부모의 지정 이니셜라이저를 모두 사용할 수 있는 상황인 규칙 2에 부합하므로 부모클래스의 편의 이니셜라이저를 사용할 수 있다.

    - 또, 자신만의 편의 이니셜라이저인 convenience init(major:)를 구현해주었지만 편의 이니셜라이저 자동 상속에는 아무런 영향을 미치지 않는다.
    
<img width="1058" alt="AutomaticInitializerInheritanceImg-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/AutomaticInitializerInheritanceImg-4.png?raw=true" title="AutomaticInitializerInheritanceImg-4">    

- 위의 코드를 보면 Student 클래스를 상속받은 UniversityStudent 클래스는 grade 프로퍼티에 기본값이 있으며, 별도의 지정 이니셜라이저를 구현해주지 않았으므로 규칙 1에 부합한다.

    - 따라서 부모클래스의 이니셜라이저를 모두 자동 상속받는다.
    
    - 게다가 자신만의 편의 이니셜라이저를 구현했지만 자동 상속에는 영향을 미치지 않는다.
    
- 결과적으로 UniversityStudent 클래스는 상속받은 이니셜라이저와 자신의 편의 이니셜라이저들을 모두 사용할 수 있다.

- - -
- - -