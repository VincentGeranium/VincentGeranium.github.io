---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 클래스 상속(Class Inheritance, Subclassing))"
date:   2020-05-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-10-InheritanceExampleCode-2.playground)

- [Inheritance Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-10-InheritanceExampleCode-3.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 클래스 상속 (Class Inheritance, Subclassing)

- 수직으로 클래스를 확장할 수 있는 방법 = 상속

- 상속은 기반클래스를 다른 클래스에서 물려받는 것을 말한다.

- 부모클래스의 메서드, 프로퍼티 등을 재정의하거나, 기반클래스의 기능이나 프로퍼티를 물려받고 자신의 기능을 추가할 수 있다.

- 클래스 이름 뒤에 콜론을 붙이고 다른 클래스 이름을 써주면 뒤에 오는 클래스의 기능을 앞의 클래스가 상속받을 것임을 뜻한다.

```swift
class 클래스 이름: 부모클래스 이름 {
    프로퍼티와 메서드들
}
```

<img width="1058" alt="inheritanceImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-2.png?raw=true" title="inheritanceImage-2">

- 위의 코드는 Person을 상속받는 Student 클래스이다.

- 위의 코드에서 Student 클래스는 Person 클래스를 상속받았기 때문에 부모클래스가 물려준 프로퍼티와 메서드를 사용할 수 있으며 자신이 정의한 프로퍼티와 메서드도 사용할 수 있다.

<img width="1058" alt="inheritanceImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-3.png?raw=true" title="inheritanceImage-3">

- 위의 코드처럼 Person 클래스를 상속받은 Student 클래스는 다시 다른 클래스가 상속할 수 있다.

    - 즉, 어떤 클래스의 자식클래스가 다른 클래스의 부모클래스가 될 수 있다.
    
<img width="369" alt="inheritanceImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-4.png?raw=true" title="inheritanceImage-4">

- Person 클래스를 상속받은 Student 클래스는 Person의 인스턴스 메서드, 타입 메서드, 인스턴스 프로퍼티, 타입 프로퍼티, 서브스크립트 등 모든 특성을 포함하며 Student를 상속받는 HogwartStudent 클래스는 Person과 Student가 갖는 모든 특성을 포함한다.

    - 상속을 하지 못하도록 방지하는 키워드 final을 사용하면 모든 속성을 상속 받지는 않는다.

- 다른 클래스를 상속받으면 똑같은 기능을 구현하기 위하여 코드를 다시 작성할 필요가 없으므로 코드를 재사용하기 용이하고 더불어 기능을 확장할 때 기존 클래스를 변경하지 않고도 새로운 추가 기능을 구현한 클래스를 정의할 수 있다.

- - -
- - -