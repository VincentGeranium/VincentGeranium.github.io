---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 값 획득)"
date:   2020-04-07
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Capturing Values Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-CapturingValuesExample-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- [Closure Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/02/basicSyntax-1.html)

- [Basic Closure Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/02/basicSyntax-2.html)

- [Nested Function Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/01/basicSyntax-1.html)

- [후행 클로저, 클로저 표현 간소화 Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/07/basicSyntax-1.html)

- [동시성 프로그래밍, 비동기성 프로그래밍, 병렬성 프로그래밍 Summary](https://vincentgeranium.github.io/ios,/swift,/cs/2019/12/19/Concurrency-And-AsynchronousProgramming-Summary.html)

- - -

### 값 획득 (Capturing Values)

- `클로저는 자신이 정의된 위치의 주변 문맥을 통해 상수나 변수를 '획득(Capture)' 할 수 있다.`

- `값 획득을 통해 클로저는 주변에 정의한 상수나 변수가 더 이상 존재하지 않더라도 해당 상수나 변수의 값을 자신 내부에서 참조하거나 수정할 수 있다.`

    - 위의 설명을 하는 이유는 `클로저가 비동기 작업에 많이 사용되기 때문이다.`
    
- `클로저를 통해 비동기 콜백(Call-back)을 작성하는 경우, 현재 상태를 미리 획득해두지 않으면, 실제로 클로저의 기능을 실행하는 순간에는 주변의 상수나 변수가 이미 메모리에 존재하지 않는 경우가 발생한다.`

- `중첩 함수(Nested Function)도 하나의 클로저 형태이다, 이 중첩 함수 주변의 변수나 상수를 획득해 놓을 수도 있다.`

    - `즉, 자신을 포함하는 함수의 지역변수나 지역상수를 획득할 수 있다.`
    
- - -

### 값 획득 (Capturing Values) - 1. makeIncrementer 함수를 만들어 살펴보기.

- makeIncrementer 함수는 incrementer라는 함수를 `중첩 함수로 포함`하고 있다.

- `중첩 함수인 incrementer() 함수는 자신 주변에 있는 runningTotal 과 amount 라는 두 값을 획득한다.`

- `두 값을 획득한 후에 incrementer는 클로저로서 makeIncrementer 함수에 의해 반환된다.`

<img width="1058" alt="CapturingValuesImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CapturingValuesImage-1.png?raw=true">

- makeIncrementer 함수의 `반환 타입은 () -> Int 이다.`

    - `이는 '함수객체'를 반환한다는 의미이다.`

    - `반환하는 함수는 매개변수를 받지 않고 반환 타입은 Int인 함수로, 호출할 때마다 Int 타입의 값을 반환해준다.`
    
    - `incrementer가 반환하게 될 값을 저장하는 용도로 runningTotal을 정의했고, 0으로 초기화해두었다.`

    - 그리고 `forIncrement라는 전달인자 레이블과 amount라는 매개변수 이름이 있는 Int 타입 매개변수 하나가 있다.`

    - `incrementer() 함수가 호출될 때마다 amount의 값만큼 runningTotal 값이 증가한다.`

- `또한 값을 증가시키는 역활을 하는 incrementer라는 이름의 중첩 함수를 정의했다.`

    - `incrementer() 함수는 amount의 값을 runningTotal에 더하여 결괏값을 반환한다.`
    
```swift
// incrementer() 함수
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```

- 위의 코드처럼 `incrementer() 함수를 makeIncrementer(forIncrement:) 함수 외부에 독립적으로 떨어뜨려 놓으면 동작할 수 없는 이상한 형태가 된다.`

- `incrementer() 함수는 어떤 매개변수도 갖지 않으며, runningTotal이라는 변수가 어디있는지 찾아볼 수도 없다. 지금 위의 형태만으로는 잘못된 코드이다.`

- 그러나 '1. makeIncrementer 함수를 만들어 살펴보기.' 파트의 `그림 속 코드처럼 incrementer() 함수 주변에 runningTotal과 amount 변수가 있다면 incrementer() 함수는 두 변수의 참조를 획득할 수 있다.`

- `참조를 획득하면 runningTotal과 amount는 makeIncrementer 함수의 실행이 끝나도 사라지지 않는다.`

- 게다가 `incrementer가 호출될 때마다 계속해서 사용할 수 있다.`

- - -

### 값 획득 (Capturing Values) - 2. incrementByTwo 상수에 함수 할당

- `makeIncrementer(forIncrement:) 함수를 사용하여 incrementByTwo 라는 이름의 상수에 incrementer 함수를 할당해주었다.`

- `incrementByTwo를 호출할 때마다 runningTotal은 값이 2씩 증가한다.`

<img width="1058" alt="CapturingValuesImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CapturingValuesImage-2.png?raw=true">

- - -

### 값 획득 (Capturing Values) - 3. 각각의 incrementer의 동작

<img width="1058" alt="CapturingValuesImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/CapturingValuesImage-3.png?raw=true">

- `위의 그림 속 코드는 incrementerByTwo와는 별개의 다른 참조를 갖는 runningTotal 변숫값을 확인할 수 있다.`

- `각각의 incrementer 함수는 언제 호출이 되더라도 자신만의 runningTotal 변수를 갖고 카운트하게 된다.`

- `다른 함수의 영향도 전혀 받지 않는다. 각각 자신만의 runningTotal의 참조를 미리 획득했기 때문이다.`

- - -

### 클래스 인스턴스 프로퍼티로서의 클로저

- `클래스 인스턴스의 프로퍼티로 클로저를 할당한다면 클로저는 해당 인스턴스 또는 인스턴스 멤버의 참조를 획득할 수 있으나, 클로저와 인스턴스 사이에 강한참조 순환 문제가 발생할 수 있다.`

- 강한참조 순환 문제는 획득목록을 통해 없앨 수 있다.

- ARC의 강한참조 순환 문제에 대하여 알아보면 조금 더 쉽게 이해 갈 것이다.