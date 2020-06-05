---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트(맵, 필터, 리듀스(Map, Filter, Reduce) - 맵(Map))"
date:   2020-06-05
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Map Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-05-MapMethodExampleCode-1.playground)

- [Map Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-05-MapMethodExampleCode-2.playground)

- [Map Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-05-MapMethodExampleCode-3.playground)

- - -
- - -

### 참고 자료

- [yagom's Swift Basic](https://yagom.github.io/swift_basic/contents/22_higher_order_function/)

- - -
- - -

### 맵(Map), 필터(Filter), 리듀스(Reduce)

- 스위프트는 함수를 일급 객체로 취급한다. 따라서 함수를 다른 함수의 전달인자(Argument)로 사용할 수 있다.

- 매개변수(Parameter)로 함수를 갖는 함수를 고차함수(Higher-order function)라고 부르는데, 스위프트의 유용한 대표적인 고차함수로는 맵(Map), 필터(Filter), 리듀스(Reduce) 등이 있다.

    - 고차함수(Higher-order function)는 '다른 함수를 전달인자(Argument)로 받거나 함수실행의 결과를 함수로 반환하는 함수'를 뜻한다.

- - -
- - -

### 맵(Map)

- **맵(Map)은 자신을 호출할 때 매개변수로 전달된 함수를 실행하여 그 결과를 다시 반환해주는 함수이다.**

- 스위프트에서 맵은 배열(Array), 딕셔너리(Dictionary), 세트(Set), 옵셔널(Optional) 등에서 사용할 수 있다.

    - 조금 더 정확히 말하자면 스위프트의 Sequence, Collection 프로토콜(Protocol)을 따르는 타입과 옵셔널(Optional)은 모두 맵(Map)을 사용할 수 있다.
    
- 앱을 사용하면 컨테이너가 담고 있던 각각의 값을 매개변수를 통해 받은 함수에 적용한 후 다시 컨테이너에 포장하여 반환한다.

    - 기존 컨테이너의 값은 변경되지 않고 새로운 컨테이너가 생성되어 반환된다. 그래서 **맵은 기존 데이터를 변형(transform)**하는데 많이 사용한다.
    
<img width="1058" alt="mapImage-1" src="" title="mapImage-1">

- map 메서드의 사용법은 for-in 구문과 별반 차이가 없다.

    - 다만 코드의 재사용 측면이나 컴파일러 최적화 측면에서 본다면 성능 차이가 있다.
    
    - 또, 다중 스레드 환경일때 대상 컨테이너의 값이 스레드에서 변경되는 시점에 다른 스레드에서도 동시에 값이 변경되려고 할 때 예측하지 못한 결과가 발생하는 부작용을 방지할 수도 있다.
    
<img width="1058" alt="mapImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapImage-2.png?raw=true" title="mapImage-2">

- 위 코드는 for-in 구문과 map 메서드 사용을 비교한 코드이다.

- 위 코드를 살펴보면 map 메서드를 사용했을 때 for-in 구문을 사용한 것보다 간결하고 편리하게 각 요소의 연산을 실행하는 것을 볼 수 있다.

    - 심지어 map 메서드를 사용하면 for-in 구문을 사용하기 위하여 빈 배열을 처음 생성해주는 작업도 필요 없다.

    - 또한, 배열의 append 연산을 실행하기 위한 시간도 필요 없다.
    
<img width="1058" alt="mapImage-3" src="" title="mapImage-3">

- 위 그림은 map 메서드의 동작 모식도이다.

<img width="1058" alt="mapImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapImage-4.png?raw=true" title="mapImage-4">

- map 메서드를 사용하여 코드가 조금 더 간략해지긴 했지만, 클로저 표현식을 사용하여 표현을 더 간략화해볼 수 있다.

    - 위 코드는 클로저 표현식을 사용하여 표현을 간략화한 코드이다.
    
    - 클로저 표현을 간략화하니 조금씩 코드가 더 간결해졌다.
    
- 그런데 코드의 재사용 측면에 대해 생각해볼 필요가 있다.

    - 같은 기능을 여러 번 사용할 것이라면 하나의 클로저를 여러 map 메서드에서 사용하는 편이 좋을 것 같다.

<img width="1058" alt="mapImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapImage-5.png?raw=true" title="mapImage-5">

- 위 코드는 재사용이 가능한 코드로 재구성한 코드이다.

<img width="1058" alt="mapImage-6" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/mapImage-6.png?raw=true" title="mapImage-6">

- map 메서드는 배열에서만 사용할 수 있는 것은 아니다. 여러 컨테이너(Container) 타입에 모두 적용이 가능하다.

    - 위 코드는 다양한 종류의 컨테이너에서 map 메서드를 실행해본 결과이다.

- - -
- - -