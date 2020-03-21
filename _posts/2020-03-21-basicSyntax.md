---
layout: post
title:  "기본 문법 공부(프로퍼티와 메서드 - 키 경로)"
date:   2020-03-21
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Key Path Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-21-KeyPathExample.playground)

- - -

### 키 경로 (Key Path)

- 함수는 일급시민으로서 상수나 변수에 참조를 할당할 수 있다.

```swift
func someFunction(paramA: Any, paramB: Any) {
    print("someFunction called...")
}

var functionReference = someFunction(paramA:paramB:)
```

- 위와 같이 함수를 참조해두고, 아래 첫 번째 줄 코드 처럼 나중에 원할 때 호출 할 수도 있다.

```swift
Line 1 - functionReference("A", "B") // someFunction called...
Line 2 - functionReference = anotherFunction(paramA:paramB:)
```

- 위의 두 번째 줄 코드 같이 다른 함수를 참조하도록 할 수도 있다.

- 프로퍼티도 이처럼 값을 바로 꺼내오는 것이 아니라 `어떤 프로퍼티의 위치만 참조하도록 할 수 있다.`

    - `바로 키 경로(Key Path)`를 `활용하는 방법`이다.

- `키 경로를 사용`하여 `간접적`으로 `특정 타입의 어떤 프로퍼티 값을 가리켜야 할지 미리 지정`해두고 `사용할 수 있다.`

- `키 경로 타입`은 `AnyKeyPath라는 클래스로부터 파생`된다.

- `제일 많이 확장된 키 경로 타입`은 `WritableKeyPath<Root, Value>`와 `ReferenceWritableKeyPath<Root, Value>` 타입이다.

    - `WritableKeyPath<Root, Value> 타입`은 `값 타입의 키 경로 타입`으로 `읽고 쓸 수 있는 경우에 적용`된다.
    
    - `ReferenceWritableKeyPath<Root, Value> 타입`은 `참조 타입`, 즉 `클래스 타입에 키 경로 타입으로 읽고 쓸 수 있는 경우에 적용`된다.
    
- `키 경로`는 `역슬래시(\)와 타입, 마침표(.) 경로로 구성`된다.

```
// 키 경로 구성

\타입 이름. 경로. 경로. 경로
```

- 여기서 `경로는 프로퍼티 이름이라고 생각하면 된다.`

- - -

### 키 경로 타입의 타입 확인

![keypathImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/keypathImage-3.png?raw=true)

- 위의 그림에서 보면 클래스는 ReferenceWritableKeyPath<Person, String>, 구조체는 WritableKeyPath<Stuff, String>

- - -

### 키 경로 타입의 경로 연결

![keypathImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/keypathImage-4.png?raw=true)

- 각 인스턴스의 `keyPath 서브스크립트 메서드에 키 경로를 전달`하여 `프로퍼티에 접근`할 수 있다.
    
- - -

### keyPath 서브스크립트와 키 경로 활용

![keypathImage-5](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/keypathImage-5.png?raw=true)

- `키 경로를 잘 활용하면` 프로토콜와 마찬가지로 `타입 간의 의존성을 낮추는 데 많은 도움을 준다.`

- 또, `애플의 프레임워크는 키 - 값 코딩 등 많은 곳에 키 경로를 활용`하므로, 위의 `키 경로에 대해 알아두면 애플 프레임워크 기반의 애플리케이션을 만들 때 많은 도움이 된다.`

- - -

### 접근수준과 키 경로

- `키 경로는 타입 외부로 공개된 인스턴스 프로퍼티에 한하여 표현할 수 있다.`