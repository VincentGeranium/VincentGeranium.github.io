---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 함수를 사용한 프로퍼티 기본값 설정)"
date:   2020-03-26
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Set property default value using function Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-26-SetPropertyDefaultValueUsingFunctionExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- - -

### 함수를 사용한 프로퍼티 기본값 설정 (Set property default value using function)

- `사용자정의 연산을 통해 저장 프로퍼티 기본값을 설정하고자 한다면 클로저나 함수를 사용하여 프로퍼티 기본값을 제공할 수 있다.`

- `인스턴스를 초기화할 떄 함수나 클로저가 호출되면서 연산 결괏값을 프로퍼티 기본값으로 제공해준다.`

    - 그러므로 `클로저나 함수의 반환 타입은 프로퍼티의 타입과 일치해야한다.`
    
- `프로퍼티의 기본값을 설정해주기 위해서 클로저를 사용`한다면 `클로저가 실행되는 시점은 초기화할 때 인스턴스의 다른 프로퍼티 값이 설정되기 전이다.`

    - `즉, 클로저 내부에서는 인스턴스의 다른 프로퍼티를 사용하여 연산할 수는 없다는 것이다. 다른 프로퍼티에 기본값이 있다고 해도 안 된다.`
    
    - `클로저 내부에서 self 프로퍼티도 사용할 수 없으며, 인스턴스 메서드를 호출할 수도 없다.`
    
```swift
// 클로저를 통한 프로퍼티 기본값 설정
class SomeClass {
    let someProperty: SomeType = {
        // 새로운 인스턴스를 생성하고 사용자정의 연산을 통한 후 반환해준다.
        // 반환되는 값의 타입은 SomeType과 같은 타입이어야 한다.
        return someValue
    }()
}
```

- 위의 코드에서 `클로저 뒤에 소괄호가 붙은 이유는 클로저를 실행하기 위해서이다.`

- `클로저 뒤에 소괄호가 붙어 클로저를 실행한 결괏값은 프로퍼티의 기본값이 된다.`

- `소괄호가 없다면 프로퍼티의 기본값은 클로저 그 자체가 된다.` 그것은 위의 코드의 의도와는 전혀 다른 의미가 되는 것이다.

- - -

### 클로저를 통한 student 프로퍼티 기본값 설정

![setPropertyDefaultValueUsingFuncImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/setPropertyDefaultValueUsingFuncImage-1.png?raw=true)

- 위의 코드에서 보면 `student 프로퍼티는 Student 구조체의 인스턴스를 요소로 갖는 Array 타입이다.`

- `SchoolClass 클래스의 인스턴스를 초기화하면 student 프로퍼티의 기본값을 제공하기 위해 클로저가 동작, 1 ~ 15번까지의 학생을 생성하여 배열에 할당한다.`

-` myClass 인스턴스는 생성되자마자 student 프로퍼티에 15명의 학생이 있는 상태가 되는 것이다.`

- - -

### iOS 에서의 활용

- iOS의 UI등을 구성할 때, UI 컴포넌트를 클래스의 프로퍼티로 구현하고 UI 컴포넌트의 생성과 동시에 컴포넌트의 프로퍼티를 기본적으로 설정할 때 유용하게 사용할 수 있다.