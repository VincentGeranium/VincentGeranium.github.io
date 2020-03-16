---
layout: post
title:  "기본 문법 공부(프로퍼티 감시자 - Property Observers)"
date:   2020-03-16
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [PropertyObservers Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-16-PropertyObserversExample.playground)

- [PropertyObservers Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-16-PropertyObserversExample-2.playground)

- - -

### 프로퍼티 감시자 (Property Observers)

- `프로퍼티 감시자(Property Observers)`를 사용하면 프로퍼티의 값이 변겸됨에 따라 적절한 액션을 취할 수 있다.

- 프로퍼티 감시자는 프로퍼티의 값이 새로 할당될 때마다 호출한다.

    - 이때 변경되는 값이 현재의 값과 같더라도 호출한다.
    
- `프로퍼티 감시자`는 지연 저장 프로퍼티(Lazy Stored Properties)에 사용할 수 없으며 `오로지 일반 저장 프로퍼티에면 적용할 수 있다.`

    - 또한 `프로퍼티 재정의(Override)를` 통해 `상속받은 저장 프로퍼티 또는 연산 프로퍼티에도 적용할 수 있다.`
    
- `상속받지 않은 연산 프로퍼티`에는 프로퍼티 감시자를 사용할 필요가 없으며 할 수도 없다.

    - `연산 프로퍼티의 접근자(get)와 설정자(set)를 통해 프로퍼티 감시자를 구현할 수 있기 때문이다.`
    
- 연산 프로퍼티는 `상속받았을 때만` 프로퍼티 `재정의`를 통해 `프로퍼티 감시자를 사용한다.`

- - -

### 프로퍼티 감시자의 willSet과 didSet

- 프로퍼티 감시자에는 프로퍼티의 `값이 변경되기 직전에 호출`하는 `willSet 메서드`가 있다.

- 프로퍼티 감시자에는 프로퍼티의 `값이 변경된 직후에 호출`하는 `didSet 메서드`가 있다.

- willSet 메서드와 didSet 메서드에는 `매개변수가 하나씩 있다.`

    - `willSet 메서드`에 전달되는 `전달인자`는 `프로퍼티가 변경될 값`이다.
    
    - `didSet 메서드`에 전달되는 `전달인자`는` 프로퍼티가 변경되기 전의 값`이다.
    
        - 그래서 매개변수의 이름을 따로 지정하지 않으면 willSet 메서드에는 newValue가, didSet 메서드에는 oldValue라는 매개변수 이름이 자동 지정된다.

- - -

### 저장 프로퍼티에 프로퍼티 감시자를 구현

![PropertyObserversImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PropertyObserversImage-1.png?raw=true)

- 클래스를 상속받았다면 기존의 연산 프로퍼티를 재정의하여 프로퍼티 감시자를 구현할 수도 있다.

- 연산 프로퍼티를 재정의해도 기존의 연산 프로퍼티 기능(접근자와 설정자, get과 set 메서드)은 동작한다.

- - -

### 상속받은 연산 프로퍼티의 프로퍼티 감시자 구현

![PropertyObserversImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PropertyObserversImage-2.png?raw=true)

- 위의 그림은 연산 프로퍼티인 dollarValue가 포함되어 있는 Account 클래스를 상속받은 ForeignAccount 클래스에서 기존의 dollarValue 프로퍼티를 재정의하여 프로퍼티 감시자를 구현 한 코드이다.

- 위의 그림 아래 콘솔에 출력되는 문자열의 흐름을 통해 언제 어떤 메서드가 호출되는지 확인할 수 있다.

- - -

#### 입출력 매개변수와 프로퍼티 감시자

- 만약 프로퍼티 감시자가 있는 프로퍼티를 함수의 입출력 매개변수의 전달인자로 전달한다면 항상 willSet과 didSet 감시자를 호출한다.

    - `함수 내부에서 값이 변경되든 되지 않든 간에 함수가 종료되는 시점에 값을 다시 쓰기 때문이다.`