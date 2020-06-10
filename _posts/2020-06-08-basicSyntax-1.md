---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 : (모나드(Monad) - 개요, 컨텍스트(Context))"
date:   2020-06-08
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 개요

- 스위프트에는 함수형 프로그래밍 패러다임에서 파생된 기능이나 개념이 종종 등장하는데, 이 개념(모나드 관련)을 이해하지 못하면 스위프트 기능의 절반 정도는 제대로 사용하지 못한다.

- 함수형 프로그래밍이라는 것이 단순히 고차함수를 이용한다든가, 함수를 일급 객체로 사용한다든가, 순환(재귀)함수를 사용한 로직을 구현한다는 등의 특정 기능에 국한되는 것은 아니지만 모나드와 관련된 개념을 익혀두면 나중에 좀 더 깊이 있게 함수형 프로그래밍을 이해할 수 있을 것이다.

- 모나드(Monad)는 특정한 상태로 값을 포장하는 것에서 출발한다.

    - 스위프트에서는 이를 옵셔널이라는 형태로 구현했는데 값이 있을지 없을지 모르는 상태 속에 포장하는 것이다.
    
    - 스위프트의 옵셔널은 스위프트에서 모나드를 이해하기 좋은 예 중 하나이다.
    
- 함수객체와 모나드는 특정 기능이 아닌 디자인 패턴 혹은 자료구조라고 할 수 있다.

- - -
- - -

### 컨텍스트(Context)

- 컨텍스트(Context)의 사전적 정의를 보면 '맥락', '전후 사정'등이다.

- 컨텍스트는 '콘텐츠(Contents)를 담는 그 무엇인가'를 뜻한다.

    - 즉, 물컵에 물이 담겨있으면 물은 콘텐츠이고 물컵은 컨텍스트라고 볼 수 있다.
    
- 컨택스트에 대해 알아보기 전에 옵셔널을 다시 한번 되새겨볼 필요가 있다.

    - 옵셔널은 열거형으로 구현되어 있어서 열거형 case의 연관 값을 통해 인스턴스 안에 연관 값을 갖는 형태이다.
    
    - 옵셔널에 값이 없다면 열거형의 .none case로, 값이 있다면 열거형의 .some(value) case로 값을 지니게 된다.
    
    - 옵셔널의 값을 추출한다는 것은 열거형 인스턴스 내부의 .some(value) case의 연관 값을 꺼내오는 것과 같다.
    
- 2라는 숫자를 옵셔널로 둘러싸면, 컨텍스트 안에 2라는 콘텐츠가 들어가는 모양새이다.

    - 그리고 '컨텍스트는 2라는 값을 가지고 있다'고 말할 수 있다.
    
    - 만약 값이 없는 옵셔널 상태라면 '컨텍스트는 존재하지만 내부에 값이 없다'고 할 수 있다.
    
        - 이처럼 값(콘텐츠)과 컨텍스트의 관계를 이해하는 것이 컨텍스트를 공부하는 것의 출발점이다.
        
<img width="1058" alt="contextImg-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/contextImg-1.jpg?raw=true" title="컨텍스트박스이미지">

- 옵셔널은 some과 none라는 두 가지의 컨텍스트를 갖는다.

```swift
// addThree 함수

func addThree(_ num: Int) -> Int {
    return num + 3
}
```

- 위 코드의 함수는 Int 타입의 값을 전달받아 3을 더하여 반환하는 함수이다.

- 위 코드의 addThree(_:) 함수의 전달인자(Argument))로 컨텍스트에 들어있지 않는 순수 값인 2를 전달하면 정상적으로 함수를 실행할 수 있다.

    - addThree(_:) 함수는 매개변수(Parameter)로 일반 Int 타입의 값을 받기 때문이다.

<img width="1058" alt="contextImg-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/contextImg-2.jpg?raw=true" title="addThree(_:)함수의동작이미지">

```swift
// 일반 값을 연산할 수 있는 addThree(_:) 함수

addThree(2) // 5
```

```swift
// 옵셔널을 연산할 수 없는 addThree 함수

addThree(Optional(2)) // Error !!
```

- 그러나 위 옵셔널을 연산할 수 없는 addThree 함수의 코트처럼 옵셔널을 전달인자(Argument)로 사용하려고 한다면 오류가 발생한다.

    - 순수한 값이 아닌 무언가(여기서 옵셔널의 some)로 둘러싸인 컨텍스트가 전달되었기 때문이다.
    
<img width="1058" alt="contextImg-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/contextImg-3.jpg?raw=true" title="addThree(_:)함수가받아들일수없는옵셔널이미지">

- - -
- - -