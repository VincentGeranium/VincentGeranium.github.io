---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - withoutActuallyEscaping)"
date:   2020-04-09
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [withoutActuallyEscaping Function Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-09-WithoutActuallyEscapingExample-1playground.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- - -

### withoutActuallyEscaping

- 비탈출 클로저(Nonescape Closure)나 탈출 클로저(Escaping Closure)와 관련한 여러 가지 상황 중 한 가지 애매한 경우가 있다.

    - 비탈출 클로저로 전달한 클로저가 탈출 클로저인 척 해야 하는 경우이다.
    
        - 실제로는 탈출하지 않는데 다른 함수에서 탈출 클로저를 요구하는 상황에 해당한다.
        
- - -

### 오류가 발생하는 hasElements 함수

<img width="1058" alt="withoutActuallyEscapingImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/withoutActuallyEscapingImage-1.png?raw=true">

- 위의 코드에서 보면 함수 hasElements(in:match:)는 in 매개변수(Parameter)로 검사할 배열(Array)을 전달받으며, match라는 매개변수로 검사를 실행할 클로저(Closure)를 받아들인다.

    - hasElements(in:match:) 함수는 @escaping 키워드가 없으므로 비탈출 클로저(Nonescape Closure)를 전달받게 된다.

    - 그리고 내부에서 배열의 lazy 컬렉션은 비동기 작업을 할 때 사용하기 때문에 filter 메서드가 요구하는 클로저는 탈출 클로저(Escaping Closure)이다.

    - 그래서 탈출 클로저 자리에 비탈출 클로저를 전달 할 수 없다는 오류와 마주하게 된다.

- 그런데 함수 전체를 보면, match 클로저가 탈출할 필요가 없다.

    - 이때 해당 클로저를 탈출 클로저인양 사용할 수 있게 돕는 'withoutActuallyEscaping(_:do:)'함수가 있다.
    
- - -

### withoutActuallyEscaping(_:do:) 함수의 활용

<img width="1058" alt="withoutActuallyEscapingImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/withoutActuallyEscapingImage-2.png?raw=true">

- withoutActuallyEscaping(_:do:) 함수의 첫 번째 전달인자(Argument)로 탈출 클로저인 척해야 하는 클로저가 전달되었다.

    - do 전달인자(Argument)는 이 비탈출 클로저(Nonescape Closure)를 또 매개변수(Parameter)로 전달받아 실제로 작업을 실행할 탈출 클로저(Escaping Closure)로 전달받아 실제로 작업을 실행할 탈출 클로저를 전달한다.
    
- 이렇게 withoutActuallyEscaping(_:do:) 함수를 활용하여 비탈출 클로저를 탈출 클로저처럼 사용할 수 있다.