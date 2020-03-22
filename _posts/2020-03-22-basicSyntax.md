---
layout: post
title:  "기본 문법 공부(프로퍼티와 메서드 - 메서드, 인스턴스 메서드)"
date:   2020-03-22
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Instance Method Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-22-InstanceMethodExample.playground)

- [Instance Method Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-22-InstanceMethodExample-2.playground)

- [Instance Method Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-22-InstanceMethodExample-3.playground)

- [Instance Method Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-22-InstanceMethodExample-4.playground)

- - -

### 메서드 (Method)

- `메서드는 특정 타입에 관련된 함수를 뜻한다.`

- `클래스, 구조체, 열거형 등은 각각의 인스턴스가 특정 작업을 실행하는 기능을 캡슐화하기 위해 인스턴스 메서드를 정의할 수 있다.`

- `타입 자체와 관련된 기능을 실행`하기 위해 `타입 메서드를 정의`할 수도 있다.

    - 타입 메서드는 기존의 프로그래밍 언어에서의 클래스 메서드와 유사한 개념이다.
    
- 구조체와 열거형이 메서드를 가질 수 있다는 것은 기존 프로그래밍 언어와 스위프트의 큰 차이 점 중 하나다.

- 스위프트에서는 `프로그래머가 정의하는 타입(클래스, 구조체, 열거형 등)에서 자유롭게 메서드를 정의할 수 있다.`

- - -

### 인스턴스 메서드 (Instance Method)

- `인스턴스 메서드`는 `특정 타입의 인스턴스에 속한 함수를 뜻한다.`

- `인스턴스 내부의 프로퍼티 값을 변경하거나 특정 연산 결과를 반환하는 등 인스턴스와 관련된 기능을 실행한다.`

- 인스턴스 메서드와 함수는 문법이 같다.

- `인스턴스 메서드는 함수와 달리 특정 타입 내부에 구현한다.`

    - `따라서 인스턴스가 존재할 때만 사용이 가능하다. 이 점이 함수와 유일한 차이점이다.`

- - -

### 클래스의 인스턴스 메서드

![InstanceMethodImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InstanceMethodImage-1.png?raw=true)

- 위의 그림에서 보면 LevelClass의 인스턴스 메서드는 level 인스턴스 프로퍼티의 값을 수정하는 코드가 들어있다.

    - `자신의 프로퍼티 값을 수정할 때 클래스의 인스턴스 메서드는 크게 신경쓸 필요가 없다`, 그러나 `구조체나 열거형 등은 값 타입이므로 메서드 앞에 mutating 키워드를 붙여서 해당 메서드가 인스턴스 내부의 값을 변경한다는 것을 명시해야 한다.`

- - -

### mutating 키워드의 사용

![InstanceMethodImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InstanceMethodImage-2.png?raw=true)

- 위의 그림에서 보면 LevelStruct는 구조체(Struct)이다. 

- LevelStruct 구조체의 인스턴스 메서드는 level 인스턴스 프로퍼티 값을 수정하는 코드가 들어있다.

- `구조체나 열거형 등은 값 타입`이므로 `메서드 앞에 mutating 키워드를 붙여서 해당 메서드가 인스턴스 내부의 값을 변경한다는 것을 명시해야 한다.`

- - -

### self 프로퍼티

- `모든 인스턴스는 암시적으로 생성된 self 프로퍼티를 갖는다.`

    - 자바의 this와 비슷하게 인스턴스 자기 자신을 가리키는 프로퍼티이다.
    
- `self 프로퍼티는 인스턴스를 더 명확히 지칭하고 싶을 때 사용한다.`

- 위의 클래스의 인스턴스 메서드 부분의 그림의 코드처럼 level 변수를 사용할 때, `스위프트는 자동`으로 `메서드 내부에 선언된 지역변수(Local Variable)를 먼저 사용하고, 그 다음 메서드 매개변수(Parameter), 그다음 인스턴스의 프로퍼티를 찾아서 level이 무엇을 지칭하는지 유추한다.`

- 그런데 메서드 매개변수(Parameter)의 이름이 level인데, `이 level 매개변수가 아닌 인스턴스 프로퍼티인 level을 지칭하고 싶다면 self 프로퍼티를 사용한다.`

![InstanceMethodImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InstanceMethodImage-3.png?raw=true)

- 위의 그림에서 `jumpLevel(to:) 메서드의 매개변수(Parameter) 이름 level이 인스턴스 프로퍼티 level과 이름이 같다. `

    - 그럴 때 `level = level이라고 적어주면 컴파일러는 좌측의 level은 인스턴스 프로퍼티인 level보다는 매개변수로 넘어온 level을 지칭하는 것으로 판단한다.`
    
    - 그러므로 `좌측의 level을 self.level으로 적어주면 촤측의 level이 인스턴스 프로퍼티라는 것을 명확히 알 수 있다.`
    
- - -

### self 프로퍼티와 mutating 키워드

![InstanceMethodImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InstanceMethodImage-4.png?raw=true)

- `self 프로퍼티의 다른 용도`는 `값 타입 인스턴스 자체의 값을 치환할 수 있다.`

- 위의 그림을 보면 `클래스의 인스턴스는 참조 타입이라서 self 프로퍼티에 다른 참조를 할당할 수 없다.`

- `구조체나 열거형 등은 self 프로퍼티를 사용하여 자신 자체를 치환할 수도 있다.`