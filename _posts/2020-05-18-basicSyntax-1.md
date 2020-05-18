---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 요구 이니셜라이저(Required Initializer))"
date:   2020-05-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Required Initializer Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-RequiredInitializerExampleCode-1.playground)

- [Required Initializer Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-RequiredInitializerExampleCode-2.playground)

- [Required Initializer Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-18-RequiredInitializerExampleCode-3.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -
- - -

### 요구 이니셜라이저 (Required Initializer)

- required 수식어를 클래스의 이니셜라이저 앞에 명시해주면 이 클래스를 상속받은 자식클래스에서 반드시 해당 이니셜라이저를 구현해주어야 한다.

    - 다시 말하면 상속받을 때 반드시 재정의해야 하는 이니셜라이저 앞에 required 수식어를 붙여준다.
    
    - 다만 자식클래스에서 요구 이니셜라이저를 재정의할 때는 override 수식어 대신에 required 수식어를 사용한다.
    
<img width="1058" alt="RequiredInitializerImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/RequiredInitializerImg-1.png?raw=true" title="RequiredInitializerImg-1"> 

- 위의 코드를 살펴보면 Person 클래스에 init() 요청 이니셜라이저(required initializer)를 구현해주었지만, Person 클래스를 상속받은 Student 클래스에는 요구 이니셜라이저를 구현하지 않았다.

    - 이는 Student 클래스의 major 프로퍼티에 기본값이 있으며 별다른 지정 이니셜라이저(Designated Initializer)가 없기 때문에 이니셜라이저가 자동으로 상속된 것이다.
    
- 만약 Student 클래스에 새로운 지정 이니셜라이저를 구현한다면 부모클래스로부터 이니셜라이저가 자동으로 상속되지 않으므로 요구 이니셜라이저를 구현해주어야 한다.

<img width="1058" alt="RequiredInitializerImg-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/RequiredInitializerImg-2.png?raw=true" title="RequiredInitializerImg-2">

- 위의 코드를 보면 Student와 UniversityStudent 클래스는 자신만의 지정 이니셜라이저(Designated Initializer)를 구현했다.

    - 그래서 부모클래스의 이니셜라이저를 자동 상속받지 못한다.
    
    - 그래서 Person 클래스에 정의한 요구 이니셜라이저(Required Initializer)를 이니셜라이저 자동 상속 규칙에 부합하지 않는 자식클래스인 Student에도 구현해주고, 그 자식클래스인 UniversityStudent 클래스에도 구현해주어야 한다.
    
- 이니셜라이저 자동 상속의 규칙에 부합하지 않는 한, 요구 이니셜라이저는 반드시 구현해주어야 한다.

- 부모클래스의 일반 이니셜라이저를 자신의 클래스부터 요구 이니셜라이저로 변경할 수도 있다.

    - 그럴 때는 required override를 명시해주어 재정의됨과 동시에 요구 이니셜라이저가 될 것임을 명시해주어야 한다.
    
- 또, 편의 이니셜라이저(Convenience Initializer)도 요구 이니셜라이저(Required Initializer)로 변경될 수 있다.

    - 그럴 때는 required convenience를 명시해주어 편의 이니셜라이저(Convenience Initializer)가 앞으로 요구될 것임을 명시해주면 된다.
    
<img width="1058" alt="RequiredInitializerImg-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/RequiredInitializerImg-3.png?raw=true" title="RequiredInitializerImg-3">

- 위의 코드에서 Person 클래스에는 별다른 요구 이니셜라이저(Required Initializer)가 없다.

    - 다만 Student 클래스에서 Person의 init() 이니셜라이저를 재정의하면서 요구 이니셜라이저(Required Initializer)로 변경했다.
    
    - 따라서 UniversityStudent 클래스에서는 init() 이니셜라이저를 요구 이니셜라이저(Required Initializer)로 필히 구현해주어야 한다.
    
    - 또, Student 클래스의 편의 이니셜라이저(Convenience Initializer) init(name:)이 요구 이니셜라이저(Required Initializer)로 지정되었기 때문에 UniversityStudent 클래스에서 다시 구현해주어야 한다.