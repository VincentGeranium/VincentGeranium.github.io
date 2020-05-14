---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 클래스의 초기화 위임(Class Inheritance and Initialization))"
date:   2020-05-14
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -
- - -

### 클래스의 초기화 위임 (Class Inheritance and Initialization)

- 지정 이셜라이저(Designated Initializer)와 편의 이니셜라이저(Convenience Initializer) 사이의 관계를 간단히 정리해보기 위해 세 가지 규칙을 적용해볼 수 있다.

    - 1) 자식클래스의 지정 이니셜라이저는 부모클래스의 지정 이니셜라이저를 반드시 호출해야 한다.
    
    - 2) 편의 이니셜라이저는 자신을 정의한 클래스의 다른 이니셜라이저를 반드시 호출해야 한다.
    
    - 3) 편의 이니셜라이저는 궁극적으로 지정 이니셜라이저를 반드시 호출해야 한다.
    
- 다음처럼 생각해볼 수도 있다. '누군가'는 다른 지정 이니셜라이저 또는 편의 이니셜라이저를 뜻한다.

    - 누군가는 지정 이니셜라이저에게 초기화를 반드시 위임한다.
    
    - 편의 이니셜라이저는 초기화를 반드시 누군가에게 위임한다.
    
- 위 규칙들을 아래의 그림으로 표현했다.

<img width="1058" alt="ClassInheritanceAndInitialization-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ClassInheritanceAndInitialization-1.png?raw=true" title="ClassInheritanceAndInitialization-1">

- 부모클래스는 하나의 지정 이니셜라이저(ⓐ)와 두 개의 편의 이니셜라이저(①,②)를 갖는다.

    - 부모클래스의 맨 오른쪽 편의 이니셜라이저(②)는 다른 편의 이니셜라이저(①)를 호출하며 해당 편의 이니셜라이저는 궁극적으로 지정 이니셜라이저(ⓐ)를 호출한다.
    
    - 이는 앞의 규칙 2,3을 만족하는 조건이다.
    
    - 부모클래스는 자신보다 조상인 부모를 갖지 않으므로 규칙 1은 해당사항이 없다.
    
- 자식클래스는 두 개의 지정 이니셜라이저(ⓑ,ⓒ)와 하나의 편의 이니셜라이저(③)를 갖는다.

    - 편의 이니셜라이저(③)는 두 번째 지정 이니셜라이저(ⓒ)를 호출한다.
    
    - 편의 이니셜라이저는 자신의 클래스에 구현된 이니셜라이저만 호출할 수 있으므로 부모클래스의 이니셜라이저는 호출할 수 없다.
    
    - 이는 위의 규칙 2,3을 만족한다.
    
    - 두 지정 이니셜라이저 (ⓑ,ⓒ) 모두 부모클래스의 지정 이니셜라이저(ⓐ)를 호출하므로 규칙 1도 만족한다.
    
<img width="1058" alt="ClassInheritanceAndInitialization-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ClassInheritanceAndInitialization-2.png?raw=true" title="ClassInheritanceAndInitialization-2">

- 위의 그림은 조금 더 복잡한 모식도로 지정 이니셜라이저가 어떻게 클래스의 이니셜라이저 중 기둥 역활을 하는지 조금 더 쉽게 알아볼 수 있다.

- - -
- - -