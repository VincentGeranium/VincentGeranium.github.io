---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 상수 프로퍼티, 기본 이니셜라이저와 멤버와이즈 이니셜라이저)"
date:   2020-03-24
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Initialization of Constant Property Example](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-24-InitializationofConstantPropertyExample.playground)

- [Default Initializer And Memberwise Initializer Example](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-24-DefaultInitializerAndMemberwiseInitializerExample.playground)

- - -

### 참고 문서

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -

### 상수 프로퍼티 (Constant Property)

- [옵셔널 프로퍼티 타입 (Optional Property Type)](https://vincentgeranium.github.io/ios,/swift/2020/03/24/basicSyntax.html)의 그림에서 보면 name 프로퍼티를 상수(Constant)가 아닌 변수(Variable)로 선언해둔다면 "Vincent"라는 이름을 할당하고 난 후 전혀 다른 사람으로 변할 수 있다.

    - 위와 같은 상황을 방지하려면 name 프로퍼티를 상수(let - Constant)로 선언해야 한다.

- `저장 프로퍼티를 상수로 선언시 고려해야 할 점이 있다.`

    - `상수(Constant)로 선언된 저장 프로퍼티(Stored Property)는 인스턴스(Instance)를 초기화(Initialization)하는 과정에서만 값을 할당할 수 있으며, 처음 할당된 이후로는 값을 변경할 수 없다.`
    
- `클래스 인스턴스의 상수 프로퍼티는 프로퍼티가 정의된 클래스에서만 초기화할 수 있다. 해당 클래스를 상속받은 자식클래스의 이니셜라이저에서는 부모클래스의 상수 프로퍼티 값을 초기화 할 수 없다.`

- - -

### 상수 프로퍼티의 초기화 (Initialization of Constant Property)

![InitializationofConstantPropertyImage - 1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializationofConstantPropertyImage-1.png?raw=true)

- - -

### 기본 이니셜라이저와 멤버와이즈 이니셜라이저(Default Initializer and Memerwise Initializer for Structure Type)

- `사용자정의 이니셜라이저(Customizing Initializer)를 정의해주지 않으면 클래스나 구조체는 모든 프로퍼티에 기본값이 지정되어 있다는 전제하에 기본 이니셜라이저(Default Initializer)를 사용한다.`

- `기본 이니셜라이저(Default Initializer)는 프로퍼티 기본값으로 프로퍼티를 초기화해서 인스턴스를 생성한다.`

    - `즉, 기본 이니셜라이저는 저장 프로퍼티의 기본값이 모두 지정되어 있고, 동시에 사용자정의 이니셜라이저(Customizing Initializer)가 정의되어 있지 않은 상태에서 제공된다.`
    
- `저장 프로퍼티를 선언할 때 기본값을 지정해주지 않으면 이니셜라이저에서 초깃값을 설정해야한다.`

    - 그러나, 프로퍼티 하나 때문에 매번 이니셜라이저를 추가하거나 변경하는 일은 여간 귀찮은 일이 아니다.
    
    - 때문에 `구조체는 사용자정의 이니셜라이저를 구현하지 않으면 프로퍼티의 이름으로 매개변수를 갖는 이니셜라이저인 멤버와이즈 이니셜라이저(Memberwise Initializer)를 기본으로 제공한다.`
    
    - 그렇지만 `클래스는 멤버와이즈 이니셜라이저를 지원하지 않는다.`
    
![UsedMemberwiseInitializerForStructImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UsedMemberwiseInitializerForStructImage-1.png?raw=true)

- 위의 그림의 주석을 보면 알 수 있듯이 위의 코드는 `구조체가 기본적으로 제공하는 멤버와이즈 이니셜라이저(Memberwise Initializer)를 사용하여 인스턴스를 생성하는 코드`이고, 아래는 `클래스 저장 프로퍼티의 기본값이 지정되어 있고, 동시에 사용자정의 이니셜라이저가 정의되어 있지 않은 상태로 기본 이니셜라이저(Default Initializer)를 사용하여 인스턴스를 생성하는 코드이다.`

- `멤버와이즈 이니셜라이저는 구조체만의 특권이다.`