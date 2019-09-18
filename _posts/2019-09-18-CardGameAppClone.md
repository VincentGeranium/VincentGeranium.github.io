---
layout: post
title:  "Card Game App Clone을 하며 복습한 내용 정리(2)"
date:   2019-09-18
categories: iOS, Swift
---

### Protocol Initializer 요구

- 프로토콜은 프로퍼티, 메서드 등과 마찬가지로 특정한 이니셜라이저를 요구 할 수도 있다.

- 프로토콜에서 이니셜라이저를 요구하려면 메스드 요구와 마찬가지로 이니셜라이저를 정의하지만 구현하지는 않는다

- 이니셜라이저의 매개변수를 지정하기만 할 뿐, 중괄호를 포함한 이니셜라이저 구현은 하지 않는다.

![initiaizer](https://user-images.githubusercontent.com/42841888/59573743-6d7cf500-90ef-11e9-82e6-a4b87655021c.png)

- - -

### Protocol 상속

- 프로토콜은 하나 이상의 프로토콜을 상속받아 기존 프로토콜의 요구사항보다 더 많은 요구사항을 추가할 수 있다.

- 프로토콜 상속 문법은 클래스의 상속 문법과 유사하다.

![protocolInheritance](https://user-images.githubusercontent.com/42841888/59579557-60203480-9108-11e9-91f5-220c5706d097.png)
