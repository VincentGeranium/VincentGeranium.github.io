---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 종료되지 않는 함수, 반환 값을 무시할 수 있는 함수)"
date:   2020-04-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Nonreturning Function(Method) Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-06-NonreturningFunctionExample.playground)

- [discardable Result Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-06-discardableResultExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- - -

### 종료되지 않는 함수 (Nonreturning Function and Nonreturning Method)

- `스위프트에는 종료(return)되지 않는 함수가 있다.`

    - `종료되지 않는다는 의미는 정상적으로 끝나지 않은 함수라는 뜻이다.`

    - 이를 `비반환 함수(Nonreturning function)또는 비반환 메서드(Nonreturning method)`라고 한다.

- `비반환 함수 또는 비반환 메서드는 정상적으로 끝날 수 없다.`

    - `비반환 함수 또는 메서드를 실행하면 프로세스 동작은 끝났다고 볼 수 있다.`
    
- `비반환 함수 또는 비반환 메서드 안에서는 오류를 던진다든가, 중대한 시스템 오류를 보고하는 등의 일을 하고 프로세스를 종료해 버린다.`

- 비반환 함수 또는 비반환 메서드는 `어디서든 호출이 가능하고 guard 구문의 else 블록에서도 호출이 가능하다.`

- 비반환 함수 또는 비반환 메서드는 `재정의(Override) 할 수 있지만 비반환 타입(Never)이라는 것은 변경할 수 없다.`

- `비반환 함수 또는 비반환 메서드는 반환 타입을 Never라고 명시해주면 된다.`

- - -

### 비반환 함수의 정의와 사용

<img width="1058" alt="nonreturningFunctionImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/nonreturningFunctionImage-1.png?raw=true">

- 위의 그림에 나온 함수는 아에 실행이 되지 않은 것처럼 보이지만 실제로 코드를 playground에서 실행해 보면 `프로세스가 종료가 된 뒤 오류가 보고가 된다.`

<img width="1058" alt="nonreturningFunctionImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/nonreturningFunctionImage-2.png?raw=true">

- `someFunction(isAllIsWell: true)는 정상적으로 함수가 실행되고 모든 프로세스가 종료된 후 콘솔에 All is well을 나타낸다.`

- 그러나 `첫 번째 그림에서 설명했다시피 someFunction(isAllIsWell: false)일 경우에는 모든 프로세스가 종료된 후 오류를 보고하는 것을 알 수 있다.`

    - `프로세스가 종료된 후 오류를 보고하는 것은 아래 콘솔을 보면 알 수 있듯이 '마을에 도둑이 들었습니다!'를 출력한 후 오류 보고 메시지를 콘솔에서 나타내므로 모든 프로세스가 종료된 후 오류를 보고한다.`
    
- - -

### 반환 값을 무시할 수 있는 함수

- `가끔 함수의 반환 값이 꼭 필요하지 않은 경우도 있다.`

- `프로그래머가 의도적으로 함수의 반환 값을 사용하지 않을 경우 컴파일러가 함수의 결과 값을 사용하지 않았다는 경고를 보낼 때도 있다.`

    - `이런 경우 함수의 반환 값을 무시해도 된다는 @discardableResult 선언 속성을 사용하면 된다.`

<img width="1058" alt="discardableResultImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/discardableResultImage-1.png?raw=true">

- @discardableResult 선언 속성은 스위프트 표준 라이브러리 메서드에도 종종 사용한다.

- `어떤 상황에서 해당 속성을 사용하는지 라이브러리에 구현된 함수나 메서드를 살펴보면 많은 힌트를 얻을 수 있을 것이다.`