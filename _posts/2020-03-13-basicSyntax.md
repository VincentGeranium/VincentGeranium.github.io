---
layout: post
title:  "기본 문법 공부(연산 프로퍼티)"
date:   2020-03-13
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

[Computed Properties Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-13-ComputedPropertyExample.playground)
[Computed Properties Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-13-ComputedPropertyExample-2.playground)
[Computed Properties Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-13-ComputedPropertyExample-3.playground)
[Computed Properties Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-13-ComputedPropertyExample-4.playground)

- - -

### 연산 프로퍼티 (Computed Properties)

- `연산 프로퍼티`는 실제 값을 저장하는 프로퍼티가 아니라, `특정 상태에 따른 값을 연산하는 프로퍼티`.

### 연산 프로퍼티 역활

- `인스턴스 내부, 외부의 값을 연산하여 적절한 값을 돌려주는 접근자(getter)의 역활`.

- `은닉화된 내부의 프로퍼티 값을 간접적으로 설정하는 설정자(setter)의 역활`.

### 연산 프로퍼티의 정의

- 클래스, 구조체, 열거형에 연산 프로퍼티를 정의할 수 있다.

- - -

### 연산 프로퍼티의 사용 이유

- 굳이 메서드를 두고 왜 연산 프로퍼티를 쓸까?

    - `인스턴스 외부`에서 `메서드를 통해` 인스턴스 `내부 값에 접근`하려면 `메서드를 두 개(접근자, 설정자)를 구현`해야 한다.
    
    - 위의 이유를 감수하고 메서드로 구현한다 해도 `두 메서드가 분산 구현`되어 `코드의 가독성이 나빠질 수 있다`.
    
    - 타인의 코드를 보는 프로그래머의 입장에서는 `프로퍼티가 메서드 형식보다 훨씬 더 간편하고 직관적이다`.
    
- - -

### 연산 프로퍼티의 단점

- `연산 프로퍼티`는 `접근자인 get 메서드만 구현`해둔 것처럼 `읽기 전용` 상태로 `구현하기 쉽지만`, `쓰기 전용 상태로 구현할 수 없다.`

    - `메서드로는 설정자 메서드만 구현`하여 `쓰기 전용 상태로 구현`할 수 있지만 `연산 프로퍼티는 불가능`하다.
    
- - -

### 메서드로 구현한 접근자와 설정자

![getterAndSetterMethodsImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/getterAndSetterMethodsImage.png?raw=true)

- oppositePoint() 메서드로 대칭점을 구할 수 있다.

- setOppositePoint(_:) 메서드로 대칭점을 설정해줘야 한다.

- 위의 그림에서 보면 `접근자와 설정자의 이름의 일관성을 유지하기 힘들다`.

- 해당 포인트에 접근할 때와 설정할 때 사용되는 `코드를 한번에 읽기도 쉽지 않다`.

- - -

### 연산 프로퍼티의 정의와 사용

![getterAndSetterComputedPropertiesImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/getterAndSetterComputedPropertiesImage.png?raw=true)

- 위의 그림에서 보다시피 `연산 프로퍼티를 사용`하면 `하나의 프로퍼티에 접근자와 설정자가 모두 모여있고`, `해당 프로퍼티가 어떤 역활을 하는지 좀 더 명확하게 표현`이 가능하다.

- 인스턴스를 사용하는 입장에서도 `마치 저장 프로퍼티를 사용하는 것처럼 편하게 사용`할 수 있다.

- - -

### 매게변수 이름을 생략한 설정자

![ExceptParameterNameOfSetterImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ExceptParameterNameOfSetterImage.png?raw=true)

- `설정자(set)의 매개변수(Parameter)로 원하는 이름을 소괄호 안에 명시해주면 set 메서드 내부에서 전달받은 전달인자(Argument)를 사용할 수 있다`.

- 관용적인 표현으로 `newValue`로 `매개변수 이름을 대신할 수 있다`.

    - 즉, `설정자의 매개변수를 표기해주지 않으면` newValue가 매개변수 이름을 대신하여 사용된다.

- - -

### 읽기 전용 연산 프로퍼티

![readOnlyComputedPropertiesImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/readOnlyComputedPropertiesImage.png?raw=true)

- 굳이 대칭점을 설정해줄 필요가 없으면 `읽기 전용(read-only)`으로 `연산 프로퍼티를 사용할 수도 있다`.

- `연산 프로퍼티를 읽기 전용으로 구현하려면 위의 그림처럼 get 메서드만 사용한다`.