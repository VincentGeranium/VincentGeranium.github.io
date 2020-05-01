---
layout: post
title:  "기본 문법 공부(확장(expansion) - 서브스크립트(Subscript), 서브스크립트 문법, 서브스크립트 구현)"
date:   2020-04-28
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Subscript Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-28-SubscriptExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Subscripts.html)

- [기본 문법 공부(연산 프로퍼티) - get, set](https://vincentgeranium.github.io/ios,/swift/2020/03/13/basicSyntax.html)

- - -

### 서브스크립트(Subscript)

- **클래스, 구조체, 열거형에는 컬렉션, 리스트, 시퀀스 등 타입의 요소에 접근하는 단축 문법인 서브스크립트(Subscript)를 정의할 수 있다.**

- **서브스크립트는 별도의 설정자(Setter) 또는 접근자(Getter)등의 메서드를 구현하지 않아도 인덱스를 통해 값을 설정하거나 가져올 수 있다.**

    - `예를 들어 someArray라는 Array 인스턴스의 index를 통해 해당 인덱스의 값에 접근하고 싶다면 someArray[index]라고 표현.`
    
    - `또 다른 예로는 someDictionary라는 Dictionary의 key를 통해 해당 키의 값을 가져오고 싶다면 someDictionary[key]라고 표현`
    
        - **위의 두 가지의 예시와 같이 표현하는 것이 바로 서브스크립트이다.**
    
- **한 타입에 여러 개의 서브스크립트를 정의**할 수 있으며 **다른 타입을 인덱스로 갖는 여러 개의 서브스크립트를 중복 정의(Overload)할 수도 있으며,** **필요에 따라 여러 개의 매개변수를 인덱스로 사용**할 수도 있다.

- - -

### 서브스크립트 문법

- **서브스크립트는 인스턴스의 이름 뒤에 대괄호로 감싼 값을 싸줌으로써 인스턴스 내부의 특정 값에 접근할 수 있다.**

- **서브스크립트 문법은 연산 프로퍼티나 인스턴스 메서드 문법과 유사한 형태로 볼 수 있다.**

- 서브스크립트는 **subscript 키워드를 사용하여 정의**한다.

- **인스턴스 메서드와 비슷하게 매개변수의 개수, 타입, 반환 타입 등을 지정한다.**

- **읽고 쓰기(get, set)가 가능하도록 구현하거나 읽기 전용(read-only)으로만 구현할 수 있다.**

    - **이는 접근자(get)와 설정자(set)를 사용할 수 있는 연산 프로퍼티의 형태와 유사하다.**
    
```swift
// 서브스크립트 정의 문법
subscript(index: Int) -> Int {
    get {
        // 적절한 서브스크립트 결과값 반환
    }
    
    set(newValue) {
        // 적절한 설정자 역활 수행
    }
}
```

- `위의 코드는 서브스크립트를 정의하는 문법이다.`

- **서브스크립트를 정의하는 코드틑 각 타입의 구현부 또는 타입의 익스텐션 구현부에 위치해야 한다.**

- 위의 코드에 구현한 **서브스크립트 설정자의 newValue의 타입은 서브스크립트의 반환 타입과 동일하다.**

- `연산 프로퍼티와 마찬가지로 매개변수를 따로 명시해주지 않으면 설정자(set)의 암시적 전달인자(Argument) newValue를 사용할 수 있다.`

- **또, 연산 프로퍼티와 마찬가지로 읽기 전용 프로퍼티를 구현할 때는 get이나 set 키워드를 사용하지 않고 적절한 값만 반환해주는 형태로 구현해도 된다.**

```swift
// 읽기 전용 서브스크립트 정의 문법
subcript(index: Int) -> Int {
    get {
        // 적절한 서브스크립트 값 반환
    }
}

subscript(index: Int) -> Int {
    // 적절한 서브스크립트 결과값 반환
}
```

- 위 코드의 두 서브스크립트 정의는 **동일한 역활**을 한다.

- **get 메서드 없이 단순히 값만 반환하도록 구현한다면 읽기 전용이 된다.**

- `연산 프로퍼티와 유사한 문법임을 알 수 있다.`

- - -

### 서브스크립트 구현

- **서브스크립트는 자신이 가지는 시퀀스나 컬렉션, 리스트 등의 요소를 반환하고 설정할 때 주로 사용된다.**

<img width="1058" alt="subscriptImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/subscriptImage-1.png?raw=true">

- **위의 School 클래스는 읽기 전용 서브스크립트가 하나 있다.**

    - **학생의 번호를 전달인자(Argument)로 전달받아 자신의 students 프로퍼티의 인덱스에 맞는 Student 인스턴스를 반환한다.**

- - -
- - -