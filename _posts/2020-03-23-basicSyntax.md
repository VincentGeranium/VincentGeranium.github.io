---
layout: post
title:  "기본 문법 공부(프로퍼티와 메서드 - 타입 메서드)"
date:   2020-03-23
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Type Method Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-23-TypeMethodExample.playground)

- [Type Method Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-23-TypeMethodExample-2.playground)

- - -

### 타입 메서드 (Type Method)

- 인스턴스 프로퍼티와 타입 프로퍼티가 있듯이 `메서드에도 인스턴스 메서드와 타입 메서드가 있다.`

- `타입 자체에 호출이 가능한 메서드를 타입 메서드(흔히 객체지향 프로그래밍에서 지칭하는 클래스 메서드와 유사)라고 부른다.`

- `메서드 앞에 static 키워드를 사용`하여 타입 메서드임을 나타내준다.

- - -

### 클래스의 타입 메서드
    
![TypeMethodImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeMethodImage-1.png?raw=true)

- `클래스의 타입 메서드`는 `static 키워드와 class 키워드를 사용할 수 있다.`

    - `static으로 정의`하면 `상속 후 메서드 재정의(override)가 불가능.`
    
    - `class로 정의`하면 `상속 후 메서드 재정의(override)가 가능.
    
- - -

### 타입 프로퍼티와 타입 메소드의 사용

![TypeMethodImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeMethodImage-2.png?raw=true)

- `타입 메서드는` 인스턴스 메서드와는 달리 `self 프로퍼티가 타입 그 자체를 가리킨다는 점이 다르다.`

- `인스턴스 메서드에서는 self가 인스턴스`를 가리킨다면 `타입 메서드의 self는 타입을 가리킨다.`

- `타입 메서드 내부에서 타입 이름과 self는 같은 뜻`이라고 볼 수 있다.

- `타입 메서드에서 self 프로퍼티를 사용하면 타입 프로퍼티 및 타입 메서드를 호출할 수 있다.`