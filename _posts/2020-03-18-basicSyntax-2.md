---
layout: post
title:  "기본 문법 공부(프로퍼티와 메서드 - 타입 프로퍼티)"
date:   2020-03-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [TypeProperty Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-18-TypePropertyExample.playground)

- [TypeProperty Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-18-TypePropertyExample-2.playground)

- - -

### 타입 프로퍼티

- `인스턴스 프로퍼티의 개념은 모두 타입을 정의하고 해당 타입의 인스턴스가 생성되었을 때 사용할 수 있는 프로퍼티이다.`

- `인스턴스 프로퍼티`는 `새로 생성할 때마다 초깃값에 해당하는 값이 프로퍼티의 값`이 되고, `인스턴스마다 다른 값을 지닐 수 있다.`

- 각각의 인스턴스가 아닌 `타입 자체에 속하는 프로퍼티를 타입 프로퍼티라고 한다.`

- `타입 프로퍼티`는 `타입 자체에 영향을 미치는 프로퍼티이다.`

- `인스턴스의 생성 여부와 상관없이 타입 프로퍼티의 값은 하나`이며, `그 타입은 모든 인스턴스가 공통으로 사용하는 값`(C 언어의 static constant와 유사), `모든 인스턴스에서 공용으로 접근하고 값을 변경할 수 있는 변수`(C 언어의 static 변수와 유사) 등을 `정의할 때 유용`하다.

- `타입 프로퍼티는 두 가지이다.`

    - 1) `저장 타입 프로퍼티.`
    
        - `변수 또는 상수로 선언할 수 있다.`
        
        - `반드시 초깃값을 설정`해야 하며 `지연 연산된다.`
        
        - `지연 저장 프로퍼티(Lazy Stored Property)와는 조금 다르게 다중 스레드 환경이라고 하더라도 단 한 번만 초기화된다는 보장을 받는다.`
        
        - 지연 연산이 된다고 해서 `lazy 키워드로 표시해주지는 않는다.`
    
    - 2) `연산 타입 프로퍼티.`
    
        - `변수로만 선언 할 수 있다.`
        
- - -

### 타입 프로퍼티와 인스턴스 프로퍼티

![TypePropertyExampleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypePropertyExampleImage-1.png?raw=true)

- 위의 그림에서 보듯이 `타입 프로퍼티는 인스턴스를 생성하지 않고도 사용할 수 있으며 타입에 해당하는 값이다.`

    - 그래서 `인스턴스에 접근할 필요 없이 타입 이름만으로도 프로퍼티를 사용할 수 있다.`
    
- - -

### 타입 프로퍼티의 사용

![TypePropertyExampleImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypePropertyExampleImage-2.png?raw=true)

- 위의 그림과 같이 `타입 프로퍼티를 타입 상수로 사용할 수도 있다.`