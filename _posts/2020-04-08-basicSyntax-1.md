---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 클로저는 참조 타입)"
date:   2020-04-08
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Reference Type Closure Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-08-ReferenceTypeClosureExample-1playground.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- [값 획득 Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/07/basicSyntax-2.html)

- - -

### 클로저는 참조 타입

- [값 획득(Capturing Values) Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/07/basicSyntax-2.html)의 그림 속 코드에서 incrementByTwo와 incrementByTen은 모두 상수이다.

    - 이 두 상수 클로저는 값 획득(Capturing Values)를 통해 runningTotal 변수를 계속해서 증가시킬 수 있다. 그 이유는 함수와 클로저는 참조 타입이기 때문이다.
    
- 함수나 클로자를 상수나 변수에 할당할 때마다 사실은 상수나 변수에 함수나 클로저의 참조를 설정하는 것이다.

    - 다시 말하자면 incrementByTwo라는 상수에 클로자를 할당한다는 것은 클로저의 내용물, 즉 값을 할당하는 것이 아니라 해당 클로저의 참조를 할당하는 것이다.
    
    - 결국 클로저의 참조를 다른 상수에 할당해준다면 이는 두 상수가 모두 같은 클로저를 가리킨다는 뜻이다.
    
- - -

### 참조 타입인 클로저

<img width="1058" alt="ReferenceTypeClosureImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ReferenceTypeClosureImage-1.png?raw=true">

- 위의 코드를 보면 두 상수는 같은 클로저를 참조하기 때문에 동일한 클로저가 동작하는 것을 확인할 수 있다.

- - -