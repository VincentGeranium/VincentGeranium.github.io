---
layout: post
title:  "기본 문법 공부(상속(Inheritance) - 재정의(Override), 메서드 재정의(Method Override))"
date:   2020-05-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Inheritance Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-10-InheritanceExampleCode-4.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)

- - -
- - -

### 재정의 (Override)

- `자식클래스는 부모클래스로부터 물려받은 특성(인스턴스 메서드, 타입 메서드, 인스턴스 프로퍼티, 타입 프로퍼티, 서브스크립트 등)을 그대로 사용하지 않고 자신만의 기능으로 변경하여 사용할 수 있다. 이를 재정의(Override)라고 한다.`

- `상속받은 특성들을 재정의하려면 새로운 정의 앞에 override라는 키워드를 사용한다.`

- `override 키워드를 스위프트 컴파일러가 조상클래스(부모를 포함한 그 상위 부모클래스)에 해당 특성이 있는지 확인한 후 재정의하게 된다.`

- `만약 조상클래스에 재정의할 해당 특성이 없는데 override 키워드를 사용하면 컴파일 오류가 발생한다.`

- `만약 자식클래스에서 부모클래스의 특성을 재정의했을 때, 부모클래스의 특성을 자식클래스에서 사용하고 싶다면 super 프로퍼티를 사용하면 된다.`

    - **즉, 자식클래스에서 특성을 재정의 했지만 필요에 따라 부모클래스의 특성을 활용하고 싶을 때 super를 사용한다.**
    
- `super 키워드를 타입 메서드 내에서 사용한다면, 부모클래스의 타입 메서드와 타입 프로퍼티에 접근할 수 있으며 인스턴스 메서드 내에서 사용한다면, 부모클래스의 인스턴스 메서드와 인스턴스 프로퍼티, 서브스크립트에 접근할 수 있다.`

- **재정의한 someMethod()의 부모 버전을 호출하고 싶다면 super.someMethod()라고 호출하면 된다.**

- **재정의한 someProperty의 부모 버전에 접근하고 싶다면 super.someProperty라고 접근하면 된다.**

- **재정의한 서브스크립트에서 부모 버전의 서브스크립트로 접근하고 싶다면 super[index]라고 접근하면 된다.**

- - -
- - -

### 메서드 재정의 (Method Override)

- `부모클래스로부터 상속받은 인스턴스 메서드나 타입 메서드를 자식클래스에서 용도에 맞도록 재정의할 수 있다.`

<img width="1058" alt="inheritanceImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-5.png?raw=true" title="inheritanceImage-5">
<img width="1058" alt="inheritanceImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/inheritanceImage-6.png?raw=true" title="inheritanceImage-6">

- `위의 코드를 보면 Student 클래스는 Person 클래를 상속받았고, HogwartStudent 클래스는 Student 클래스를 상속받았다.`

- `Student 클래스에서 Person 클래스에 정의된 speak() 메서드를 재정의했다.`

- `HogwartStudent 클래스에서는 Person 클래스의 introduceClass() 메서드를 재정의했다.`

- `Student 클래스에서 재정의한 speak() 메서드는 HogwartStudent 클래스로 상속되었으므로 HogwartStudent 클래스의 인스턴스는 speak() 메서드를 호출하면 Student 클래스에서 재정의한 메서드가 호출된다.`

- `HogwartStudent 클래스의 introduceClass() 메서드에 override 키워드가 붙은 메서드와 그렇지 않은 메서드 두 가지가 있는 이유는 바로 반환 타입이 다르기 때문이다.`

    - **스위프트는 메서드의 반환 타입이나 매개변수가 다르면 서로 다른 메서드로 취급한다.**
    
    - **서로 다른 타입의 반환 값을 받아오기 위해 타입캐스팅 as 연산자를 사용했다.**
    
- `부모클래스의 메소드에 접근하기 위해서는 HogwartStudent 클래스의 speak()와 introduceClass() 메서드에서처럼 super 프로퍼티를 사용하면 된다.`

- - -
- - -