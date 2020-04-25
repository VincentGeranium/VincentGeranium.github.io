---
layout: post
title:  "기본 문법 공부(연산자(Basic Operator) - 후위 연산자 정의와 구현)"
date:   2020-04-25
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Postfix Operator Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-25-PostfixOperatorExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html)

- - -

### 후위 연산자 정의와 구현

- 후위 연산자를 사용자정의하는 방법은 사용자정의 전위 연산자를 구현한 것과 크게 다르지 않다.

<img width="1058" alt="basicOperatorImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-5.png?raw=true">

- 위의 코드는 정수 타입의 값 뒤에 '**' 를 붙이면 10을 더해주는 사용자정의 후위 연산자 정의와 함수를 구현한 코드이다.

- 후위 연산자의 함수 구현 앞에는 'postfix'라는 키워드를 붙여준다.

<img width="1058" alt="basicOperatorImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-6.png?raw=true">

- 하나의 피연산자에 전위 연산과 후위 연산을 한 줄에 사용하게 되면 후위 연산을 먼저 수행한다.

- 위의 코드를 통해 전위 연산자와 후위 연산자를 한 번에 사용하게 되면 후위 연산을 먼저 실행한다는 것을 확인할 수 있다.

- - -
- - -