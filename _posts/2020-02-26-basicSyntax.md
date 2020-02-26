---
layout: post
title:  "기본 문법 공부(구조체)"
date:   2020-02-26
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 구조체와 클래스

- 구조체와 클래스는 프로그래머가 데이터를 용도에 맞게 묶어 표현하고자 할 때 유용하다.

- 구조체와 클래스는 프로퍼티와 메서드를 사용하여 구조화된 데이터와 기능을 가질 수 있다.

- 하나의 새로운 사용자정의 데이터 타입을 만들어 주는 것이다.

- 스위프트에서 구조체와 클래스의 모습과 문법은 거의 흡사하다.

- `구조체의 인스턴스는 값 타입이고, 클래스의 인스턴스는 참조 타입이다.`

    - 구조체와 클래스를 구분하는 가장 큰 차이점.
    
- 소스파일 하나에 여러 개의 구조체와 여러 개의 클래스를 정의하고 구현해도 문제가 없다.

- 중첩 함수와 마찬가지로 구조체 안에 구조체, 클래스 안에 클래스 등과 같이 중첩 타입의 정의 및 선언이 가능하다.

- - -

### 구조체

- struct 키워드로 정의

```swift
struct 구조체 이름 {
    프로퍼티와 메서드들
}
```

![structImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/structImage-1.png?raw=true)

- 위의 그림을 보면 BasicInformation 이라는 이름으로 정의, String 타입의 name과 Int 타입인 age라는 저장 프로퍼티가 있다.

- - -

### 구조체 인스턴스의 생성 및 초기화

- 구조체 정의를 마친 후, 인스턴스를 생성하고 초기화하고자 할 때는 기본적으로 생성되는 멤버 와이즈 이니셜라이저를 사용한다.

- 구조체에 기본 생성된 이니셜라이저의 매개변수는 구조체의 프로퍼티 이름으로 자동 지정된다.

- 인스턴스가 생성되고 초기화된 후 프로퍼티 값에 접근하고 싶다면 마침표(.)를 사용하면 된다.

- 구조체를 상수 let로 선언하면 인스턴스 내부의 프로퍼티 값을 변경할 수 없다.

- 구조체를 변수 var로 선언하면 내부의 프로퍼티가 var로 선언된 경우에 값을 변경해줄 수 있다.

![structImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/structImage-2.png?raw=true)
