---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 : (맵, 필터, 리듀스(Map, Filter, Reduce) - 필터(Filter))"
date:   2020-06-06
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Filter Method Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-06-06-FilterMethodExampleCode-1.playground)

- - -
- - -

### 필터(Filter)

- 필터(Filter)는 말 그대로 컨테이너 내부의 값을 걸러서 추출하는 역활을 하는 고차함수이다.

- 맵(Map)과 마찬가지로 새로운 컨테이너에 값을 담아 반환해준다.

     - 다만 맵처럼 기존 콘텐츠를 변형하는 것이 아니라, 특정 조건에 맞게 걸러내는 역활을 할 수 있다는 점이 다르다.
     
- filter 함수의 매개변수로 전달되는 함수의 반환 타입은 Bool이다.

    - 해당 콘텐츠의 값을 갖고 새로운 컨테이너에 포함될 항목이라고 판단되면 true를, 포함되지 않을 항목이라고 판단되면 false를 반환해주면 된다.
    
<img width="1058" alt="filterImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/filterImage-1.png?raw=true" title="filterImage-1">

- 위의 코드는 간단한 필터 메서드를 사용한 코드이다.

<img width="1058" alt="filterImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/filterImage-2.png?raw=true" title="filterImage-2">

- 만약 컨텐츠의 변형 후에 필터링하고 싶다면 위의 코드처럼 맵을 사용한 후에 필터 메서드를 호출하면 된다.

- 위의 코드처럼 맵과 필터를 연결하여 사용하면 복잡한 연산도 손쉽게 실행할 수 있다.

- - -
- - -