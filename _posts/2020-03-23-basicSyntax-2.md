---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 초기화과정이란?, 인스턴스 생성, 프로퍼티 기본값)"
date:   2020-03-23
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Initializer Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-23-InitializerExample.playground)

- [Initializer Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-23-InitializerExample-2.playground)

- [Initializer Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-23-InitializerExample-3.playground)

- - -

### 초기화(Initializaion) 과정이란?

-` 초기화(Initializaion)는 클래스나 구조체 또는 열거형의 인스턴스를 사용하기 위한 준비 과정이다.`

- `초기화가 완료된 인스턴스는 사용 후 소멸 시점이 오면 소멸한다.`

### 인스턴스 생성

- `초기화 과정은 새로운 인스턴스를 사용할 준비를 하기 위하여 저장 프로퍼티의 초깃값을 설정하는 등의 일을 한다.`

- `이니셜라이저(Initializer)를 정의하면 초기화 과정을 직접 구현할 수 있다.`

    - `구현된 이니셜라이저`는 `새로운 인스턴스를 생성할 수 있는 특별한 메서드`가 된다.

- 스위프트의 `이니셜라이저는 반환 값이 없다.`

- `이니셜라이저의 역활`은 `그저 인스턴스의 첫 사용을 위해 초기화`하는 것뿐이다.

- `이니셜라이저는 해당 타입의 새로운 인스턴스를 생성하기 위해 호출한다.`

- - -

### 클래스, 구조체, 열거형의 기본적인 형태의 이니셜라이저

![InitializerImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerImage-1.png?raw=true)

- 위의 그림은 `매개변수가 없는 기본 이니셜라이저의 모습`이다.

- `이니셜라이저는` func 키워드를 사용하지 않고 오로지 `init 키워드`를 사용하여 `이니셜라이저 메서드임을 표현한다.`

- `init 메서드`는 `클래스, 구조체, 열거형 등의 구현부 또는 해당 타입의 익스텐션 구현부에 위치`한다.

    - 다만 `클래스의 지정 이니셜라이저는 익스텐션에서 구현해줄 수 없다.`

- - -

### 프로퍼티 기본값 (Property Default Value)

- `구조체와 클래스의 인스턴스는 처음 생성할 때 옵셔널 저장 프로퍼티를 제와한 모든 저장 프로퍼티에 적절한 초깃값(Initial Value)을 할당해야 한다.`

- `이니셜라이저가 실행될 때 저장 프로퍼티에 적절한 초깃값을 할당할 수 있다.`

- `초기화 후에 값이 확정되지 않은 저장 프로퍼티는 존재할 수 없다.`

- 프로퍼티를 정의할 때 `프로퍼티 기본값(Default Value)을 할당`하면 `이니셜라이저에서 따로 초깃값을 할당하지 않더라도 프로퍼티 기본값으로 저장 프로퍼티의 값이 초기화된다.`

- - -

### 초기화와 프로퍼티 감시자

- `이니셜라이저를 통해 초깃값을 할당`하거나, `프로퍼티 기본값을 통해 처음 저장 프로퍼티가 초기화될 때`는 `프로퍼티 감시자 메서드가 호출되지 않는다.`

- [Property Observers Summary in Vincent Blog](https://vincentgeranium.github.io/ios,/swift/2020/03/16/basicSyntax.html)

- - -

### 구조체와 이니셜라이저

![InitializerImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerImage-2.png?raw=true)

- 위의 그림에서 보면 Area 구조체는 squareMeter라는 Double 타입의 저장 프로퍼티를 가지고 있다.

- `init 이니셜라이저로 인스턴스를 초기화하며 squareMeter의 초깃값은 0.0이 된다.`

- - -

### 프로퍼티 기본값 지정

![InitializerImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerImage-3.png?raw=true)

- 위의 그림은 `프로퍼티에 기본값을 할당하는 방법이다.`

- 이니셜라이저로 저장 프로퍼티에 초깃값을 설정하는 방식도 있지만, `프로퍼티를 정의할 때 프로퍼티에 기본값을 할당하는 방식을 사용할 수도 있다.`

- `초기화 과정`은 `이니셜라이저의 매개변수(Parameter), 옵셔널 프로퍼티, 상수 프로퍼티의 값 할당 등 프로그래머의 의도대로 구현할 수 있는 수많은 패턴의 이니셜라이저가 있다.`