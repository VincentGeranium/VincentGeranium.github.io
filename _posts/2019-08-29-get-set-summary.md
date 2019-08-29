---
layout: post
title:  "get, set 설명"
date:   2019-08-29
categories: iOS, Swift
---

### 이 포스트는 Stack overflow에서 나온 질문과 답변을 참고로 하여 작성하였습니다.

- 그냥 번역을 제 식에 맞게 한 것이니 불편하실 수 있습니다, 그럴 경우에 아래의 링크를 통하여 원문으로 보실 수 있으니 참고하시길 바랍니다.

[Stack Overflow](https://stackoverflow.com/questions/24699327/what-are-get-and-set-in-swift)

---

```swift

var perimeter: Double {
    get {
        return 3.0 * sideLength
    }
    set {
        sideLength = newValue / 3.0
    }
}

```

- 질문 : get과 set에 대한 내용이 책에서도 정확하게 설명이 안되어 있는데 get과 set에 대해서 설명 부탁드립니다

---

- 답변 : 저장 프로퍼티의 속성에는 getter과 setter이 있을 수 있습니다

```swift

class EquilateralTriangle: NamedShape {
...

```

- 어떤 다른 클래스가 변수를 얻길 원한다면 다음과 같이 할 수 있습니다.

```swift

let someVar = myTriangle.perimeter
```

- 이렇게 호출 되는것이죠.

```swift

get{
    return 2.0 * self.sideLength
}
```

- 본질적으로 calling controller이 수행한 경우는 아래와 같습니다.

```swift

let someVar = 3.0 * myTriangle.sideLength

```

- 다른 오브젝트에서 변수를 set 하면 다음과 같이 나타납니다.

```swift

myTriangel.perimeter = 100
```

- 그러면 이렇게 `set {}` 블록에서 코드를 호출합니다.

```swift

set{
    sideLength = newValue / 3.0
}
```

- 그리고 클래스가 이렇게 변수를 setting 하는것과 같습니다

```swift

myTriangle.sideLength = 100/3.0
```

- 다른 코드의 호출이 없어도, 언제든 3으로 곱하거나 나눌수 있습니다.

- 그 이유는 변수를 설정하거나 가져오기 직전에 수행되기 때문입니다