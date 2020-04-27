---
layout: post
title:  "기본 문법 공부(연산자(Basic Operator) - 중위 연산자(Infix Operator) 정의와 구현, 연산자 우선순위 그룹 정의, 중위 연산자를 정의하는 방법)"
date:   2020-04-26
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Infix Operator Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-26-InfixOperatorExampleCode-1.playground)

- [Infix Operator Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-26-InfixOperatorExampleCode-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html)

- - -

### 중위 연산자 정의와 구현

- `중위 연산자 정의도 전위 연산자나 후위 연산자 정의와 크게 다르지 않다.`

- 다만 `중위 연산자`는 **우선순위 그룹을 명시해줄 수 있다.**

- - -

### 중위 연산자 정의와 구현 - 연산자 우선순위 그룹 정의

```swift
precedencegroup 우선순위 그룹 이름 {
    higherThan: 더 낮은 우선순위 그룹 이름
    lowerThan: 더 높은 우선순위 그룹 이름
    associaitivity: 결합방향(left / right / none)
    assignment: 할당방향 사용(true / false)
}
```

- `연산자 우선순위 그룹`은 **precedencegroup** 뒤에 `그룹 이름을 써주어 정의`할 수 있다.

    - `연산자 우선순위 그룹은 중위 연산자에서만 사용된다.`
    
    - `전위 연산자 및 후위 연산자는 결합방향 및 우선순위를 지정하지 않는다.`
    
        - 대신, 하나의 피연산자에 전위 연산과 후위 연산을 한 줄에 사용하게 되면 후위 연산을 먼저 수행한다 [후위 연산자 Post 참고](https://vincentgeranium.github.io/ios,/swift/2020/04/25/basicSyntax-1.html)
        
- `더 낮은 우선순위 그룹 이름을 넣을 수 있는 higherThan.`

- `더 높은 우선순위 그룹 이름을 넣을 수 있는 lowerThan.`

    - **lowerThan 속성**에는 `현재 모듈 밖에 정의된 우선순위 그룹만 명시할 수 있다.`

- `higherThan 과 lowerThan에 들어갈 수 있는 그룹 이름을 통해` **기존의 우선순위 그룹과 새로 만들어줄 우선순위 그룹과의 상하관계를 설정**해 줄 수 있다.

- `결합방향을 명시`해줄 수 있는 **associativity**에는 **left, right, none을 지정**해줄 수 있다.

    - 만약 **associativity를 빼놓고 연산자 우선순위 그룹을 정의하면 기본적으로 none이 설정**된다.
    
    - `결합방향이 없는 연산자`는 **여러 번 연달아 사용할 수 없다.**
    
    - `결합방향이 있는` **더하기(+) 또는 빼기(-) 등의 연산자는 1 + 2 + 3과 같이 연산해줄 수 있고, 3 - 2 - 1과 같이 연산해줄 수 있다.**
    
    - `결합방향이 있는 연산자`는 **섞어서 1 + 2 - 3처럼도 사용할 수 있다.**
    
    - `결합방향이 없는 부등호 연산자(<)의 경우`에는 **연달아 사용해줄 수 없다.**
    
        - `1 < 2 < 3 과 같은 모양으로 사용할 수 없다는 뜻이다.`
        
- `연산자 우선순위 그룹`의 **assignment는 옵셔널 체이닝과 관련된 사항이다.** [옵셔널 체이닝 Post 참고](https://vincentgeranium.github.io/ios,/swift/2020/04/14/basicSyntax-1.html)

    - `연산자가 옵셔널 체이닝을 포함한 연산에 포함되어 있을 경우` **연산자의 옵셔널 체이닝을 할 때 표준 라이브러리의 할당 연산자와 동일한 결합방향 규칙을 사용한다.**
    
        - **즉, 스위프트의 할당 연산자는 오른쪽 결합을 사용하므로 assignment를 true로 설정하면 연산자를 사용하여 옵셔널 체이닝을 할 때 오른쪽부터 체이닝이 시작된다는 뜻이다.
        
    - **false를 설정하거나 assignment를 따로 명시해주지 않으면** `해당 우선순위 그룹에 해당하는 연산자는 할당을 하지 않는 연산자와 같은 옵셔널 체이닝 규칙을 따른다.`
    
        - **즉, 연산자에 옵셔널 체이닝 기능이 포함되어 있다면 왼쪽부터 옵셔널 체이닝을 하게 된다.**s
        
- **만약, 중위 연산자를 정의할 때 우선순위 그룹을 명시해주지 않는다면 우선순위가 가장 높은 DefaultPrecedence 그룹을 우선순위 그룹으로 갖게 된다.**

- - -

### 중위 연산자 정의와 구현 - 중위 연산자를 정의하는 방법

- **중위 연산자의 정의**에는 **infix**라는 `키워드를 사용한다.`

<img width="1058" alt="basicOperatorImage-7" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-7.png?raw=true">

- 위의 코드에서 `'**'을 중위 연산자로 사용하기 위해 정의해보았다.`

    - `연산자의 이름`은 '**'이고, `MultiplicationPrecedence 연산자 우선순위 그룹에 속하게 된다.`
    
    - **만약 MultiplicationPrecedence라고 명시해주지 않는다면 DefaultPrecedence 그룹으로 자동 지정된다.**
    
    
<img width="1058" alt="basicOperatorImage-8" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-8.png?raw=true">

- `위의 코드는 문자열과 문자열 사이에 '**' 연산자를 사용하면 뒤에 오는 문자열이 앞의 문자열 안에 속해있는지 확인하는 연산을 실행하도록 구현했다.`

- **중위 연산자 구현 함수에는 따로 키워드를 추가하지 않는다.**

<img width="1058" alt="basicOperatorImage-9" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-9.png?raw=true">

- 위의 코드를 살펴보면 **우리가 정의한 데이터 타입(클래스, 구조체 등)에서 유용하게 사용할 수 있는 연산자도 새로 정의하거나 중복 정의할 수 있음을 알 수 있다.**

- `위의 코드의 사용자정의 연산자는 전역함수로 구현했다.`

    - 그러나 **특정 타입에 국한된 연산자 함수라면 그 타입 내부에 구현되는 것이 읽고 이해하기에 더욱 쉬울 것이다.**
    
        - **그래서 타입 내부에 타입 메서드로 구현할 수도 있다.** `아래의 코드에서 타입 메서드로 구현된 사용자정의 연산자 함수를 확인해볼 수 있다.`
        
<img width="1058" alt="basicOperatorImage-10" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-10.png?raw=true">

- `코드에서 타입 메서드로 구현한 사용자정의 연산자`는 **각 타입의 익스텐션으로 구현해도 된다.**

- 사용자정의 연산자는 굉장히 강력한 무기가 될 수 있다.

    - 복잡한 연산을 하나의 특수문자로 구현한다면 일반 함수만으로 기능을 실행하는 것보다 훨씬 강력할 것이다.

- - -
- - -