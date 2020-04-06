---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 매개변수 기본값, 가변 매개변수와 입출력 매개변수)"
date:   2020-04-05
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Default Parameter Values Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-05-DefaultParameterValuesExample.playground)

- [Variadic Parameters Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-05-VariadicParametersExample.playground)

- [In-Out Parameters Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-05-InOutParametersExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- [값 타입과 참조 타입 Summary](https://vincentgeranium.github.io/ios,/swift/2020/02/29/basicSyntax.html)

- [함수 Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/04/basicSyntax-1.html)

- [연산 프로퍼티 Summary](https://vincentgeranium.github.io/ios,/swift/2020/03/13/basicSyntax.html)

- [프로퍼티 감시자 Summary](https://vincentgeranium.github.io/ios,/swift/2020/03/16/basicSyntax.html)

- - -

### 매개변수 기본값 (Default Parameter Value)

- `스위프트의 함수에서는 매개변수(Parameter)마다 기본값(Default Value)을 지정할 수 있다.`

    - `즉, 매개변수가 전달되지 않으면 기본값을 사용한다.`
    
- `매개변수 기본값이 있는 함수는 함수를 중복 정의(Overload)한 것처럼 사용 할 수 있다.`

- - -

### 매개변수 기본값이 있는 함수의 정의와 사용

<img width="1058" alt="defaultParameterValuesImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/defaultParameterValuesImage-1.png?raw=true">

- `기본값이 없는 매개변수를 기본값이 있는 매개변수 앞에 사용.`

    - 기본값이 없는 매개변수는 대체로 함수를 사용함에 있어 중요한 값을 전달할 가능성이 높다.
    
    - `무엇보다 기본값이 있는지와 없는지 상관 없이 중요한 매개변수는 앞쪽에 배치하는 것이 좋다.`
    
- - -

### 가변 매개변수와 입출력 매개변수 (Variadic Parameters and In-Out Parameters)

- `매개변수로 몇 개의 값이 들어올지 모를 때, 가변 매개변수(Variadic Parameter)을 사용할 수 있다.`

- `가변 매개변수(Variadic Parameter)는 0개 이상(0개 포함)의 값을 받아올 수 있다.`

- `가변 매개변수로 들어온 인자 값은 배열처럼 사용이 가능하다.`

- `함수마다 가변 매개변수는 하나만 가질 수 있다.`

- - -

### 가변 매개변수를 가지는 함수의 정의와 사용

<img width="1058" alt="variadicParameterImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/variadicParameterImage-1.png?raw=true">

- - -

### 입출력 매개변수(In-Out Parameter)

- `함수의 전달인자(Argument)로 값을 전달할 때는 보통 값을 복사해서 전달한다.`

- `값이 아닌 참조를 전달하려면 입출력 매개변수(In-Out Parameter)를 사용한다.`

- `값 타입 데이터의 참조를 전달인자(Argument)로 보내면 함수 내부에서 참조하여 원래 값을 변경한다.`

    - C 언어의 포인터와 유사하다.
    
    - `이 방법은 함수 외부의 값에 어떤 영향을 줄지 모르기 때문에 함수형 프로그래밍 패러다임에서는 지양하는 패턴이다.`
    
    - `객체지향 프로그래밍 패러다임을 사용하는 애플의 프레임워크(iOS, macOS등)에서는 유용할 수 있지만, 애플 프레임워크를 벗어난 다른 환경에서 함수형 프로그래밍 패러다임을 사용할 때는 입출력 매개변수(In-Out Parameter)를 사용하지 않는 것이 좋다.`
    
- `입출력 매개변수의 전달 순서는 다음과 같다.`

    - 1), 함수를 호출할 때, 전달인자의 값을 복사한다.
    
    - 2), 해당 전달인자의 값을 변경하면 1에서 복사한 것을 함수 내부에서 변경한다.
    
    - 3), 함수를 반환하는 시점에 2에서 변경된 값을 원래의 매개변수에 할당한다.
    
- `연산 프로퍼티 또는 감시자가 있는 프로퍼티가 입출력 매개변수(In-Out Parameter)로 전달된다면, 함수 호출 시점에 그 프로퍼티의 접근자가 호출되고 함수의 반환 시점에 프로퍼티의 설정자가 호출된다.

    - `위의 명시된 '입출력 매개변수의 전달 순서'와 '연산 프로퍼티와 프로퍼티 감시자의 접근자, 설정자 호출 순서' 이 두 가지를 함께 생각하면 이해하기 쉽다.`

- `참조는 inout 매개변수로 전달될 변수 또는 상수 앞에 앰퍼샌드(&)를 붙여서 표현한다.`

- `입출력 매개변수는 매개변수 기본값을 가질 수 없으며, 가변 매개변수로 사용될 수 없다.`

- 또한, `상수는 변경될 수 없으므로 입출력 매개변수의 전달인자로 사용될 수 없다.`

- - -

### inout 매개변수의 활용

<img width="1058" alt="inoutParameterImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inoutParameterImage-1.png?raw=true">

```swift
class Person {
    var height: Float = 0.0
    var weight: Float = 0.0
}

var jun: Person = Person()

// 참조 타임의 inout 매개변수 사용은 더욱 주의해야 한다.
// C 언어의 이중 포인터와 유사하게 동작한다.
func reference(_ person: inout Person) {
    person.height = 130 // 이렇게 사용하면 기존 참조 매개변수처럼 동작하지만
    print(jun.height) // 130
    person = Person() // 이렇게 다른 인스턴스를 할당하면 참조 자체가 변경되어 버린다.
}

reference(&jun)
jun.height // 0 - 함수 안에서 새로운 인스턴스가 할당되었기 때문에 위 jun과 다른 참조를 갖는다.
```