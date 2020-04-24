---
layout: post
title:  "기본 문법 공부(연산자(Basic Operator) - 전위 연산자 정의와 구현)"
date:   2020-04-24
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Prefix Operator Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-24-PrefixOperatorExampleCode-1.playground)

- [Prefix Operator Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-24-PrefixOperatorExampleCode-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html)

- - -

### 전위 연산자(Prefix Operator) 정의와 구현

- Int 타입의 제곱을 구하는 연산자로 '**' 을 전위연산자로 사용하려고 한다.

- 기존에 없던 전위 연산자를 만들고 싶다면 연산자 정의를 먼저 해주어야 한다.

    - 정의한다는 뜻은 '이제 이 연산자를 사용하겠다'라고 알리는 것을 뜻한다.
    
- 정의된 연산자는 모듈 전역에서 사용된다.

<img width="1058" alt="basicOperatorImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-1.png?raw=true">

- 위의 코드처럼 연산자의 정의를 마치면, 어떤 데이터 타입에 이 연산자가 동작할 것인지 함수를 구현한다.

<img width="1058" alt="basicOperatorImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-2.png?raw=true">

- 전위 연산자(Prefix Operator) 함수를 구현할 때는 함수 func 키워드 앞에 prefix 키워드를 추가해준다.

<img width="1058" alt="basicOperatorImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-3.png?raw=true">

- 스위프트 표준 라이브러리에 존재하는 전위 연산자(Prefix Operator)에 기능을 추가할 때는 따로 연산자를 정의하지 않고 함수만 중복 정의(Overload)하면 된다.

- 위의 코드에서는 기존에 존재하는 전위 연산자(Prefix Operator)중 정수(Int)에 사용되는 느낌표(!)를 문자열(String)에도 사용하고자 한다.

    - 문자열(String) 앞에 사용하면 문자열이 비어있는지 확인하는 연산자로 사용하기 위해 함수를 중복 정의(Overload)해준다.
    
<img width="1058" alt="basicOperatorImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/basicOperatorImage-4.png?raw=true">

- 위에서 만들어주었던 ** 연산자를 String 타입에서도 동작할 수 있도록 중복 정의(Overload)해줄 수도 있다.

- - -