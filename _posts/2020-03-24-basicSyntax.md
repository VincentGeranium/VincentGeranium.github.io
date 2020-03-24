---
layout: post
title:  "기본 문법 공부(인스턴스 생성 및 소멸 - 이니셜라이저 매개변수, 옵셔널 프로퍼티 타입)"
date:   2020-03-24
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Initializer Parameter Example - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-24-InitializerParameterExample-1.playground)

- [Initializer Parameter Example - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-24-InitializerParameterExample-2.playground)

- - -

### 이니셜라이저 매개변수 (Initializer Parameter)

- 함수나 메서드를 정의할 때와 마찬가지로 `이니셜라이저도 매개변수를 가질 수 있다.`

    - `즉, 인스턴스를 초기화하는 과정에 필요한 값을 전달받을 수 있다.`
    
![InitializerParameterImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerParameterImage-1.png?raw=true)

- 위의 그림에서 보면 두 종류의 이니셜라이저를 만든것을 볼 수 있다.

    - 1) 평수를 입력받아 제곱미터로 환산한 값을 squareMeter 프로퍼티에 할당하는 이니셜라이저.
    
    - 2) 제곱미터를 입력받아 그래도 squareMeter 프로퍼티에 할당하는 이니셜라이저.
    
- 위와 같이 `사용자정의 이니셜라이저를 만들면 기존의 기본 이니셜라이저(init())는 별도로 구현하지 않는 이상 사용할 수 없다.`

- `두 번째 이니셜라이저 init(formSquareMeter squareMeter: Double)`에서는 `self 프로퍼티를 사용(self.squareMeter)하여 이니셜라이저의 전달인자(Argument) 레이블인 squareMeter와 구분지었다.`

- `세 번째 이니셜라이저에서는 따로 전달인자(Argument) 레이블을 사용하지 않았다.`

- 세 번째 이니셜라이저를 보면 별다른 의미 없는 value라는 이름의 매개변수(Parameter)가 있는데, `만약 자동으로 지정되는 전달인자 레이블 value가 필요하지 않다면 네 번째 이니셜라이저처럼 와일드카드 식별자(_)를 사용하여 전달인자 레이블을 없애주면 된다.`
    
- - -

### 옵셔널 프로퍼티 타입 (Optional Property Type)

- `초기화(Initialization)과정에서 값을 초기화하지 않아도 되는, 즉 인스턴스가 사용되는 동안에 값을 꼭 갖지 않아도 되는 저장 프로퍼티가 있다면 해당 프로퍼티를 옵셔널로 선언할 수 있다.`

- `또는 초기화 과정에서 값을 지정해주기 어려운 경우 저장 프로퍼티를 옵셔널로 선언할 수 있다.`

- `옵셔널로 선언한 저장 프로퍼티는 초기화 과정에서 값을 할당해주지 않는다면 자동으로 nil이 할당된다.`

![InitializerParameterImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/InitializerParameterImage-2.png?raw=true)

- 위의 그림에서 보면 사람의 이름은 아는데 나이는 민감한 부분이므로 모를 수 있기 때문에 age 프로퍼티를 옵셔널로 선언했다.

- 이니셜라이저에서 특별히 초기화하지 않았지만 자동으로 nil이 할당되어 있다.

- 나중에 나이를 알게 되는 시점에서 제대로 된 값을 할당할 수 있다.