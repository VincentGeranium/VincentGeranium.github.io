---
layout: post
title:  "기본 문법 공부(while 구문, repeat-while 구문, 구문 이름표) - 200218"
date:   2020-02-18
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### while 구문

- 특정 조건 `(Bool 타입으로 지정되어야 한다)`이 성립하는 한 블록 내부의 코드를 반복해서 실행

- 제어 키워드 (break, continue등) 사용이 가능하다

![whileImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/whileImage-1.png?raw=true)

- - -

### repeat-while 구문

- repeat 블록의 코드를 최초 1회 실행한 후, while 다음의 조건이 성립하면 블록 내부의 코드를 반복 실행한다.

![repeatWhileImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/repeatWhileImage-1.png?raw=true)

- - -

### 구문 이름표

- 반복문 앞에 이름과 함께 콜론을 붙여 구문의 이름을 지정해주는 구문 이름표를 사용할 수 있다.

- 이름이 지정된 구문을 제어하고자 할 때는 제어 키워드와 구문 이름을 함께 써주면 된다.

![SyntaxNameImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/SyntaxNameImage-1.png?raw=true)