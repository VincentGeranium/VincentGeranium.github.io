---
layout: post
title:  "iOS 면접을 위한 문답 정리 - 5 (Operation Queues, Operation Objects, Operation, Concurrent VS Non-concurrent Operations,  모르는 단어)"
date:   2020-05-26
categories: iOS, Swift
---

이 포스트는 iOS 개발 면접을 위한 문답을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [ZeddiOS](https://zeddios.tistory.com/510)

- [꼬마상어의 생각](https://littleshark.tistory.com/40)

- [iOSTORY](https://gwangyonglee.tistory.com/21)

- [MDN web docs](https://developer.mozilla.org/ko/docs/Glossary/Semantics)

- [System Chunk 개념](https://lascrea.tistory.com/61)

- - -
- - -

## Operation Queues

- **Cocoa Operations는 비동기적으로 수행하려는 작업(work)을 캡슐화하는 '객체지향적인 방법(object-oriented way)' 이다.**

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
    
    - 이미 필요한 task를 수행하는 기존 메소드가 있는 경우, 이 클래스를 시용할 수 있다.
    
    - 하위클래스화가 필요하지 않으므로 이 클래스를 사용하여 보다 동적인 방식으로 Operation 객체를 만들 수도 있다.
    
    - Xcode 6.1 부터 Swift에서 disabled 됨.
    
- **NSBlockOperation**

    - 현재 하나 이상의 블록 객체를 동시에 실행하는데 사용하는 클래스이다.
    
    - 둘 이상의 블록을 실행할 수 있으므로 블록 operation 객체는 그룹 semantic을 사용하여 작동한다.
    
    - 연관된 모든 블럭이 실행을 완료한 경우에만 operation 자체가 완료된 것으로 간주한다.

- **NSOperation**

    - 커스텀 operation 객체를 정의하기 위한 base class이다.
    
    - NSOperation을 하위 클래스화 하면, operation이 실행되는 기본방식을 변경하고, 상태를 보고하는 기능을 포함하여, 자체 operation의 구현을 완벽하게 제어(Complete control) 할 수 있다.
    
    - 모든 operation 객체는 다음과 같은 주요 기능을 지원한다.
    
        - operation 객체간의 그래프 기반 종속성 설정 지원. 이러한 종속성은 종속된 모든 작업이 완료할 때까지 주어진 operation이 실행되는 것을 방지한다.
        
        - operation의 main task가 완료된 후에 실행되는 optional completion 블록을 지원한다(OS X v10.6 이상에만 해당)
        
        - KVO 알림을 사용하여 operation이 실행 상태 변경 모니터링을 지원한다.
        
        - operation 우선 순위 지정을 지원하므로, 상대적인 실행 순서에 영향을 준다.
        
        - 실행 중 조작을 정지 할 수 있는 canceling semantics 기능을 지원한다.
        
- - -
- - -

### Operation

- operation은 앱의 동시성 수준을 향상시킬 수 있도록 설계되었다.

- operation은 앱의 동작을 단순한 개별 청크로 구성하고, 캡슐화하는 좋은 방법이기도 하다.

- 앱의 main thread에서 코드를 실행하는 대신 하나 이상의 operation 객체를 큐에 제출하고, 하나 이상의 개별 thread에서 해당 작업을 비동기적으로 수행 할 수 있다.

- - -
- - -

## Concurrent VS Non-concurrent Operations

- 일반적으로 operation을 operation queue에 추가하여 operation을 실행하지만, 그렇게 하지 않아도 된다.

    - 또한 start 메소드를 호출하여 operation 객체를 수동으로 실행 할 수도 있다.

        - 그렇지만, 그렇게 해도 코드의 나머지 부분과 동시에 operation이 실행되는 것은 아니다.
    
- NSOperation 클래스의 isConcurrent 메소드는 start 메소드가 호출 된 쓰레드와 관련하여 operation이 동기적 / 비동기적으로 실행되는지 여부를 알려준다.

    - 기본적으로 이 메소드는 False를 반환한다. 이는 호출 쓰레드에서 작업이 동기적으로 실행됨을 의미한다.
    
        - **즉, isConcurrent는 비동기적으로 실행되는 경우에는 true를, 동기적으로 실행되는 경우에는 false를 리턴한다.**
        
- **isConcurrent 의 문서에 가보면 Discussion에 'Use the isAsynchromous property instead.' isConcurrent 대신에 isAsynchronous를 사용하라고 나온다.**    

- concurrent operation(호출 쓰레드와 비동기적으로 실행되는 작업)을 구현하려면, 비동기적으로 operation을 시작하는 추가코드를 작성해야한다.

    - 예를 들어, 별도의 쓰레드를 생성하거나, 비동기 시스템 함수를 호출하거나, start 메소드가 operation을 시작하고, operation이 완료되기 전에 즉각적으로 반환되도록 할 수 있다.
    
- 대부분의 개발자는 concurrent operation 객체를 구현할 필요가 없다.

    - **operation을 항상 operation queue에 추가하는 경우, concurrent operation을 구현할 필요가 없다.**
    
        - nonconcurrent operation을 operation queue에 제출하면, 해당 operation을 실행할 쓰레드가 큐 자체에 생성된다.
        
        - 따라서 nonconcurrent operation을 operation queue에 추가해도, operation 객체 코드는 비동기적으로 실행된다.
        
- concurrent operations을 정의하는 기능은, 해당 operation을 operation queue에 추가하지 않고, 비동기식으로 실행해야 하는 경우에만 필요하다.

    - 즉, operation을 그냥 operation queue에 제출하기만 하면 concurrent operation 객체를 만든거나 다름이 없으니 굳이 concurrent operation을 개발자 자기 자신이 '직접 만들거다' 하면, **그 만든 concurrent operation을 operation queue에 추가히지 "않고" 바동기적으로 실행해야 하는 경우에만 만들라는 것이다.**

- - -
- - -

### 모르는 단어

- overhead

    - 오버헤드는 어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리 등을 말한다. 예를 들어 A라는 처리를 단순하게 실행한다면 10초 걸리는데, 안전성을 고려하고 부가적인 B라는 처리를 추가한 결과 처리시간이 15초 걸렸다면, 오버헤드는 5초가 된다.

- Serial

    - 직렬

- Concrete Class

    - 구상 클래스, 구현 클래스, 구체 클래스로 불린다. 
    
        - 정의한 모든 연산(operation)이나 일부 연산의 구현을 서브클래스로 넘기는 추상 클래스(abstract class)나 객체의 연산에 대한 구현이 포함되어 있지 않고 정의만 존재하는 인터페이스를 통해 인스턴스를 만들 수 없다. 완성되지 않은 설계도를 가지고 건물을 만들수는 없기 때문이다.
    
        - **그렇다면, 모든 연산에 대한 구현을 가지고 있는 클래스는?? 바로 Concrete Class라고 한다. 정의한 모든 연산에 대한 구현을 가지고 있는 완전한 클래스이므로 개발자는 이 클래스의 인스턴스를 만들 수 있다.**
        
- Selector

    - **함수를 직접 지정하는 기능을 가진 일종의 함수 선택자.**
    
    - **함수의 매개변수로 다른 함수를 사용할 떄 사용하는 키워드. 함수를 참조하는 Type이라고 생각하면 된다. CallBack 함수랑 유사한 개념.**
    
    - selector은 본래 Objective-C에서 클래스 메소드의 이름을 가르키는데 사용되는 참조 타입(reference type)이다.
    
    - 동적 호출 등의 목적으로 @selector() attributes 메소드 이름을 인자값으로 넣어 전달하면 이를 내부적으로 정수값으로 매핑해서 처리하는 형태이다.
    
    - **이것이 Swift로 넘어오면서 구조체 형식으로 정의되고 #selector() 구문을 사용하여 해당 타입의 값을 생성할 수 있게 되었다.**
    
         - Swift4부터는 Selector 타입으로 전달할 메소드를 작성시 반드시 @objc attributes를 붙여주어야 한다.
         
         - 이는 Swift에서 정의한 메소드를 Objective-C 에서도 인식할 수 있도록 해 준다.
    
- Attributes

    - Attribute는 컴파일러에게 특별한 신호라고 생각하면 된다.
    
    - swift에서는 @ 심볼을 두가지 이유에서 사용한다.
    
        - 1) 선언하기 위해
        
        - 2) 타입을 적용하기 위해
        
```swift
// 사용할 때는 아래와 같이 사용
@attribute name

@attribute name(attribute arguments)
```

- Semantic

    - 프로그래밍에서, 시멘틱은 코드 조각의 의미를 나타낸다.
    
    - 예를 들어 '이 HTML 엘리먼트가 가진 목적이나 역활은 무엇인가?' 하는 것이다.
    
- Chunk

    - chunk (청크)란 하나의 영역을 뜻함.
    
    - 데이터를 분산해서 관리하는 방법.
    
    - 데이터 덩어리.