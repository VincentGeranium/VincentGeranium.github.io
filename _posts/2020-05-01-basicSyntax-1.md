---
layout: post
title:  "기본 문법 공부(확장(expansion) - 제네릭 함수(Generic Functions))"
date:   2020-05-01
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Generic Function Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-01-GenericFunctionExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

- - -

### 제네릭 함수(Generic Functions)

<img width="1058" alt="genericImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-2.png?raw=true" title="genericImage-2">

<img width="1058" alt="genericImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericImage-3.png?raw=true" title="genericImage-3">

<img width="1058" alt="newGenericImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/newGenericImage-4.png?raw=true" title="newGenericImage-4">

- `위의 코드들은 모두 제네릭을 사용하지 않은 함수`인데 **이 함수들의 한계점을 제네릭 함수를 통해 해결할 수 있다.**

    - `즉, 같은 타입인 두 변수의 값을 교환한다는 목적을 타입에 상관없이 할 수 있도록 단 하나의 함수로 구현할 수 있다.`
    
<img width="1058" alt="genericFuncImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/genericFuncImage-1.png?raw=true" title="genericFuncImage-1">

- 위의 코드의 swapTwoValues(_:_:) 함수는 **제네릭을 사용하여 구현한 함수**이다.

- `함수 내부의 모습은 swapTwoInts(_:_:), swapTwoStrings(_:_:) 함수 등과 특별히 다를게 없다.`

    - 그러나 **함수의 이름 뒤에 뭔가 추가된 것을 확인할 수 있다.**
    
    - 또, **매개변수의 데이터 타입도 처음보는 T 라는 알파벳이 있는 것을 볼 수 있다.**
    
- **제네릭 함수는 실제 타입 이름(Int, String 등)을 써주는 대신에 플레이스홀더(Placeholder)(위의 함수에서는 T)를 사용한다.**

- **플레이스홀더(T)는 타입의 종류를 알려주지 않지만 말 그대로 어떤 타입이라는 것은 알려준다.**

     - `즉, 매개변수로 플레이스홀더 타입이 T인 두 매개변수가 있으므로, 두 매개변수는 같은 타입이라는 정도는 알 수 있다.`
     
- **T의 실제 타입은 함수가 호출되는 그 순간 결정된다.**

    - **Int 타입의 변수가 전달인자로 전달되었다면 T는 Int가 되고, String 타입의 변수가 전달인자로 전달되었다면 그 호출 순간에 T는 String이 된다.**
    
- **제네릭 함수의 플레이스홀더를 지정하는 방법**은 **함수 이름 오른쪽의 홀화살 기호(<>) 안쪽에 플레이스홀더 이름들을 나열하는 것이다.**

    - `예를 들어 func swapTwoValues<T>에서 T가 이 함수의 플레이스홀더로 사용된다는 것을 뜻한다.`
    
    - `T가 플레이스홀더로 사용되기 때문에 스위프트 컴파일러는 함수의 문법을 검사할 때, T의 실제 타입을 신경쓰지 않는다.`
    
- **플레이스홀더 타입 T는 타입 매개변수(Type Parameter)의 한 예로 들 수 있다.**

- **타입 매개변수(Type Parameter)는 플레이스홀더 타입의 이름을 지정하고 명시하는 역활을 하며, 함수의 이름 뒤 홀화살괄호 기호(<>) 안쪽에 위치한다. <T> 처럼.**
    
- **타입 매개변수를 지정해주면** 이를 **함수의 매개변수의 타입으로 사용할 수 있다.** 또는 **함수의 반환타입으로 사용**할 수도 있으며, **함수 내부 변수의 타입 지정을 위해 사용**할 수도 있다.

    - **각각의 경우 타입 매개변수는 함수를 호출할 때마다 실제 타입으로 치환된다.**
    
        - `즉, Int 타입 변수 두 개를 통해 swapTwoValues(:_:_) 함수를 호출한다면 T는 Int로 치환되고, String 타입 변수 두 개를 통해 swapTwoValues(_:_) 함수를 호출한다면 T는 String으로 치환된다.`
        
        - **호출할 때마다 다른 타입으로 작동한다는 뜻이다.**
        
- swapTwoValues(_:_:) 함수처럼 **하나의 타입 매개변수를 갖지 않고 여러 개의 타입 매개변수**를 갖고 싶다면 **홀화살괄호 기호 안쪽에 쉼표로 분리한 여러 개의 타입 매개변수를 지정**해줄 수 있다. **<T, U, V> 처럼.**

- `타입 매개변수 대부분은 의미있는 이름을 갖게 되는 경우가 많다.`

    - `예를 들어 딕셔너리에 쓰이는 Key, Value. Dictionary<Key, Value>와 같이 표현.`
    
    - `배열에서 요소를 표현하기 위해 Array<Element>와 같이 표현.`
    
        - 이렇게 `의미있는 이름으로 타입 매개변수의 이름을 지정`해주면 `제네릭 타입 및 제네릭 함수와 타입 매개변수와의 관계를 조금 더 명확히 표현`해줄 수 있다.
        
        - 그러나 `특별히 관계의 의미를 이름으로 표현하기 어려운 때는 관용적으로 T, U, V 등의 대문자 한 글자로 표현`한다.
        
- `타입 매개변수 이름은 타입 이름이기도 하므로 대문자 카멜케이스를 사용`하여 표현한다. T, Key, Value, Element, TypeParameter과 같이 `각 단어의 첫 글자를 대문자로 표현`해준다.

- - -
- - -