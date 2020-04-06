---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 함수 ~ 전달인자 레이블 변경을 통한 함수 중복 정의)"
date:   2020-04-04
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Function Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-04-FunctionExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- - -

### 함수 (Function)

- `함수 대부분은 작업의 가장 작은 단위이자 하나의 작은 프로그램이기도 하다.`

- `함수는 프로그램을 이루는 주된 요소 중 하나이다.`

- `스위프트에서 함수는 일급 객체이기 때문에 하나의 값으로도 사용할 수 있다.`

- - -

### 함수와 메서드 (Function and Method)

- `함수와 메서드는 기본적으로 같다.`

    - `다만 상황이나 위치에 따라 다른 용어로 부르는 것뿐이다.`
    
        - `구조체(Struct), 클래스(Class), 열거형(Enumeration) 등 특정 타입에 연관되어 사용하는 함수를 '메서드(Method)' 라고 한다.`
    
        - `모듈 전체에서 전역적으로 사용할 수 있는 함수를 그냥 '함수(Function)'라고 부른다.`
        
- `즉, 함수가 위치하거나 사용되는 범위 등에 따라 호칭이 달라질 뿐, 함수라는 것 자체에는 변함이 없다.`

- - -

### 함수의 정의와 호출

- `함수와 메서드는 정의하는 위치와 호출되는 범위만 다를 뿐, 정의하는 키워드와 구현하는 방법은 같다.`

- 조건문이나 반복문 같은 스위프트의 다른 문법과 달리 함수에서는 소괄호를 생략할 수 없다.

- `스위프트의 함수는 재정의(Override)와 중복 정의(Overload)를 모두 지원한다.`

    - 따라서 `매개변수(Parameter)의 타입이 다르면 같은 이름의 함수를 여러 개 만들 수 있고, 매개변수의 개수가 달라도 같은 이름의 함수를 만들 수 있다.`
    
- - -

### 기본적인 함수의 정의와 호출

-` 스위프트의 함수는 자유도가 굉장히 높은 문법 중 하나이다.`

- 기본으로 `함수의 이름과 매개변수(Parameter), 반환 타입(Return Type)등을 사용하여 함수를 정의한다.`

- `함수를 정의하는 키워드는 'func'이다.`

- `함수의 이름을 지정해준 후 매개변수는 소괄호로 감싸준다.`

- `반환 타입을 명시하기 전에는 '->' 를 사용하여 어떤 타입이 반환될 것인지를 명시해준다.`

- `반환을 위한 키워드는 'return'이다.`

```swift
// 함수의 기본 형태

func 함수 이름(매개변수...) -> 반환 타입 {
    실행 구문
    return 반환 값
}
```

<img width="1058" alt="functionExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-1.png?raw=true">

- - -

### 매개변수와 전달인자 (Parameter And Argument)

- `매개변수(Parameter)는 함수를 정의할 때 외부로부터 받아들이는 전달 값의 이름`을 의미한다.

- `전달인자(Argument) 혹은 인자는 함수를 실제로 호출할 때 전달하는 값`을 의미한다.

    - `예를 들어 위의 '기본적인 함수의 정의와 호출'의 그림을 보면 hello(name:) 함수에서 매개변수(Parameter)는 name이고, 실제 사용 시 전달받는 값인 "Jun"이 전달인자(Argument)이다.`
    
- - -

### 매개변수 (Parameter)

- `스위프트의 함수는 매개변수(Parameter)를 어떻게 정의하느냐에 따라서도 모습이 크게 달라질 수 있다.`

- - -

### 매개변수가 없는 함수와 매개변수가 여러 개인 함수

<img width="1058" alt="functionExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-2.png?raw=true">

- `함수에 매개변수가 필요 없다면 매개변수 위치를 공란으로 비워둔다.`

<img width="1058" alt="functionExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-3.png?raw=true">

- `매개변수가 여러 개 필요한 함수를 정의할 때는 쉼표(,)로 매개변수를 구분한다.`

- `주의할 점은 함수를 호출할 때, 매개변수 이름을 붙여주고 콜론(:)을 적어준 후 전달인자(Argument)를 보내준다는 점이다.`

- `호출 시에 매개변수에 붙이는 이름을 '매개변수 이름(Parameter Name)'이라고 한다.`

- - -

### 매개변수 이름과 전달인자 레이블 (Parameter Name And Argument Label)

- `'매개변수가 없는 함수와 매개변수가 여러 개인 함수' 파트의 2번째 그림의 코드에서 'sayHello(myName:yourName:)' 함수를 호출할 때 myName과 yourName이라는 '매개변수 이름(Parameter Name)'을 사용했다.`

- 매개변수 이름과 더불어 `'전달인자 레이블(Argument Label)'을 지정해줄 수 있다.`

- 보통 `함수를 정의할 때 매개변수를 정의하면 매개변수 이름과 전달인자 레이블 같은 이름으로 사용할 수 있지만 전달인자 레이블을 별도로 지정하면 함수 외부에서 매개변수의 역활을 좀 더 명확히 할 수 있다.`

- `전달인자 레이블을 사용하려면 함수 정의에서 매개변수 이름 앞에 한 칸을 띄운 후 전달인자 레이블을 지정한다.`

```swift
// 매개변수 이름과 전달인자 레이블을 지정할 때는 아래와 같이 표현한다.

func 함수 이름(전달인자 레이블 매개변수 이름: 매개변수 타입, 전달인자 레이블 매개변수 이름: 매개변수 타입...) -> 반환 타압 {
    실행 구문
    return 반환 값
}
```

<img width="1058" alt="functionExampleImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-4.png?raw=true">

- `함수 내부`에서 `전달인자 레이블을 사용할 수 없으며`, `함수를 호출`할 때는 `매개변수 이름을 사용할 수 없다.`

<img width="1058" alt="functionExampleImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-5.png?raw=true">

- `전달인자 레이블을 사용하고 싶지 않다면 위와 같이 와일드카드 식별자(_)를 사용하면 된다.`

- `전달인자 레이블을 변경하면 함수의 이름 자체가 변경된다.`

    - `때문에 전달인자 레이블만 다르게 써주더라도 함수 중복 정의(Overload)로 동작할 수 있다.`

- - -

### 전달인자 레이블 변경을 통한 함수 중복 정의

<img width="858" alt="functionExampleImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functionExampleImage-6.png?raw=true">
