---
layout: post
title:  "기본 문법 공부(확장(expansion) - 제네릭 타입(Generic Types))"
date:   2020-05-01
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Generic Type Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-01-GenericTypeExampleCode-1.playground)

- [Generic Type Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-01-GenericTypeExampleCode-2.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -
- - -

### 제네릭 타입(Generic Types)

- 제네릭 함수에 이어 **제네릭 타입을 구현할 수도 있다.**

- **제네릭 타입을 구현하면 사용자정의 타입인 구조체, 클래스, 열거형 등이 어떤 타입과도 연관되어 동작할 수 있다.**

    - **Array와 Dictionary 타입이 자신의 요소로 모든 타입을 대상으로 동작할 수 있는 것과 유사하다.**

- - -

### Stack 제네릭 컬렉션 타입 (Stack Generic Collection Type)

- `스택은 배열과 유사하게 순서가 있는 값들의 모음이다.`

- **배열은 중간중간 요소를 삽입하거나 삭제**할 수 있지만, **스택은 컬렉션의 끝 부분에서만 요소를 추가하고 삭제**할 수 있다.

    - `추가를 Push, 삭제를 Pop 이라 칭한다.`
    
<img width="1058" alt="StackExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/StackExampleImage.png?raw=true" title="StackExampleImage-1">

- `위의 그림은 스택의 요소가 어떻게 추가되고 삭제되는지에 대한 그림이다.`

- - -

### 제네릭을 사용하지 않은 IntStack 구조체 타입

<img width="1058" alt="genericTypeImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericTypeImage-1.png?raw=true" title="genericTypeImage-1">

- `위의 코드의 IntStack 타입은 Int 타입을 요소로 가질 수 있는 간단한 스택 기능을 구현한 구조체 타입이다.`

- **내부에 items라는 이름의 Int 타입 배열을 가짐으로써, Int 타입의 요소들을 pop 하고 push 할 수 있는 스택의 기능을 구현했다.**

- - -

### 제네릭을 사용한 Stack 구조체 타입

- 아래의 코드는 **제네릭을 사용**하여 **모든 타입을 대상으로 동작할 수 있는 스택 기능을 구현**했다.

    - `모든 타입을 대상으로 동작할 수 있다는 뜻이 모든 타입이 섞여 들어올 수 있다는 것은 아니다.`
    
    - **만약 요소로 모든 타입을 수용할 수 있도록 구현하려고 했다면** `'제네릭을 사용하지 않은 IntStack 구조체 타입'의 코드`에서 **items 배열의 타입을 Any로 지정해주면 그만이다.**
    
- **우리는 스택의 요소로 한 타입을 지정해주면 그 타입으로 계속 스택이 동작하길 바라며, 처음 지정해주는 타입은 스택을 사용하고자 하는 사람 마음대로 지정할 수 있도록 제네릭을 사용한다는 것이다.**

<img width="1058" alt="genericTypeImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericTypeImage-2.png?raw=true" title="genericTypeImage-2">

- 위 코드의 **Stack 구조체**는 Int라는 타입 대신 **Element라는 타입 매개변수를 사용했다.**

    - **Element라는 타입 매개변수는 items Array의 요소 타입으로 지정**했으며, **push(_:)와 pop() 메서드의 매개변수와 반환 타입으로도 지정**했다.
    
- **Stack의 인스턴스를 생성할 때 실제로 Element 대신 어떤 타입을 사용할지 명시해주는 방법은 Stack<Type> 처럼 선언해주면 된다.**
    
    - 그래서 **Stack<Double>이라고 타입을 선언**해준 **doubleStack 인스턴스**는 **Element의 타입으로 Double을 사용**한다.
    
    - 마치 `Array 타입을 사용할 때 Array<Type>`, `Dictionary 타입을 사용할 때 Dictionary<KeyType, ValueType>처럼 표기해줬던 것과 유사하다.` `Array도 제네릭 타입이기 때문이다.`
    
- 위 코드의 **anyStack의 예처럼 Element으 타입으로 Any를 사용해도 무방**하다.

    - **Stack의 items 배열을 Any 타입으로 정의하는 것보다 제네릭을 사용했을 때 훨씬 유용하고 광범위하게 사용**할 수 있으며, **Element의 타입을 정해주면 그 타입에만 동작하도록 제한할 수 있어 더욱 안전하고 의도한 대로 기능을 사용하도록 유도할 수 있다.**
    
- - -
- - -