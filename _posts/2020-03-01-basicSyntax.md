---
layout: post
title:  "기본 문법 공부(프로퍼티, 저장 프로퍼티)"
date:   2020-03-01
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

오늘은 제101주년 3.1절 입니다.

3.1절은 1919년 3월 1일, 한민족이 일본의 식민통치에 항거하고, 독립선언서를 발표하여 한국의 독립 의사를 세계 만방에 알린 날을 기념하는 국경일입니다.

조국을 위해 희생하신 모든 분들에게 존경과 감사의 인사를 드리며, 순국선열의 희생정신을 절대 잊지 않도록 하겠습니다.

- - -

### 프로퍼티

- 프로퍼티(Property)는 클래스, 구조체 또는 열거형 등에 관련된 값을 뜻한다.

- 메서드(Method)는 특정 타입에 관련된 함수를 말한다.

- `변수나 상수, 함수등이 어떤 목적으로 쓰이느냐, 어디에서 어떻게 쓰이느냐에 따라 용어가 조금씩 달라질 뿐이다.`

- 프로퍼티는 크게 `Stored Properties 저장 프로퍼티`, `Computed Properties 연산 프로퍼티`, `Type Properties 타입 프로퍼티`로 나눌 수 있다.

- 저장 프로퍼티는 인스턴스의 변수 또는 상수를 의미한다.

- 연산 프로퍼티는 값을 저장한 것이 아니라 특정 연산을 실행한 결괏값을 의미한다.

- 연산 프로퍼티는 클래스, 구조체, 열거형에 쓰일 수 있다.

- 저장 프로퍼티는 구조체와 클래스에서만 사용할 수 있다.

- 저장 프로퍼티와 연산 프로퍼티는 특정 타입의 인스턴스에 사용되는 것을 뜻하지만 특정 타입에 사용되는 프로퍼티도 존재한다. 이를 타입 프로퍼티라고 한다.

- 정리해보자면 기존 프로그래밍 언어에서 사용되던 인스턴스 변수는 저장 프로퍼티로, 클래스 변수는 타입 프로퍼티로 구분지을 수 있다.

- 더불어, 프로퍼티의 값이 변하는 것을 감시하는 `Property Observers 프로퍼티 감시자`도 있다

- Property Observers (프로퍼티 감시자)는 프로퍼티의 값이 변할 때 값의 변화에 따른 특정 액션을 실행한다.

- Property Observers (프로퍼티 감시자)는 저장 프로퍼티에 적용할 수 있으며 부모 클래스로부터 상속받을 수 있다.

- - -

### 저장 프로퍼티(Stored Property)

- 클래스 또는 구조체의 인스턴스와 연관된 값을 저장하는 가장 단순한 개념의 프로퍼티이다.

- 저장 프로퍼티는 var 키워드를 사용, 변수 저장 프로퍼티가 된다. 

- 저장 프로퍼티는 let 키워드를 사용, 상수 저장 프로퍼티가 된다.

- 저장 프로퍼티를 정의할 때 프로퍼티 기본값을 지정할 수 있으며, 초기화할 때 초깃값을 지정해줄 수도 있다.

- - -

### 구조체와 클래스의 저장 프로퍼티

- 구조체의 저장 프로퍼티가 옵셔널이 아니더라도, 구조체는 저장 프로퍼티를 모두 포함하는 이니셜라이저를 자동으로 생성한다.

- 클래스의 저장 프로퍼티는 옵셔널이 아니라면 프로퍼티 기본값을 지정해주거나 사용자정의 이니셜라이저를 통해 반드시 초기화해주어야 한다.

- 클래스 인스턴스의 상수 프로퍼티는 인스턴스가 초기화(이니셜라이즈) 될 때 한 번만 값을 할당할 수 있으며, 자식 클래스에서 이 초기화를 변경(재정의) 할 수 없다.

- - -

### 저장 프로퍼티의 선언 및 인스턴스 생성

![PropertyImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PropertyImage-1.png?raw=true)

- 구조체는 프로퍼티에 맞는 이니셜라이저를 자동으로 제공하지만 클래스는 그렇지 않아서 클래스 인스턴스의 저장 프로퍼티를 사용하는 일은 좀 번거롭다.

- 클래스의 저장 프로퍼티에 초깃값을 지정해주면 따로 사용자정의 이니셜라이저를 구현해줄 필요가 없다

- - -

### 저장 프로퍼티의 초깃값 지정

![PropertyImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PropertyImage-2.png?raw=true)

- 초깃값을 미리 지정하니 인스턴스를 만드는 과정이 훨씬 간편해졌다. 그러나 의도와 맞지 않게 인스턴스가 사용될 가능성이 남아있고, 인스턴스를 생성한 후에 원하는 값을 일일이 할당해야 해서 불편하다.

- Position의 name 프로퍼티는 한 번 값을 할당해준 후에 변경하지 못하도록 상수로 정의해주고 싶은데, 인스턴스를 생성한 후에 값을 할당해주어야 하기 때문에 그렇게 할 수 없다.

- 인스턴스를 생성할 때 이니셜라이저를 통해 초깃값을 보내야 하는 이유는 프로퍼티가 옵셔널이 아닌 값으로 선언되어 있기 때문이다.

    - 그러므로 인스턴스를 생성할 때 프로퍼티에 값이 꼭 있는 상태여야 한다
    
- 저장 프로퍼티의 값이 있어도 그만, 없어도 그만인 옵셔널이라면 굳이 초깃값을 넣어주지 않아도 된다.

    - 즉, 이니셜라이저에서 옵셔널 프로퍼티에 꼭 값을 할당해주지 않아도 된다.
    
- - -

### 옵셔널 저장 프로퍼티

![PropertyImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/PropertyImage-3.png?raw=true)

- 위의 그림은 옵셔널의 사용과 사용자정의 이니셜라이저를 적절히 혼합하여 의도에 맞는 구조체와 클래스를 정의.

- 위의 그림과 같이 옵셔널과 이니셜라이저를 적절히 사용하면 다른 프로그래머가 사용할 때, 내가 처음 의도했던 대로 구조체와 클래스를 사용할 수 있도록 유도할 수 있다.