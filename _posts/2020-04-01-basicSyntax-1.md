---
layout: post
title:  "기본 문법 공부(함수 - 중첩 함수)"
date:   2020-04-01
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Nested Functions Example - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-01-NestedFunctionsExample.playground)

- [Nested Functions Example - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-01-NestedFunctionsExample-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)

- - -

### 중첩 함수 (Nested Functions)

- 스위프트는 데이터 타입의 중첩이 자유롭다. 예를 들어 열거형 안에 또 하나의 '열거형'이 들어갈 수 있고 클래스 안에 또 다른 '클래스'가 들어올 수 있는 등 다른 프로그래밍 언어에서 생각하지 못했던 패턴을 자유롭게 만들어볼 수 있다.

- 함수의 중첩은 함수 안에 함수를 넣을 수 있다는 의미이다.

- 함수는 특별한 위치에 속해 있지 않는 한 모든 함수는 전역함수이다.

- 함수 안의 함수로 구현된 중첩 함수는 상위 함수의 몸통 블록 내부에서만 함수를 사용할 수 있다.

    - 중첩 함수의 사용 범위가 해당 함수 안쪽이라고 해서 아예 외부에서 사용할 수 없는 것은 아니다.
    
    - 함수가 하나의 반환 값으로 사용될 수 있으므로 중첩 함수를 담은 함수가 중첩 함수를 반환하면 밖에서도 사용할 수 있다.
    
- - -

### 원점으로 이동하기 위한 함수

- 원점이 0이고 좌로는 음수, 우로는 양수로 이루어진 보드가 있다. 특정 위치에서 원점으로 이동하는 함수를 만들려고 한다.

    - 아래의 코드는 왼쪽으로 한 칸 이동하는 함수와 오른쪽으로 한 칸 이동하는 함수, 둘 중 무엇을 호출해야 하는지 판단하는 함수를 구현했다.
    
<img width="1058" alt="NestedFunctionExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/NestedFunctionExampleImage-1.png?raw=true">

- 위의 코드는 중첩 함수를 구현하지 않고 그냥 함수를 구현하던 방식이다.

- 하지만 위의 코드에서 보면 왼쪽으로 이동하는 함수와 오른쪽으로 이동하는 함수는 사소한 기능의 차이일 뿐 원점을 찾아가는 목적은 같다.

    - 따라서 굳이 모듈 전역에서 사용할 필요가 없다.

- - -

### 중첩 함수의 사용

- 원점으로 이동하기 위한 함수 코드를 보면 중첩 함수의 구현 없이 함수를 구현하였다.

    - 원점으로 이동하기 위한 함수의 코드 중 왼쪽으로 이동하는 함수와 오른쪽으로 이동하는 함수는 사소한 기능의 차이만 있고 원점을 찾아가는 목적을 같다.
    
    - 따라서 굳이 모듈 전역에서 사용할 필요가 없다.
    
- 위와 같은 이유로 인하여 사용 범위를 한정하고자 함수를 하나의 함수 안쪽으로 배치하여 중첩 함수로 구현하고, 필요할 때만 외부에서 사용 할 수 있도록 하는 중첩 함수 구현하는 코드를 아래와 같이 구현해 보았다.

<img width="1058" alt="NestedFunctionExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/NestedFunctionExampleImage-2.png?raw=true">

- 원점으로 이동하기 위한 함수의 코드를 보면 전역함수로 구현된 goLeft(_:) 함수와 goRight(_:) 함수를 functionForMove(_:) 함수 안쪽으로 배치하여 위의 코드에서 보이듯이 중첩 함수로 구현하였다.

- 중첩 함수를 구현하면 전역함수가 많은 큰 프로젝트에서는 전역으로 사용이 불필요한 함수의 사용 범위를 조금 더 명확하고 깔끔하게 표현해줄 수 있다.