---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 반환 타입 ~ 데이터 타입으로서의 함수)"
date:   2020-04-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Functions Without Return Value Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-06-FunctionsWithoutReturnValueExample.playground)

- [Used Functions By Type Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-06-UsedFunctionsByTypeExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- - -

### 반환 타입 (Return Type)

- 함수는 특정 연산을 실행한 후 결괏값을 반환한다.

- 값의 반환이 굳이 필요하지 않은 함수도 있다.

    - 반환 값이 없는 함수를  만들어 줄 수 있다.
    
    - 반환 값이 없는 함수라면 반환 타입을 '없음'을  의미하는 'Void'로 표기하거나 아예 반환 타입 표현을 '생략'해도 된다.
    
        - 즉, 반환 타입이 Void이거나 생략되어 있다면 반환 값이 없는 함수이다.
        
- 함수형 프로그래밍에서 특정 로직에 관여할 함수의 매개변수와 반환 타입은 매우 중요하다.
    
    - 타입 별칭을 통해 손쉽게 함수를 관리할 수 있으며 매개변수와 반환 타입만 잘 연계된다면 훌륭한 패턴을 완성할 수 있다.
    
        - 타입 별칭을 통해 함수를 관리한 예는 아래의 '함수 타입의 사용' 파트의 그림 속 코드를 참고하면 된다.

- - -

### 반환 값이 없는 함수의 정의와 사용 (Functions Without Return Values)

<img width="1058" alt="noReturnValueFunctionImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/noReturnValueFunctionImage-1.png?raw=true">

- - -

### 테이터 타입으로서의 함수

- 스위프트의 함수는 일급 객체이므로 하나의 데이터 타입으로 사용할 수 있다.

    - 즉, 각 함수는 매개변수 타입과 반환 타입으로 구성된 하나의 타입으로 사용(정의)할 수 있다는 뜻이다.
    
- 함수를 하나의 데이터 타입으로 나타내는 방법은 아래와 같다.

```swift
(매개변수 타입의 나열) -> 반환 타입
```

- 예를 들어 아래와 같은 함수가 있다고 하자.

```swift
func sayHello(name: String, times: Int) -> String {
    // ...
}
```

- sayHello 함수의 타입은 (String, Int) -> String이다.

- 두 번째 예를 들어보면, 아래와 같은 함수가 있다고 하자.

```swift
func sayHelloToFriends(me: String, names: String...) -> String {
    // ...
}
```

- sayHelloToFriends 함수의 타입은 (String, String...) -> String 이다.

- 아래와 같이 만약 매개변수나 반환 값이 없다면 Void 키워드를 사용하여 없음을 나타낸다.

```swift
func sayHelloWorld() {
    // ...
}
```

- sayHelloWorld 함수의 타입은 (Void) -> Void 이다.

- 참고로 Void 키워드를 빈 소괄호의 묶음으로 표현할 수도 있다.

- 아래의 표현들은 모두 (Void) -> Void 와 같은 표현이다.

    - (Void) -> Void
    
    - () -> Void
    
    - () -> ()
    
- - -

### 함수 타입의 사용

- 아래의 그림에 나오는 코드는 함수를 데이터 타입으로 사용할 수 있는 간단한 예이다.

- 함수를 데이터 타입으로 사용할 수 있다는 것은 함수를 전달인자(Argument)로 받을 수도, 반환 값(Return value)으로 돌려줄 수도 있다는 의미이다.

- 상황에 맞는 함수를 전달인자로 넘겨 적절히 처리할 수도 있으며 상황에 맞는 함수를 반환해주는 것도 가능하다는 뜻이다.

- 위의 명시된 내용이 가능한 이유는 스위프트의 함수가 일급 객체이기 때문이다.

<img width="1058" alt="UsedFunctionByTypeImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UsedFunctionByTypeImage-1.png?raw=true">

- 먼저 위의 코드를 보면 두 Int 값을 입력받아 계산 후 Int 값을 돌려주는 형태의 함수를 CalculateTwoInts라는 별칭(typealias)으로 지었다.

    - 그리고 addTwoInts(_:_:)와 multiplyTwoInts(_:_:)라는 간단한 함수 두 개를 만들었다.
    
    - 두 함수는 변수 mathFunction에 번갈아가며 할당되거나 mathFunction이라는 이름으로 호출할 수도 있다.
    
    - 또 아래의 그림 속 코드처럼 전달인자(Argument)로 함수를 넘겨줄 수도 있다.
    
- - -

### 전달인자로 함수를 전달받는 함수

<img width="1058" alt="UsedFunctionByTypeImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UsedFunctionByTypeImage-2.png?raw=true">

- - -

### 특정 조건에 따라 적절한 함수를 반환해주는 함수

- 위의 코드는 반환 값으로 함수를 반환하는 예시이다.

<img width="1058" alt="UsedFunctionByTypeImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/UsedFunctionByTypeImage-3.png?raw=true">

- - -

### TIP. 전달인자 레이블과 함수 타입

- 전달인자 레이블은 함수 타입의 구성요소가 아니므로 함수 타입을 작성할 때는 전달인자 레이블을 써줄 수 없다.

```swift
let someFunction: (lhs: Int, rhs: Int) -> Int // Error!!

let someFunction: (_ lhs: Int, _ rhs: Int) -> Int // OK!!

let someFunction: (Int, Int) -> Int // OK!!
```

- - -

- 기존의 C 언어 등에서는 함수가 일급 객체가 아니었기 때문에 함수의 포인터를 사용해야 했고, 그로 인해 발생하는 다양한 문제가 있었다.

- 일급 객체가 아닌 기존 언어의 함수와 스위프트 함수와의 차이가 무엇인지, 어떤 점이 더 좋은지 등을 깊이 생각해볼 필요가 있다.

- 또, 함수가 일급 객체인 경우 어떤 상황에서 유용하게 사용할 수 있을지, 내 프로그램의 어떤 부분에서 쓸 수 있을지 고민해봐야 한다.

- - -