---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 5 (Operation Queues, Operation)"
date:   2020-05-26
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- []()

- - -
- - -

## Operation Queues

- Cocoa Operations는 비동기적으로 수행하려는 작업(work)을 캡슐화하는 '객체지향적인 방법(object-oriented way)' 이다.

- **Operation은 operation queue와 함께 사용되거나 자체적으로 사용되도록 설계됨.**

    - Objective-C 기반이기 때문에 Operation은 OS X 및 iOS의 Cocoa 기반 앱에서 가장 일반적으로 사용된다.
    
- 아래에 나오는 내용들은 Operation을 정의하고 사용하는 방법을 보여준다.

### Operation Objects

- **operation 객체는 앱에서 수행 할 작업을 캡슐화하는데 사용하는 Foundation 프레임워크 NSOperation 클래스의 인스턴스이다.**

- **NSOperation 클래스 자체는 유용한 작업을 수행하기 위해서 서브클래싱 되어야 하는 추상 기본 클래스이다.**

    - 추상적임에도 불구하고 이 클래스는 자신의 하위클래스에서 해야하는 작업량을 최소화하기 위해 상당한 양의 인프라를 제공한다.
    
    - 또한 Foundation 프레임워크는 기존 코드와 함께 그대로 사용 할 수 있는 두개의 concrete 하위 클래스를 제공한다.
    
- **NSInvocationOperation**

    - 앱의 객체 및 selector를 기반으로, operation 객체를 만드는데 사용하는 클래스이다.

- - -
- - -

### 모르는 단어

- overhead

    - 오버헤드는 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리 등을 말한다. 예를 들어 A라는 처리를 단순하게 실행한다면 10초 걸리는데, 안전성을 고려하고 부가적인 B라는 처리를 추가한 결과 처리시간이 15초 걸렸다면, 오버헤드는 5초가 된다.

- Serial

    - 직렬

- Concrete Class

    - 구상 클래스, 구현 클래스, 구체 클래스 로 불린다. 
    
    - 정의한 모든 연산(operation)이나 일부 연산의 구현을 서브클래스로 넘기는 추상 클래스(abstract class)나 객체의 연산에 대한 구현이 포함되어 있지 않고 정의만 존재하는 인터페이스를 통해 인스턴스를 만들 수 없다. 완성되지 않은 설계도를 가지고 건물을 만들수는 없기 때문이다.
    
        - **그렇다면, 모든 연산에 대한 구현을 가지고 있는 클래스는 ?? 바로 Concrete Class라고 한다. 정의한 모든 연산에 대한 구현을 가지고 있는 완전한 클래스이므로 개발자는 이 클래스의 인스턴스를 만들 수 있다.**