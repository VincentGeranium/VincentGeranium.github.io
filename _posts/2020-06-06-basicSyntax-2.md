---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 : (맵, 필터, 리듀스(Map, Filter, Reduce) - 리듀스(Reduce))"
date:   2020-06-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Reduce Method Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-ReduceMethodExampleCode-1.playground)

- [Reduce Method Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-ReduceMethodExampleCode-2.playground)

- [Reduce Method Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-ReduceMethodExampleCode-3.playground)

- [Reduce Method Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-ReduceMethodExampleCode-4.playground)

- - -
- - -

### 리듀스(Reduce)

- 리듀스(Reduce) 기능은 사실 결합(Combine)이라고 불러야 마땅한 기능이다.

- 리듀스는 컨테이너 내부의 콘텐츠를 하나로 합하는 기능을 실행하는 고차함수이다.

    - 배열이라면 배열의 모든 값을 전달인자로 전달받은 클로저의 연산 결과로 합해준다.
    
- 스위프트의 리듀스는 두 가지 형태로 구현되어 있다.

    - 첫 번째 리듀스는 클로저가 각 요소를 전달받아 연산한 후 값을 다음 클로저 실행을 위해 반환하며 컨테이너를 순환하는 형태이다.
    
    ```swift
    // 첫 번째 리듀스 메소드 정의
    public func reduce<Result>(_ initialResult: Result, 
        _ nextPartialResult: (Result, Element) throws -> Result) rethrows -> Result
    ```
    
    - initialResult 이라는 이름의 매개변수로 전달되는 값을 통해 초깃값을 지정해 줄 수 있다.
    
    - nextPartialResult 이라는 이름의 매개변수로 클로저를 전달받는다.
    
        - nextPartialResult 클로저의 첫 번째 매개변수는 리듀스 메서드의 initialResult 매개변수를 통해 전달받은 초깃값 또는 이전 클로저의 결괏값이다.
        
        - 모든 순회가 끝나면 리듀스의 최종 결괏값이 된다.
        
        - nextPartialResult 클로저의 두 번째 매개변수는 리듀스 메서드가 순환하는 컨테이너의 요소이다.
        
    - 두 번째 리듀스 메서드는 컨테이너를 순환하며 클로저가 실행되지만 클로저가 따로 결괏값을 반환하지 않는 형태이다.
    
        - 대신 inout(입출력 매개변수) 매개변수를 사용하여 초깃값에 직접 연산을 실행하게 된다.
        
    ```swift
    // 두 번째 리듀스 메소드 정의
    public func reduce<Result>(into initialResult: Result,
        _ updateAccumulatingResult: (inout Result, Element) throws -> ()) rethrows ->
        Result
    ```
    
    - updateAccumulatingResult 매개변수로 전달받는 클로저의 매개변수 중 첫 번째 매개변수를 inout 매개변수로 사용한다.
    
        - updateAccumulatingResult 클로저의 첫 번째 매개변수는 리듀스 메서드의 initialResult 매개변수를 이용해 전달받은 초깃값 또는 이전에 실행된 클로저 때문에 변경되어 있는 결괏값이다.
        
        - 모든 순회가 끝나면 리듀스의 최종 결괏값이 된다.
        
    - updateAccmulatingResult 매개변수로 전달받는 클로저의 매개변수 중 두 번째 매개변수는 리듀스 메서드가 순환하는 컨테이너 요소이다.
    
    - 상황에 따라서는 리듀스를 맵과 유사하게 사용할 수도 있다.
    
<img width="1058" alt="reduceImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-1.png?raw=true" title="reduceImage-1">
<img width="1058" alt="reduceImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-2.png?raw=true" title="reduceImage-2">
<img width="1058" alt="reduceImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-3.png?raw=true" title="reduceImage-3">
<img width="1058" alt="reduceImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-4.png?raw=true" title="reduceImage-4">
<img width="1058" alt="reduceImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-5.png?raw=true" title="reduceImage-5">

- 위 코드는 리듀스 메서드의 사용법이다.

<img width="1058" alt="reduceImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/reduceImage-6.png?raw=true" title="reduceImage-6">

- 리듀스도 위의 코드처럼 맵과 필터로 결합을 이룰 수 있다.