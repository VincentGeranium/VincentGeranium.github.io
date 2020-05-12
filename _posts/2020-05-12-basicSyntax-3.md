---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 재정의 방지(Preventing Overrides, final))"
date:   2020-05-12
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 재정의 방지 (Preventing Overrides, final)

- 만약 부모클래스를 상속받는 자식클래스에서 몇몇 특성을 재정의할 수 없도록 제한하고 싶다면 재정의를 방지하고 싶은 특성 앞에 final 키워드를 명시하면 된다.

    - 예를 들면 final var, final func, final class func, final subscript와 같이 표현하면 된다.
    
- 재정의를 방지한 특성을 자식클래스에서 재정의하려고 하면 컴파일 오류가 발생한다.

- 만약 클래스를 상속하거나 재정의할 수 없도록 하고싶다면 class 키워드 앞에 final 키워드를 명시해주면 된다.

    - 그렇게하면 더 이상 자식클래스를 가질 수 없다.
    
- 상속이 방지된 클래스를 다른 클래스가 상속받으려고 하면 컴파일 오류가 발생한다.

```swift
class Person {
    final var name: String = ""
    
    final funn speak() {
        print("HELLO")
    }
}

final class Student: Person {
    // Error!! Person의 name은 final을 사용하여 재정의(Override)를 할 수 없도록 했다.
    override var name: String {
        set {
            super.name = newValue
        }
        
        get {
            return "학생"
        }
    }
    
    // Error!! Person의 speak()는 final을 사용하여 재정의(Override)를 할 수 없도록 했다.
    override func speak() {
        print("저는 학생입니다.")
    }
}

// Error!!
// Student 클래스는 final을 사용하여 재정의(Override)를 할 수 없도록 했다.
class UniversityStudent: Student { }
```

- - -
- - -