---
layout: post
title:  "Class, Struct, Enum Summary"
date:   2019-10-07
categories: iOS, Swift
---

이 포스트는 Zedd 님의 블로그 글 "Swift 기초문법 2"를 참고하여 쓴 글 임을 미리 밝힙니다

[Zedd 님의 블로그](https://zeddios.tistory.com/15?category=685736)

- - -

Swift 기초문법1 정리 코드, 자료는 아래의 레포지토리로 가면 있습니다

[Swift 기초문법 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-07-BasicSyntax-1.playground)

- - -

### Class / Struct / Enum의 대표적 차이점

- Call by reference, Call by value

- **Class = call by reference, 참조타입**

- **Struct, Enum = call by value, 값타입**

- **참조타입(call by reference) = 데이터를 전달할 때 값의 메모리 위치를 전달한다**

    - **그 데이터가 있는 "위치"를 전달했기 때문에 그 데이터를 참조하는 곳 어디서든 원본에 접근이 가능**
    
- **값타입(call by value) = 데이터를 전달할 때 값을 복사하여 전달. 즉, "사본"이다. 원본은 그대로 유지가 된다.**

- - -

### 참조타입과 값타입의 예제

[아래의 예제 코드 파일이 있는 레포지토리](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-07-referenceAndValueType.playground)

```swift

struct Point {

    var x = 0.0
    
    var y = 0.0
    
}

let point = Point.init()

var comparePoint = point

comparePoint.x = 5

print(comparePoint.x, point.x) // 5.0 0.0
```

- 위와 같이 결과가 나온 이유는 comparePoint에 point를 말 그대로 "복사"해서 comparePoint에만 값을 넣어주었기 때문이다.

```swift

class Point {

    var x = 0.0
    
    var y = 0.0
    
}

let point = Point.init()

var comparePoint = point

comparePoint.x = 5

print(comparePoint.x, point.x) // 5.0 5.0
```

- 위와 같이 결과가 나온 이유는 comparePoint, point 둘다 같은 메모리에 있는 "원본"을 접근하였기 때문이다

- - -

### 클래스와 구조체가 언제 쓰이는 것일까??