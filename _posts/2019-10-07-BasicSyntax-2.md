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

### 클래스와 구조체 - 클래스

- **iOS 프레임워크의 대부분이 클래스로 구성되어있다**

![VcImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/VCimage.png?raw=true)

- ViewController 앞에 **class**키워드가 보일것이다 또 **UIViewController**를 상속받고 있다

![uiViewControllerimg](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/uiviewControllerImage.png?raw=true)

- UIViewController의 정의부분을 보면 위와 같이 되어있다. UIViewcontroller앞에 **class** 키워드가 보일것이다

- 이렇게 iOS는 클래스를 상속받아 해당 클래스, 즉 부모클래스에 있는 기능들을 자식클래스에서 쓸 수 있게된다

- 만약 iOS 프레임워크가 **구조체였다면 상속이 불가해서** 위의 그림 같이 사용할 수 없었을 것이다.

- **그래서 iOS 프레임워크에서는 클래스를 사용하연다고 할 수 있다.**

- - -

### 클래스와 구조체 - 구조체

- 그렇다면 상속도 안되는 구조체를 왜쓸까?

    - **Swift의 대부분의 큰 뼈대는 구조체이다.**
    
    - 이 **대부분의 큰 뼈대**는 무엇을 의미??
    
        - 정말 자주 쓰는 Int, Double, String...등의 타입들의 구현을 보면 이해가 갈 수 있다.
        
![DataTypeDocImage](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/IntStringDoubleDocumentImage.png?raw=true)

- 위의 그림에서도 보이듯이 Int, Double, String 데이터 타입들의 구현이 **struct(구조체)** 로 구현되어 있다

- Int 타입을 보면 public struct Int: SignInteger, Comparable, Equatable 로 되어 있다

    - 이것은 상속을 받은 것이 아니고 (구조체는 상속 불가) **프로토콜을 채택 한 것이다**
    
- **왜 이런 데이터 타입들을 정말 굳이 구현했을까?**

    - 그 이유에는 여러가지가 있겠지만 몇까지만 말해보면
    
        - 1) 속도 : 값타입은 시스템 리소스를 적게 먹는다
        
        - 2) 안정성 : 클래스는 참조타입이기 때문에 "원본"에 바로 접근이 가능하다. 구조체는 원본은 그대로 두고 "복사"가 일어나기 때문에 **원본을 지킬 수 있게 된다.** 이러한 점에서 클래스보다 좀 더 안전한 코딩이 가능하다고 볼 수 있다. 이는 여러 클래스 또는 다중스레드 환경에서 변수를 전달 할 때 유용, 변수의 복사본을 다른곳으로 보낼 수 있으며 다른 곳에서 변수값을 변경하는 것에 대해 걱정할 필요가 없다.
        
- **구조체의 주요 목적은 비교적 간단한 데이터 값을 캡슐화 하는 것이다.**

- - -

### 정리

- 구조체는 언제 사용해야 할까??

    - 참조가 아닌 **복사**를 원할 때
    
    - 자신을 **상속할 필요가 없거나** 자신이 **다른 타입을 상속 받을 필요가 없을때**
    
    - **연관된 몇몇의 값들을 모아서 하나의 데이터 타입으로 표현하고 싶을때**
    
- 클래스는 위와 반대로 생각하면 된다.

- - -

### Swift 가이드라인

- 아래의 조건중에 한가지 또는 그 이상 해당하는 경우에는 구조체를 생각하세요.

    - 구조체의 주목적이 몇몇의 연관성있는 간단한 테이터 값의 캡슐화일 경우
    
    - 구조체에 저장되는 모든 프로퍼티들이 참조보다는 복사가 예상되는 값 형식일 경우
    
    - 캡슐화된 값들이 그 구조체의 인스턴스가 할당될때나 전달될때 참조보다는 복사가 예상될 경우
    
    - 구조체가 다른 형(type)에서부터 프로퍼티나 기능이 상속될 필요가 없을 경우