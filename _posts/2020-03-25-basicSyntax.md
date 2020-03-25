---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 초기화 위임, 실패 가능한 이니셜라이저)"
date:   2020-03-25
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Failable Initializer Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-25-FailableInitializerExample.playground)

- [Failable Initializer Of Enumeration Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-25-FailableInitializerOfEnumExample.playground)

- [Initializer Delegation Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-25-InitializerDelegationExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- [Vincent Blog - 열거형](https://vincentgeranium.github.io/ios,/swift/2020/03/17/basicSyntax.html)

- [vincent Blog - 기본 이니셜라이저와 멤버와이즈 이니셜라이저](https://vincentgeranium.github.io/ios,/swift/2020/03/24/basicSyntax-2.html)

- - -

### 초기화 위임 (Initializer Delegation for Value Type)

- 값 타입(Value Type)인 구조체(Structure)와 열거형(Enumeration)은 코드의 중복을 피하기 위하여 이니셜라이저가 다른 이니셜라이저에게 일부 초기화를 위임하는 초기화 위임(Initializer Delegation)을 간단하게 구현할 수 있다.

- 클래스는 상속을 지원하므로 간단한 초기화 위임도 할 수 없다.

- 값 타입에서 이니셜라이저가 다른 이니셜라이저를 호출하려면 self.init을 사용한다.

- self.init은 이니셜라이저 안에서만 사용할 수 있다.

    - self.init을 사용한다는 것 자체가 사용자정의 이니셜라이저를 정의하고 있다는 뜻이다.
    
- 사용자정의 이니셜라이저를 정의하면 [기본 이니셜라이저와 멤버와이즈 이니셜라이저](https://vincentgeranium.github.io/ios,/swift/2020/03/24/basicSyntax-2.html)를 사용할 수 없다고 했다.

    - 따라서 초기화 위임을 하려면 최소한 두 개 이상의 사용자정의 이니셜라이저를 정의해야 한다.
    
- 사용자정의 이니셜라이저를 정의할 때도 기본 이니셜라이저나 멤버와이즈 이니셜라이저를 사용하고 싶다면 익스텐션을 사용하여 이니셜라이저를 구현하면 된다.

- - -

### Student 열거형과 초기화 위임

![InitializerDelegationImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerDelegationImage-1.png?raw=true)

- 위 그림의 열거형은 두 개의 사용자정의 이니셜라이저가 있다.

    - 첫 번째 사용자정의 이니셜라이저는 나이를 전달받아 나이에 맞는 학교를 case로 구분한 이니셜라이저를 초기화한다.
    
    - 두 번째 사용자정의 이니셜라이저는 태어난 해와 현재  연도를 전달받아 나이로 계산한 후 첫 번째 이니셜라이저에 초기화를 위임한다.
    
- 이렇게 초기화 위임 방법을 사용하면 중복으로 쓰지 않고도 효율적으로 여러 case의 이니셜라이저를 만들 수 있다.

- - -

### 실패 가능한 이니셜라이저 (Failable Initializer)

- 이니셜라이저를 통해 인스턴스를 초기화할 수 없는 여러 가지 예외 상황이 있다.

    - 대표적으로 이니셜라이저의 전달인자로 잘못된 값이나 적절치 못한 값이 전달되었을 때, 이니셜라이저는 인스턴스 초기화에 실패할 수 있다.
    
    - 그 외에도 여러 이유로 인스턴스 초기화에 실패할 수 있다.
    
- 이니셜라이저를 정의할 때 위와 같은 실패 가능성을 염두에 두기도 하는데, 이렇게 실패 가능성을 내포한 이니셜라이저를 실패 가능한 이니셜라이저(Failable Initializer)라고 부른다.

- 실패 가능한 이니셜라이저는 클래스, 구조체, 열거형 등에서 모두 정의할 수 있다.

- 실패 가능한 이니셜라이저는 실패했을 때 nil을 반환해주므로 반환 타입이 옵셔널로 지정된다.

- 실패 가능한 이니셜라이저는 init? 키워드를 사용한다.

![InitializerDelegationImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerDelegationImage-2.png?raw=true)

- 실패 가능한 이니셜라이저는 구조체와 클래스에서도 유용하지만 특히 [열거형](https://vincentgeranium.github.io/ios,/swift/2020/03/17/basicSyntax.html)에서 유용하게 사용할 수 있다.

    - 특정 case에 맞지 않는 값이 들어오면 생성에 실패할 수 있다.

    - 혹은 rawValue로 초기화할 때, 잘못된 rawValue가 전달되어 들어온다면 열거형 인스턴스를 생성하지 못할 수 있다.
    
    - 따라서 rawValue를 통한 이니셜라이저는 기본적으로 실패 가능한 이니셜라이저로 제공된다.
    
- - -

### 열거형의 실패 가능한 이니셜라이저 (Failable Initializer of Enumeration)

![InitializerDelegationImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerDelegationImage-3.png?raw=true)

- - -

### 이니셜라이저의 매개변수 (Parameter of Initializer)

- 실패하지 않는 이니셜라이저와 실패 가능한 이니셜라이저를 같은 이름과 같은 매개변수 타입을 갖도록 정의 할 수 없다.

- 실패 가능한 이니셜라이저는 실제로 특정 값을 반환하지 않는다.

- 초기화를 실패했을 때는 return nil을 반대로 초기화에 성공했을 때는 return을 적어 초기화의 성공과 실패를 표현할 뿐, 실제 값을 반환하지는 않는다.

- - -