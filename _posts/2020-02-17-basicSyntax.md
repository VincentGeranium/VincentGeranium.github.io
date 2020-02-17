---
layout: post
title:  "기본 문법 공부(Tuple) - 200217"
date:   2020-02-17
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 튜플 한 줄 정리

- `타입의 이름이 따로 지정되어 있지 않은, 프로그래머 마음대로 만드는 타입, 지정된 데이터의 묶음.`

- - -

### 튜플

- 타입의 이름이 따로 지정되어 있지 않은, 프로그래머 마음대로 만드는 타입.

- `지정된 데이터의 묶음.`

- 튜플은 타입 이름이 따로 없으므로 일정 타입의 나열만으로 튜플 타입을 생성해 줄 수 있다.

- 튜플에 포함될 데이터의 개수는 자유롭게 정할 수 있다.

![TupleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TupleImage-1.png?raw=true)

- - -

### 튜플의 요소 이름 지정

- 튜플의 각 요소를 이름 대신 숫자로 표현하기 때문에 차후에 다른 프로그래머가 코드를 볼 때 각 요소가 어떤 의미가 있는지 유추하기가 어렵다.

- 이름 없이 인덱스로만 각 요소의 데이터가 무엇을 나타내는지 쉽게 파악하기 어렵기 때문이다.

![TupleImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TupleImage-2.png?raw=true)

- - -

### 튜플 별칭 지정

- 튜플에는 타입 이름에 해당하는 키워드가 따로 없다 보니 사용에 불편함이 있다.

- 매번 같은 모양의 튜플을 사용시, 선언해줄 때마다 긴 튜플 타입을 모두 써줘야 하는 불편함이 있다.

- `타입 별칭을 사용하여 조금 더 깔끔하고 안전하게 코드를 작성할 수 있다.`

![TupleImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TupleImage-3.png?raw=true)