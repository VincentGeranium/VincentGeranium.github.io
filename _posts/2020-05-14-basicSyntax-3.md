---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 이니셜라이저 상속 및 재정의(Initializer Inheritance and Overriding))"
date:   2020-05-14
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Initializer Inheritance and Overriding Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-14-InitializerInheritanceAndOverridingExampleCode-1.playground)

- [Initializer Inheritance and Overriding Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-14-InitializerInheritanceAndOverridingExampleCode-2.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -
- - -

### 이니셜라이저 상속 및 재정의 (Initializer Inheritance and Overriding)

- 기본적으로 스위프트의 이니셜라이저는 부모클래스의 이니셜라이저를 상속받지 않는다.

    - 부모클래스로부터 물려받은 이니셜라이저는 자식클래스에 최적화되어 있지 않아서, 부모클래스의 이니셜라이저를 사용했을 때 자식클래스의 새로운 인스턴스가 완전하고 정확하게 초기화되지 않는 상황을 방지하고자 함이다.
    
- 안전하고 적절하다고 판단되는 특정한 상황에서는 부모클래스의 이니셜라이저가 상속되기도 한다.(이니셜라이저 자동 상속)

- 보통 부모클래스의 이니셜라이저와 똑같은 이니셜라이저를 자식클래스에서 사용하고 싶다면 자식클래스에서 부모의 이니셜라이저와 똑같은 이니셜라이저를 구현해주면 된다.

- 부모클래스와 동일한 지정 이니셜라이저를 자식클래스에서 구현해주려면 재정의(Override)하면 된다. 그러려면 override 수식어를 붙여야 한다.

    - 클래스에 주어지는 기본 이니셜라이저를 재정의 할 때도 마찬가지이다.
    
- 자식클래스의 편의 이니셜라이저(Convenience Initializer)가 부모클래스의 지정 이니셜라이저(Designated Initializer)를 재정의하는 경우에도 override 수식어를 붙여준다.

- 반대로 부모클래스의 편의 이니셜라이저와 동일한 이니셜라이저를 자식클래스에 구현할 때는 override 수식어를 붙이지 않는다.

    - 자식클래스에서 부모클래스의 편의 이니셜라이저는 절대로 호출할 수 없기 때문이다. 즉, 재정의할 필요가 없다.
    
<img width="1058" alt="InitializerInheritanceAndOverriding-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerInheritanceAndOverriding-1.png?raw=true" title="InitializerInheritanceAndOverriding-1">

- 위의 코드를 보면 Person 클래스를 상속받은 Student 클래스에서 부모클래스의 편의 이니셜라이저와 동일한 편의 이니셜라이저를 정의할 때 override 수식어를 붙이지 않은 것을 볼 수 있다.

- 반대로 지정 이니셜라이저는 재정의를 위해 override 수식어를 사용한 것을 볼 수 있다.

- 기본 이니셜라이저 외에 지정 이니셜라이저를 자식클래스에서 동일한 이름으로 정의하려면 재정의를 위한 override 수식어를 명시해주어야 한다.

- 부모클래스의 실패 가능한 이니셜라이저를 자식클래스에서 재정의하고 싶을 때는 실패 가능한 이니셜라이저로 재정의해도 되고 필요에 따라서 실패하지 않는 이니셜라이저로 재정의해줄수도 있다.

<img width="1058" alt="InitializerInheritanceAndOverriding-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerInheritanceAndOverriding-2.png?raw=true" title="InitializerInheritanceAndOverriding-2">

- 위의 코드의 Person 클래스는 하나의 지정 이니셜라이저와 두 개의 실패 가능한 지정 이니셜라이저가 있다.

- 이를 Student 클래스에서 재정의해줄 때 하나는 부모클래스와 마찬가지로 실패 가능한 이니셜라이저로 재정의했고, 하나는 실패하지 않는 이니셜라이저로 재정의했다.

- 이처럼 부모클래스에서는 실패 가능한 이니셜라이저였더라도 자식클래스에서는 필요에 따라 실패하지 않는 이니셜라이저로 재정의해줄 수 있다.

- - -
- - -