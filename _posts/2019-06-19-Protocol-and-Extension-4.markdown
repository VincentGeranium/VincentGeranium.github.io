---
layout: post
title:  "Protocol과 Extension (4)"
date:   2019-06-19
categories: iOS, Swift
---

# Protocol and Extension(4)

---

### 참고자료

이 포스트는 야곰님의 블로그 글 중 `Swift - 프로토콜, 익스텐션` 을 참고하여 쓴 포스트임을 미리 밝힙니다

아래의 링크를 클릭하시면 `야곰님의 블로그` 로 이동 할 수 있습니다

[야곰님의 블로그](https://blog.yagom.net/529)

---

#### 아래의 링크를 클릭하시면 Protocol과 Extension (1),(2),(3)을 볼 수 있습니다.

[Protocol과 Extension (1)](https://vincentgeranium.github.io/ios,/swift/2019/06/15/Protocol-and-Extension.html)

[Protocol과 Extension (2)](https://vincentgeranium.github.io/ios,/swift/2019/06/17/Protocol-and-Extensions-2.html)

[Protocol과 Extension (3)](https://vincentgeranium.github.io/ios,/swift/2019/06/18/Protocol-and-Extension-3.html)

---

# 익스텐션 문법

**Extension은** `extension`이라는 **키워드를 사용하여 선언**

```swift

extension 확장할 타입 이름 {
    // 타입에 추가될 새로운 기능 구현
}
```

익스텐션은 기존에 존재하는 타입이 추가적으로 다른 프로토콜을 채택 할 수 있도록 확장 할 수도 있다

**이런 경우에는 클래스나 구조체에서 사용하던 것과 똑같은 방법으로 프로토콜 이름을 나열해준다**

```swift

extension 확장할 타입 이름: 프로토콜1, 프로토콜2, 프로토콜3 {
    // 프로토콜 요구사항 구현
}
```

---

## 익스텐션으로 확장할 수 있는 항목

- 익스텐션을 통해 추가할 수 있는 기능에는 연산 프로퍼티, 메서드, 이니셜라이저, 서브스크립트, 중첩 데이터 타입 등이 있다

### 연산프로퍼티 추가

![addComputedProperty](https://user-images.githubusercontent.com/42841888/59694991-702d3680-9224-11e9-95dd-2b8fd8de41f2.png)

**코드 링크** [github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-18-Extension-add-computedProperty.playground)

### 메서드 추가

익스텐션을 통해 타입에 메서드를 추가할 수 있다

![addMethod](https://user-images.githubusercontent.com/42841888/59733869-49a1e680-928a-11e9-90eb-5bfc8c96017c.png)

**코드링크** [github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-19-Extension-Method.playground)

### 이니셜라이저 추가

인스턴스를 초기화(이니셜라이즈) 할 때 인스턴스 초기화에 필요한 다양한 데이터를 전달 받을 수 있도록 여러 종류의 이니셜라이저를 만들 수 있다

타입의 정의부에 이니셜라이저를 추가하지 않더라도 익스텐션을 통해 이니셜라이저를 추가할 수 있다

- 익스텐션으로 클래스 타입에 편의 이니셜라이저(convenience initializer)는 추가 가능

- 익스텐션으로 클래스 타입에 지정 이니셜라이저(Designated Initializer)는 추가 할 수 없다

- 지정 이니셜라이저(Designated Initializer)와 디이니셜라이저(Deinitializer)는 반드시 클래스 타입의 구현부에 위치해야 한다

![addinitializer](https://user-images.githubusercontent.com/42841888/59734940-6b04d180-928e-11e9-9b9c-b771be38591c.png)

**코드 링크** [github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-06-19-Extension-initializer.playground)