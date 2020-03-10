---
layout: post
title:  "기본 문법 공부(지연 저장 프로퍼티)"
date:   2020-03-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 지연 저장 프로퍼티

- 인스턴스를 생성할 때 프로퍼티에 값이 필요 없다면 프로퍼티를 옵셔널로 선언해줄 수 있다. 그런데 그것과는 조금 다른 용도로 필요할 때 값이 할당되는 `Lazy Stored Properties (지연 저장 프로퍼티)` 가 있다.

- `지연 저장 프로퍼티는 호출이 있어야 값을 초기화`하며, 이때 `lazy` 키워드를 사용한다.

- `상수는 인스턴스가 완전히 생성되기 전에 초기화`해야 하므로 `필요할 때 값을 할당`하는 `지연 저장 프로퍼티와는 맞지 않다.`

- `지연 저장 프로퍼티`는 `var 키워드`를 사용하여 `변수로 정의`한다.

- 지연 저장 프로퍼티는 주로 복잡한 클래스나 구조체를 구현할 때 많이 사용된다.

- - -

### 지연 저장 프로퍼티의 사용

- 클래스 인스턴스의 저장 프로퍼티로 다른 클래스 인스턴스나 구조체 인스턴스를 할당해야 할 때가 있다.

    - 이럴 때 인스턴스를 초기화하면서 저장 프로퍼티로 쓰이는 인스턴스들이 한 번에 생성되어야 한다면?
    
    - 굳이 모든 저장 프로퍼티를 사용할 필요가 없다면?
    
    - `위 질문의 답이 지연 저장 프로퍼티 사용이다.`
    
- `지연 저장 프로퍼티를 잘 사용하면 불필요한 성능저하나 공간 낭비를 줄일 수 있다.`

- - -

### 예시 코드

[Vincent Github about Lazy Stored Properties Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-10-LazyStoredPropertyExample.playground)

![LazyStoredPropertiesImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/LazyStoredPropertiesImage-1.png?raw=true)

- - -

### 다중 스레드와 지연 저장 프로퍼티

- 다중 스레드 환경에서 지연 저장 프로퍼티에 동시다발적으로 접근할 때는 한 번만 초기화된다는 보장이 없다.

- 생성되지 않은 지연 저장 프로퍼티에 많은 스레드가 비슷한 시점에 접근한다면, 여러 번 초기화될 수 있다.