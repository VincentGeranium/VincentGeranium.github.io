---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 : (모나드(Monad) - 함수객체(Functor))"
date:   2020-06-09
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Functor example code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-09-ContextAndFunctorExampleCode-1.playground)

- - -
- - -

### 참고 자료

- [ZeddiOS](https://zeddios.tistory.com/449)

- [mokacoding.com](http://www.mokacoding.com/blog/functor-applicative-monads-in-pictures/)

- - -
- - -

### 함수객체(Functor)

- **함수객체는 "고차함수인 map을 적용 할 수 있는 컨테이너 타입"이다.**

    - 맵(map)은 컨테이너의 값을 변형시킬 수 있는 고차함수이다.
    
    - 옵셔널(Optional)은 컨테이너(컨텍스트가 일종의 컨테이너 역활을 한다)와 값을 갖기 때문에 맵 함수를 사용할 수 있다.
    
    - 아래의 코드처럼 맵을 사용하면 컨테이너 안의 값을 처리할 수 있다.
    
<img width="1058" alt="functorImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-1.png?raw=true" title="functorImg-1">

- 따라서 아래의 코드처럼 함수가 없어도 클로저를 사용할 수도 있다.

<img width="1058" alt="functorImg-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-2.png?raw=true" title="functorImg-2">

<img width="1058" alt="functorImg-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-3.jpg?raw=true" title="옵셔널의맵메서드를통한연산그림">

- 처음 위의 내용에서 부터 맵을 언급한 이유는 **"함수객체란 맵을 적용할 수 있는 컨테이너 타입"이라고 말할 수 있기 때문이다.**

- 맵을 사용해보았던 Array, Dictionary, Set 등등 스위프트의 많은 컬렉션 타입은 함수객체이다.

- 맵을 사용하여 컨테이너 내부의 값을 처리할 수 있다.

    - 그렇다면 맵은 어떻게 컨테이너 내부의 값을 갖고 addThree(_:) 함수를 사용할 수 있을까?
    
    - 아래의 그림을 통해 함수객체에서 맵이 어떻게 동작하는지 봐보자.
    
<img width="1058" alt="functorImg-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-4.jpg?raw=true" title="함수객체와맵메서드동작모식도">

- 위의 그림을 코드로 보자면 아래와 같이 표현할 수 있다.

```swift
extension Optional {
    func map<U>(f: Wrapped) -> U) -> U? {
    switch self {
    case .some(let x): return f(x)
    case .none: return .none
        }
    }
}

// 위 코드는 옵셔널의 맵 메서드를 코드로 참고하고자 작성한 것이므로 
// 실제 프로젝트나 플레이그라운드에서 위 코드를 작성하면 기존 맵 메서드와 충돌을 일으킨다.
```

- 옵셔널의 map(_:) 메서드를 호출하면 옵셔널 스스로 값이 있는지 switch 구문으로 판단한다.

    - 값이 있다면 전달받은 함수에 자신의 값을 적용한 결괏값을 다시 컨텍스트에 넣어 반환하고, 그렇지 않다면 함수를 실행하지 않고 빈 컨텍스트를 반환한다.

<img width="1058" alt="functorImg-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-5.jpg?raw=true" title="OptionalMap의동작모식도">

- Optional(2).map(addThree)를 실행할 때는 위의 그림과 같이 동작한다.

<img width="1058" alt="functorImg-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/functorImg-6.jpg?raw=true" title="OptionalNoneMap의동작모식도">

- 만약 값이 없는 Optional.none.map(addThree)와 같은 상황이라면 위와 같은 상황이라면 위의 그림과 같은 동작이 실행될 것이다.

    - 컨텍스트에 값이 없다면 빈 컨텍스트로 다시 반환한다.
    
- - -
- - -