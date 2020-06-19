---
layout: post
title:  "알고리즘 풀이 : 백준 온라인 저지 알고리즘 문제(1008번, A / B)"
date:   2020-06-19
categories: iOS, Swift
---

이 포스트는 알고리즘 문제를 풀고 공부하고 정리한 내용 입니다.

- - -
- - -

### 예제 코드

- [백준 온라인 저지 알고리즘 문제(1008번, A / B) 코드](https://github.com/VincentGeranium/Algorithm-Study/blob/master/Algorithm-Practice/2020-06-16-Algorithm-Practice-1/2020-06-16-Algorithm-Practice-1/main.swift)

- - -
- - -

### 참고 자료

- [ZeddiOS - 나누기가 안될 때](https://zeddios.tistory.com/171)

- - -
- - -

### 백준 온라인 저지 알고리즘 문제(1008번, A / B)

<img width="820" alt="no.1008ScreenShot-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/no.1008ScreenShot-1.png?raw=true">

<img width="820" alt="no.1008ScreenShot-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/no.1008ScreenShot-2.png?raw=true">

- 처음 이 문제를 풀 때 두 피연산자를 Int 형으로 만들어서 나누었더니 계속 0이 나왔다. 무엇이 문제일까 생각하다가 두 피연산자를 Int 타입에서 Double 타입으로 바꾸어 주니 제대로 된 답이 나왔다.

    - 그 이유는 바로 "/" 연산자에 있다.
    
- 나누기 연산자("/")는 두 피연산자의 타입에 따라 반환해 주는 타입이 다르다. 즉, 피연산자의 타입이 Int 타입이냐 Double 타입이냐에 따라 답(반환값)이 달리 나온다.

<img width="1280" alt="divideImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/divideImage-1.png?raw=true">

- 위 그림을 보면 "/" 가 받아오는 두 피연산자가 Int 타입일 경우 반환 타입을 Int로 반환 해준다.

    - 예를 들어 두 피연산자를 각각 Int 타입의 1 과 3으로 주고 "/"를 사용하면 아래의 그림과 같이 나온다.
    
<img width="820" alt="no.1008ScreenShot-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/no.1008ScreenShot-3.png?raw=true">    

<img width="1280" alt="divideImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/divideImage-2.png?raw=true">

- 위 그림을 보면 "/" 가 받아오는 두 피연산자가 Double 타입일 경우 반환 타입을 Double 반환해 준다.

    - 예를 들어 두 피연산자를 각각 Double 타입의 1.0 과 3.0으로 주고 "/"를 사용하면 아래의 그림과 같이 나온다.
    
<img width="820" alt="no.1008ScreenShot-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/no.1008ScreenShot-1.png?raw=true">

- 두 피연산자 중 하나만이라도 Double 타입일 경우에도 반환 타입을 Double 타입으로 반환해 준다.

    - 예를 들어 두 피연산자를 Int 타입의 1 과 Double 타입의 3.0으로 주고 "/"를 사용하면 두 피연산자를 Double 타입을 준 것과 동일한 반환값인 0.333333333이 나온다.

- Think Note : 연산자도 func 이라는 것을 알아두자.

- - -
- - -