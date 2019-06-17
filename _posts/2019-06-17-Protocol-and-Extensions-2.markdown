---
layout: post
title:  "Protocol과 Extension (2)"
date:   2019-06-17
categories: iOS, Swift
---

# Protocol and Extension(2)

---

### 참고자료

이 포스트는 야곰님의 블로그 글 중 `Swift - 프로토콜, 익스텐션` 을 참고하여 쓴 포스트임을 미리 밝힙니다

아래의 링크를 클릭하시면 `야곰님의 블로그` 로 이동 할 수 있습니다

[야곰님의 블로그](https://blog.yagom.net/529)

---

#### 아래의 링크를 클릭하시면 Protocol과 Extension (1)을 볼 수 있습니다.

[Protocol과 Extension (1)](https://vincentgeranium.github.io/ios,/swift/2019/06/15/Protocol-and-Extension.html)

---

## 메서드 요구

- 프로토콜은 `특정 인스턴스 메서드나 타입 메서드를 요구 할 수도 있다`

- 프로토콜이 요구할 메서드는 프로토콜 정의에서 작성

- 메서드의 실제 구현부인 중괄호 부분은 제외하고 `메서드의 이름, 매개변수, 반환 타입 등만 작성`

- 프로토콜의 메서드 요구에서는 매개변수 기본값을 지정할 수 없다

- 프로토콜에서 타입 메서드를 요구할 때는 타입 프로퍼티 요구와 마찬가지로 앞에 `static` 키워드를 명시한다

- static 키워드를 사용하여 요구한 타입 메서드를 클래스에서 실제 구현할 때에는 static 키워드나 class 키워드 어느 쪽을 사용해도 무방

![methodImage](https://user-images.githubusercontent.com/42841888/59573087-3527e780-90ec-11e9-8cd8-11dd3d1cc77b.png)

##### 코드 링크

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-17-Protocol-Method.playground)

---

## 이니셜라이저 요구

- 프로토콜은 프로퍼티, 메서드 등과 마찬가지로 특정한 이니셜라이저를 요구 할 수도 있다

- 프로토콜에서 이니셜라이저를 요구하려면 메스드 요구와 마찬가지로 `이니셜라이저를 정의하지만 구현하지는 않는다`

- 이니셜라이저의 매개변수를 지정하기만 할 뿐, `중괄호를 포함한 이니셜라이저 구현은 하지 않는다`

![initImage](https://user-images.githubusercontent.com/42841888/59573743-6d7cf500-90ef-11e9-82e6-a4b87655021c.png)

##### 코드 링크

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-17-Protocol-And-Initializer.playground)

---

## 프로토콜의 상속

- `프로토콜은 하나 이상의 프로토콜을 상속받아 기존 프로토콜의 요구사항보다 더 많은 요구사항을 추가할 수 있다`

- 프로토콜 상속 문법은 클래스의 상속 문법과 유사

![protocolInheritanceImage](https://user-images.githubusercontent.com/42841888/59579557-60203480-9108-11e9-91f5-220c5706d097.png)

##### 코드 링크

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-17-Protocol-Inheritance.playground)
