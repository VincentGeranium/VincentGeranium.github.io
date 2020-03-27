---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 인스턴스 소멸)"
date:   2020-03-27
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Deinitializer Example](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-27-DeinitializerExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)

- [Initializer Summary](https://vincentgeranium.github.io/ios,/swift/2020/03/23/basicSyntax-2.html)

- - -

### 인스턴스 소멸 (Deallocated Instance, Deinitialization)

- `클래스의 인스턴스는 디이니셜라이저(Deinitializer)를 구현할 수 있다.`

- `디이니셜라이저(Deinitializer)는 이니셜라이저(Initializer)와 반대 역활을 한다.`

    - `즉, 메모리에서 해제되기 직전 클래스 인스턴스와 관련하여 원하는 정리 작업을 구현할 수 있다.`
    
- `디이니셜라이저는 클래스의 인스턴스가 메모리에서 소멸되기 바로 직전에 호출된다.`

- `deinit 키워드`를 사용하여 `디이니셜라이저를 구현하면 자동으로 호출된다.`

- `디이니셜라이저는 클래스의 인스턴스에만 구현할 수 있다.`

- `스위프트는 인스턴스가 더 이상 필요하지 않으면 자동으로 메모리에서 소멸시킨다.`

- `인스턴스 대부분은 소멸시킬 때 디이니셜라이저를 사용해 별도의 메모리 관리 작업을 할 필요는 없다.`

    - 그렇지만 예를 들어 `인스턴스 내부에서` 파일을 불러와 열어보는 등의 `외부 자원을 사용했다면 인스턴스를 소멸하기 직전에 파일을 다시 저장하고 닫아주는 등의 부가 작업을 해야한다.`
    
    - 또는 `인스턴스를 메모리에서 소멸하기 직전에 인스턴스에 저장되어 있던 데이터를 디스크에 파일로 저장해줘야 하는 경우도 있을 수 있다. 그런 경우에 디이니셜라이저는 굉장히 유용하게 사용할 수 있다.`
    
- `클래스에는 디이니셜라이저를 단 하나만 구현할 수 있다.`

- `디이니셜라이저는` 이니셜라이저와는 다르게 `매개변수를 갖지 않으며, 소괄호도 적어주지 않는다.`

- `디이니셜라이저는 자동으로 호출되기 때문에 별도의 코드로 호출할 수도 없다.`

- `디이니셜라이저는 인스턴스를 소멸하기 직전에 호출되므로 인스턴스의 모든 프로퍼티에 접근 할 수 있으며 프로퍼티의 값을 변경할 수도 있다.`

- `디이니셜라이저를 잘 활용하면 메모리 관리 측면 외에도 프로그래머가 설계한 로직에 따라 인스턴스가 메모리에서 해제되기 직전에 적절한 작업을 하도록 할 수 있다.`

- - -

### 디이니셜라이저의 구현

```swift
calss SomeClass {
    deinit {
        print("Instance will be deallocated immediately")
    }
}

var instance: SomeClass? = SomeClass()
instance = nil // Instance will be deallocated immediately
```

- - -

### FileManager 클래스의 디이니셜라이저 활용

![DeinitializerImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/DeinitializerImage-1.png?raw=true)

- 위의 그림의 코드의 클래스는 디스크 파일을 불러와 사용하는 FileManager 클래스이다.

- FileManager의 인스턴스가 파일을 불러와 사용하며, 인스턴스의 사용이 끝난 후에는 파일의 변경사항을 저장하고 다시 닫아줘야 메모리에서 파일이 해제되기 때문에 인스턴스가 메모리에서 해제되기 직전에 파일도 닫아주는 작업을 한다.