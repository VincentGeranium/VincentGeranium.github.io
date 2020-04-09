---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 탈출 클로저)"
date:   2020-04-08
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Escaping Closure And Nonescape Closure Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-08-EscapingClosureExample-1playground.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- [값 획득 Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/07/basicSyntax-2.html)

- [동시성 프로그래밍, 비동기성 프로그래밍, 병렬성 프로그래밍 Summary](https://vincentgeranium.github.io/ios,/swift,/cs/2019/12/19/Concurrency-And-AsynchronousProgramming-Summary.html)

- - -

### 탈출 클로저 (Escaping Closures)

- `함수의 전달인자(Argument)로 전달한 클로저(Closure)가 함수(Function) 종료 후에 호출될 때 클로저가 함수를 탈출(Escape)한다고 표현한다.`

- `클로저를 매개변수(Parameter)로 갖는 함수를 선언할 때 매개변수 이름의 콜론(:) 뒤에 @escaping 키워드를 사용하여 클로저가 탈출하는 것을 허용한다고 명시해줄 수 있다.`

- 예를 들어 `비동기 작업을 실행하는 함수들은 클로저를 컴플리션 핸들러(Completion Handler) 전달인자로 받아온다.`

- `비동기 작업으로 함수가 종료되고 난 후 작업이 끝나고 호출할 필요가 있는 클로저를 사용해야 할 때 '탈출 클로저(Escaping Closures)'가 필요하다.`

- sorted(by:)메서드를 비롯해 계속 살펴보았던 함수에는 `'@escaping' 키워드를 찾아볼 수 없다.`

    - 정렬할 요소를 비교 연산하기 위해 전달인자로 전달하는 클로저는 `'비탈출 클로저(Nonescape Closures)'이기 때문이다.`
    
    - `'@escaping' 키워드를 따로 명시하지 않는다면 매개변수로 사용되는 클로저는 기본적으로 비탈출 클로저이다.`
    
    - `비탈출 클로저는 함수의 동작이 끝난 후 전달된 클로저가 필요 없을 때 사용한다.`
    
- `클로저가 함수를 탈출할 수 있는 경우 중 하나는 함수 외부에 정의된 변수나 상수에 저장되어 함수가 종료된 후에 사용할 경우이다.`

    - 예를 들어 `비동기로 작업을 하기 위해서 컴플리션 핸들러(Completion Handler)를 전달인자를 이용해 클로저 형태로 받는 함수들이 많다.`
    
    - `함수가 작업을 종료하고 난 이후(즉, 함수의 return 후)에 컴플리션 핸들러(Completion Handler), 즉 클로저를 호출하기 때문에 클로저는 함수를 탈출해(escape) 있어야만 한다.`
    
    - `함수의 전달인자(Argumetn)로 전달받은 클로저를 다시 반환(return)할 때도 마찬가지이다.`
    
- - -

### 탈출 클로저를 매개변수로 갖는 함수

<img width="1058" alt="EscapingClosureImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EscapingClosureImage-1.png?raw=true">

- `위의 코드는 탈출 클로저(Escaping Closure)와 그 클로저를 저장할 수 있는 함수 외부의 배열(Array) 변수(Variable)가 있는 것을 확인할 수 있다.`

- - -

### 함수를 탈출하는 클로저의 예

<img width="1058" alt="EscapingClosureImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EscapingClosureImage-2.png?raw=true">

- `위의 코드에서 두 함수의 전달인자로 전달하는 클로저 앞에 @escaping 키워드를 사용하여 탈출 클로저임을 명시해 주었다.`

- 이 코드는 `클로저 모두가 탈출할 수 있는 조건이 명확하기 때문에 @escaping 키워드를 사용하여 탈출 클로저임을 명시하지 않으면 컴파일 오류가 발생한다.`

- `이 코드는 함수 외부로 다시 전달되어 외부에서 사용이 가능하다든가, 외부 변수에 저장되는 등 클로저의 탈출 조건을 모두 갖추고 있다.`
    
- - -

### 클래스 인스턴스 메서드에 사용되는 탈출, 비탈출  클로저

```swift
typealias VoidVoidClosure = () -> Void
```

<img width="1058" alt="EscapingClosureImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EscapingClosureImage-3.png?raw=true">

- `위의 코드의 비탈출 클로저에서는 인스턴스의 프로퍼티인 x를 사용하기 위해 self 키워드를 생략해도 무관했지만, 탈출하는 클로저에서는 값 획득을 하기 위해 self 키워드를 사용하여 프로퍼티에 접근해야만 한다.`

- `타입 내부 메서드의 매개변수 클로저에 @escaping 키워드를 사용하여 탈출 클로저임을 명시한 경우, 클로저 내부에서 해당 타입의 프로퍼티나 메서드, 서브스크립트 등에 접근하려면 self 키워드를 명시적으로 사용해야한다.`

- `비탈출 클로저(Nonescape Closure)는 클로저 내부에서 타입 내부의 프로퍼티나 메서드, 서브스크립트 등에 접근할 때 self 키워드를 꼭 써주지 않아도 된다.`

    - 즉, 비탈출 클로저 내부에서 self 키워드는 선택 사항이다.