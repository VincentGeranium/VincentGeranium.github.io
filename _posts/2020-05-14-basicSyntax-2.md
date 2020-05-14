---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 2단계 초기화(Two-Phase Initialization))"
date:   2020-05-14
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Two-Phase Initialization Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-14-TwoPhaseInitializationExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -
- - -

### 2단계 초기화 (Two-Phase Initialization)

- 스위프트의 클래스 초기화는 2단계(Two-Phase)를 거친다.

    - 1단계는 클래스에 정의한 각각의 저장 프로퍼티에 초깃값이 할당된다.
    
    - 모든 저장 프로퍼티의 초기 상태가 결정되면 2단계로 돌입해 저장 프로퍼티들을 사용자정의할 기회를 얻는다.
    
        - 그 후 비로소 새로운 인스턴스를 사용할 준비가 끝난다.
        
    - 2단계 초기화는 프로퍼티를 초기화하기 전에 프로퍼티 값에 접근하는 것을 막아 초기화를 안전하게 할 수 있도록 해준다.
    
        - 또, 다른 이니셜라이저가 프로퍼티의 값을 실수로 변경하는 것을 방지할 수도 있다.
        
- 스위프트 컴파일러는 2단계 초기화를 오류 없이 처리하기 위해 다음과 같은 네 가지 안전확인(Safty-checks)을 실행한다.
    
    - 1) 자식클래스의 지정 이니셜라이저(Designated Initializer)가 부모클래스의 이니셜라이저를 호출하기 전에 자신의 프로퍼티를 모두 초기화했는지 확인한다.
    
        - 그래서 자식클래스의 지정 이니셜라이저에서 부모클래스의 이니셜라이저를 호출하기 전에 자신의 모든 (기본값이 없는) 저장 프로퍼티에 값을 할당해주어야 한다.
        
    - 2) 자식클래스의 지정 이니셜라이저는 상속받은 프로퍼티에 값을 할당하기 전에 반드시 부모클래스의 이니셜라이저를 호출해야한다.
    
    - 3) 편의 이니셜라이저(Convenience Initializer)는 자신의 클래스에 정의한 프로퍼티를 포함하여 그 어떤 프로퍼티라도 값을 할당하기 전에 다른 이니셜라이저를 호출해야 한다.
    
    - 4) 초기화 1단계를 마치기 전까지는 이니셜라이저는 인스턴스 메서드를 호출할 수 없다. 또, 인스턴스 프로퍼티의 값을 읽어들일 수도 없다. self 프로퍼티를 자신의 인스턴스를 나타내는 값으로 활용할 수도 없다.
    
- 클래스의 인스턴스는 초기화 1단계를 마치기 전까지는 아직 유효하지 않다.

     - 프로퍼티는 읽기만 가능하며, 메서드는 호출될 수 있을 뿐이다.
     
- 클래스의 인스턴스가 초기화 1단계를 마쳤을 때 비로소 유효한 인스턴스가 되는 것이다.

- - -
- - -

### 네 가지 안전확인(Safty-checks)에 근거하여 2단계 초기화가 이루어지는 과정

#### 1단계

- 1) 클래스가 지정 또는 편의 이니셜라이저를 호출한다.
    
- 2) 그 클래스의 새로운 인스턴스를 위한 메모리가 할당된다. 메모리는 아직 초기화되지 않은 상태이다.
    
- 3) 지정 이니셜라이저는 클래스에 정의된 모든 저장 프로퍼티에 값이 있는지 확인한다. 현재 클래스 부분까지의 저장 프로퍼티를 위한 메모리는 이제 초기화되었다.
    
- 4) 지정 이니셜라이저는 부모클래스의 이니셜라이저가 같은 동작을 행할 수 있도록 초기화를 양도한다.
    
- 5) 부모클래스는 상속 체인을 따라 최상위 클래스에 도달할 때까지 이 작업을 반복한다.
    
    - 최상위 클래스에 도달했을 때, 최상위 클래스까지의 모든 저장 프로퍼티에 값이 있다고 확인하면 해당 인스턴스의 메모리는 모두 초기화된 것이다. 이로써 1단계가 완료되었다.

<img width="1058" alt="TwoPhaseInitialization-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TwoPhaseInitialization-1.png?raw=true" title="TwoPhaseInitialization-1">

#### 2단계

- 1) 최상위 클래스로부터 최하위 클래스까지 상속 체인을 따라 내려오면서 지정 이니셜라이저들이 인스턴스를 제각각 사용자정의하게 된다. 이 단계에서는 self를 통해 프로퍼티 값을 수정할 수 있고, 인스턴스 메서드를 호출하는 등의 작업을 진행할 수 있다.

- 2) 마지막으로 각각의 편의 이니셜라이저를 통해 self를 통한 사용자정의 작업을 진행할 수 있다.

<img width="1058" alt="TwoPhaseInitialization-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TwoPhaseInitialization-2.png?raw=true" title="TwoPhaseInitialization-2">

<img width="1058" alt="TwoPhaseInitialization-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TwoPhaseInitialization-3.png?raw=true" title="TwoPhaseInitialization-3">

- 위 코드의 Student 클래스의 지정이니셜라이저(init(name:age:major:))는 부모클래스의 지정 이니셜라이저를 호출하기 전에 자신의 self 프로퍼티를 이용해 major 프로퍼티의 값을 할당한다.

    - 그렇게 하면 안전확인 중 1번의 조건에 만족한다.
    
- super.init(name: name, age: age)를 통해 부모클래스의 이니셜라이저를 호출했으며 그 외에 상속받은 프로퍼티가 없으므로 부모의 이니셜라이저 호출 이후에 값을 할당해줄 프로퍼티가 없다.

    - 따라서 안전확인 중 2번의 조건을 갖추었다.
    
- 편의 이니셜라이저인 convenience init(name:)은 따로 차후에 값을 할당할 프로퍼티가 없고, 다른 이니셜라이저를 호출했다.

    - 그러므로 안전확인 중 3번 조건에 부합한다.
    
- 마지막으로 이니셜라이저 어디에서도 인스턴스 메서드를 호출하거나 인스턴스 프로퍼티의 값을 읽어오지 않았으므로 안전확인 중 4번 조건을 충족한다.

- 안전확인 후 super.init(name: name, age: age)를 통해 1단계와 2단계의 초기화까지 마치게 된다.

- - -
- - -