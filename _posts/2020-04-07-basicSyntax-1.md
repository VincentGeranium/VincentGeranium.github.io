---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 후행 클로저, 클로저 표현 간소화)"
date:   2020-04-07
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Trailing Closure Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-TrailingClosureExample-1.playground)

- [Trailing Closure Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-TrailingClosureExample-2.playground)

- [Trailing Closure Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-TrailingClosureExample-3.playground)

- [Trailing Closure Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-TrailingClosureExample-4.playground)

- [Trailing Closure Example Code - 5](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-07-TrailingClosureExample-5.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- [Closure Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/02/basicSyntax-1.html)

- [Basic Closure Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/02/basicSyntax-2.html)

- - -

### 후행 클로저 (Trailing Closures) 

- 함수나 메서드의 마지막 전달인자(Argument)로 위치하는 클로저는 함수나 메서드의 소괄호를 닫은 후 작성해도 된다.

- 클로저가 조금 길어지거나 가독성이 조금 떨어진다 싶르면 '후행 클로저(Trailing Closure)' 기능을 사용하면 좋다.

- Xcode에서 자동완성 기능을 사용하면 자동으로 후행 클로저로 유도한다.

- 단, 후행 클로저는 맨 마지막 전달인자로 전달되는 클로저에만 해당되므로 전달인자로 클로저 여러 개를 전달할 때는 맨 마지막 클로저만 후행 클로저로 사용할 수 있다.

- 'sorted(by:)' 메서드처럼 단 하나의 클로저만 전달인자로 전달하는 경우에는 소괄호를 생략해줄 수도 있다.

- - -

### 후행 클로저 표현 (Trailing closures expression)

<img width="1058" alt="TrailingClousureImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TrailingClousureImage-1.png?raw=true">
<img width="1058" alt="TrailingClousureImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TrailingClousureImage-2.png?raw=true">

- 위 그림에 나오는 코드는 두 가지 케이스(소괄호를 닫은 후 작성, 소괄호를 생략) 모두 사용해본 코드이다.

- - -

### 클로저 표현 간소화 - 1. 문맥을 이용한 타입 유추 (Inferring parameter and return value types from context)

- 메서드의 전달인자(Argument)로 전달하는 클로저(Closure)는 메서드(Method)에서 요구하는 형태로 전달해야 한다.

    - 즉, 매개변수(Parameter)의 타입이나 개수, 반환 타입(Return Type)등이 같아야 전달인자로서 전달할 수 있다.
    
    - 이를 다르게 말하면, 전달인자로 전달할 클로저는 이미 적합한 타입을 준수하고 있다고 유출할 수 있다.
    
        - 문맥에 따라 적절히 타입을 유추할 수 있는 것이다.
        
        - 그래서 전달인자로 전달하는 클로저를 구현할 때는 매개변수의 타입이나 반환 값의 타입을 굳이 표현해주지 않고 생략하더라도 문제가 없다.
        
- - -

### 클로저의 타입 유추 (1.문맥을 이용한 타입 유추) - 매개변수의 타입이 생략된 클로저

```swift
// sorted(by:) 메서드의 정의
public func sorted(by areInIncresingOrder: (Element, Element) -> Bool) -> [Element]
```

- 메서드의 전달인자로 전달하는 클로저는 메서드에서 요구하는 형태로 전달해야 하므로 위의 sorted(by:) 메서드의 정의에서 보다시피 위와 같은 형태로 전달해줘야 한다.

<img width="1058" alt="WithoutParameterTypeClosureImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/WithoutParameterTypeClosureImage-1.png?raw=true">

- 전달인자로 전달할 클로저는 이미 적합한 타입을 준수하고 있다고 유출할 수 있으므로 위의 코드와 같이 매개변수의 타입과 반환 타입을 생략할 수 있다.

- - -

### 클로저 표현 간소화 - 2. 단축 인자 이름 (Shorthand argument name)

- 위의 예시로 들어온 모든 'sorted(by:)' 메서드로 전달하는 클로저를 살펴보면 의미없어 보이는 두 매개변수 이름 'first'와 'second'가 있다.

- 스위프트는 간결하게 표현할 수 있도록 단축 인자 이름을 제공한다.

    - 단축 인자 이름은 첫 번째 전달인자부터 '$0, $1, $2, $3, ...' 순서로 '$'와 '숫자'의 조함으로 표현한다.

- 단축 인자 표현을 사용하게 되면 매개변수 및 반환 타입과 실행 코드를 구분하기 위해 사용했던 키워드 'in'을 사용할 필요도 없어진다.

- - -

### 단축 인자 이름 사용 (2.단축 인자 이름) - 단축 인자 이름을 사용한 클로저 표현

<img width="1058" alt="shortArgumentNameImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/shortArgumentNameImage-1.png?raw=true">

- - -

### 클로저 표현 간소화 - 3. 암시적 반환 표현 (Implicit returns form single-expression closures)

- 클로저에서는 return 키워드마저 생략이 가능하다.

- 만약 클로저가 반환 값을 갖는 클로저이고 클로저 내부의 실행문이 단 한 줄이라면, 암시적으로 그 실행문을 반환 값으로 사용할 수 있다.

- - -

### 암시적 반환 표현의 사용(3.암시적 반환 표현) - 암시적 반환 표현을 사용한 클로저

<img width="1058" alt="ImplicitReturnsImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ImplicitReturnsImage-1.png?raw=true">

- - -

### 클로저 표현 간소화 - 4. 연산자 함수(Operator Method)

- 클로저의 장점은 간단한 표현이다.

- '비교 연산자'는 두 개의 피연산자를 통해 'Bool 타입'의 반환을 준다.

- sorted(by:) 메서드에 전달한 클로저와 동일한 조건이다.

- 클로저는 매개변수의 타입과 반환 타입이 '연산자'를 구현한 함수의 모양과 동일하다면 연산자만 표기하더라도 알아서 연산하고 반환한다.

- 연산자는 일종의 함수이다.

    - 스위프트 라이브러리에서 사용하는 비교 연산자의 정의를 보면 아래와 같다
    
```swift
// 연산자 정의
public func ><T : Comparable>(lhs: T, rhs: T) -> Bool
```

- func 키워드를 보면 알 수 있듯이 연산자는 함수이다.

- 함수는 클로저의 일종이다.

- 위의 연산자 정의 코드를 보면 '>' 자체가 함수의 이름이다.

- 위의 함수는 전달인자로 보내기에 충분한 조건을 가지고 있다.

- - -

### 클로저로서의 연산자 함수 사용( 4. 연산자 함수) - 연산자 함수를 클로저의 역활로 사용

<img width="1058" alt="operatorMethodImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/operatorMethodImage-1.png?raw=true">

- - -