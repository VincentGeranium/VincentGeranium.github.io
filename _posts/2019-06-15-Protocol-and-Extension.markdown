---
layout: post
title:  "Protocol과 Extension (1)"
date:   2019-06-15
categories: iOS, Swift
---

# Protocol and Extension

---

### 참고자료

이 포스트는 야곰님의 블로그 글 중 `Swift - 프로토콜, 익스텐션` 을 참고하여 쓴 포스트임을 미리 밝힙니다

아래의 링크를 클릭하시면 `야곰님의 블로그` 로 이동 할 수 있습니다

[야곰님의 블로그](https://blog.yagom.net/529)

---

# 프로토콜 (Protocol) 

- `특정 역활을 수행하기 위한 메서드, 프로퍼티, 기타 요구사항 등의 청사진을 정의`

- 구조체(Struct), 클래스(Class), 열거형(Enum)은 프로토콜을 `채택(Adopted)`해서 특정 기능을 수행하기 위한 `프로토콜의 요구사항을 실제로 구현 할 수 있다`

- 어떤 프로토콜의 요구사항을 모두 따르는 타입은 그 `프로토콜을 준수한다(conform)`고 표현

##### 타입에서 프로토콜의 요구사항을 충족시키려면 프로토콜이 제시하는 청사진의 기능을 모두 구현해야 한다

##### 프로토콜을 기능을 정의하고 제시 할 뿐, 스스로 기능을 구현하지는 않는다

---

# Protocol 정의

![defineProtocolImage1](https://user-images.githubusercontent.com/42841888/59547125-7d23fe80-8f74-11e9-8125-4a284b766409.png)

##### 아래의 링크를 누르면 Protocol의 정의 코드 구현 파일이 있는 github repo로 이동합니다

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-16-protocol-Example.playground)

---

# Protocol 요구사항

- 프로토콜은 타입이 특정 기능을 수행하기 위해 필요한 기능을 요구

- 프로토콜이 자신을 채택한 타입에 요구하는 사항 = 프로퍼티나 메서드와 같은 기능들

- 프로토콜은 `프로퍼티, 메서드, 서브스크립트, 이니셜라이저` 등의 기능을 요구 할 수 있다

## Protocol의 프로퍼티 요구

- `프로토콜`은 자신을 채택한 타입이 어떤 `프로퍼티`를 구현해야 하는지 요구 할 수 있다

- `프로토콜은` 그 `프로퍼티의 종류(연산 프로퍼티, 저장 프로퍼티)는 따로 신경쓰지 않는다`

- `프로토콜을 채택한 타입은 프로토콜이 요구하는 프로퍼티의 이름과 타입만 맞도록 구현해주면 된다`

- `프로퍼티를 읽기 전용으로 할지 혹은 읽고 쓰기가 모두 가능하게 할지`는 프로포콜이 정해야 한다

- 프로토콜의 프로퍼티 요구사항은 항상 `var 키워드를 사용한 변수 프로퍼티로 정의된다`

- `읽기와 쓰기가 모두 가능한 프로퍼티는 프로퍼티의 정의 뒤에 (get set) 이라고 명시`

- `읽기 전용 프로퍼티는 프로퍼티의 정의 뒤에 (get) 이라고 명시`

![property-and-protocol](https://user-images.githubusercontent.com/42841888/59565545-fb28f800-908f-11e9-8708-ac9601dc90d3.png)

##### 아래의 링크를 누르면 Protocol의 프로퍼티 요구 코드 구현 파일이 있는 github repo로 이동합니다

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-16-protocol-property-Study.playground)

---

