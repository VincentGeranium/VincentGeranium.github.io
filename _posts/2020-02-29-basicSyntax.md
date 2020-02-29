---
layout: post
title:  "기본 문법 공부(값 타입과 참조 타입)"
date:   2020-02-29
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 값 타입과 참조 타입

- 값 타입과 참조 타입의 `가장 큰 차이는 '무엇이 전달되느냐'이다.`

    - 구조체는 값 타입이고 클래스는 참조 타입이다.
    
- 어떤 함수의 전달인자(Argument)로 `값 타입`의 값을 넘긴다면 `전달될 값이 복사`되어 전달된다.

- 어떤 함수의 전달인자(Argument)로 `참조 타입`을 넘긴다면 전달될 값을 복사하지 않고 `참조(주소)가 전달`된다.

    - 함수의 전달인자(Argument)로 넘길 때도 참조가 전달되며 다른 변수 또는 상수에 할당될 때도 참조가 할당된다.

- 참조라는 것은 C 언어, C++, Objective-C 등의 언어에서 사용되는 포인터(Pointer)와 매우 유사한 개념이다.

- 참조라는 것을 표현해주기 위하여 애스터리스크(*)를 사용하지 않는다.

- - -

![ValueAndReferenceImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ValueAndReferenceImage-1.png?raw=true)

![ValueAndReferenceImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ValueAndReferenceImage-2.png?raw=true)

- 값 타입의 데이터를 함수의 전달인자(Argument)로 전달하면 메모리에 전달인자를 위한 인스턴스가 새로 생성된다.

- 생성된 새 인스턴스에는 전달하려는 값이 복사되어 들어간다.

- 반면 참조 타입의 데이터는 전달인자(Argument)로 전달할 때는 기존 인스턴스의 참조를 전달하므로 새로운 인스턴스가 아닌 기존의 인스턴스 참조를 전달한다.

- 함수의 전달인자(Argument)뿐만 아니라 새로운 변수에 할당될 때 또한 마찬가지이다.

- - -

### 클래스의 인스턴스 끼리 참조가 같은지 확인

- 클래스의 인스턴스끼리 참조가 같은지 확인할 때는 `Identity Operator(식별 연산자)`를 사용한다.

- Identity Operator를 사용하여 두 참조가 같은 인스턴스를 가리키고 있는지 비교해보는 것이다.

![IdentityOperatorImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/IdentityOperatorImage-1.png?raw=true)