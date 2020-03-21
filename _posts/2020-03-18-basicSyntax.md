---
layout: post
title:  "기본 문법 공부(프로퍼티와 메서드 - 전역변수와 지역변수)"
date:   2020-03-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Global Variable and Local Variable Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-18-GlobalVariableAndLocalVariableExample.playground)

- - -

### 전역변수와 지역변수

- `연산 프로퍼티(Computed Property)`와 `프로퍼티 감시자(Property Observers)`는 `전역변수와 지역변수 모두에 사용할 수 있다.`

    - 따라서 `프로퍼티에 한정하지 않고`, `전역에서 쓰일 수 있는 변수와 상수`에도 `두 기능을 사용할 수 있다.`

- 함수나 메서드, 클로저, 클래스, 구조체, 열거형 등의 범위 안에 `포함되지 않았던 변수나 상수`는 `모두 전역변수 또는 전역상수`에 해당된다.

- `전역변수 또는 지역변수`는 `저장변수`라고 할 수 있다.

- `저장변수`는 마치 `저장 프로퍼티처럼 값을 저장하는 역활`을 한다.

- `전역변수나 지역변수`를 `연산변수로 구현`할 수도 있으며, `프로퍼티 감시자를 구현`할 수도 있다.

- `전역변수나 전역상수`는 `지연 저장 프로퍼티(Lazy Stored Property)`처럼 `처음 접근할 때 최초로 연산이 이루어진다.`

    - `lazy 키워드를 사용하여 연산을 늦출 필요가 없다.`
    
- `지역변수 및 지연상수`는 절대로 `지연 연산 되지 않는다.`

- - -

### 저장변수의 감시자와 연산변수

![GlobalVariableAndLocalVariableImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/GlobalVariableAndLocalVariableImage-1.png?raw=true)