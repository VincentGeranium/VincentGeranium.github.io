---
layout: post
title:  "기본 문법 공부(접근제어 - private와 fileprivate, 읽기 전용 구현)"
date:   2020-03-31
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Private And Fileprivate Example - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-31-privateAndFileprivateExample.playground)

- [Private And Fileprivate Example - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-31-privateAndFileprivateExample-2.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)

- - -

### private와 fileprivate

- 같은 파일 내부에서 private 접근수준과 fileprivate 접근수준은 사용할 때 분명한 차이가 있다.

    - fileprivate 접근수준으로 지정한 요소는 같은 파일 어떤 코드에서도 접근할 수 있다.
    
    - private 접근수준으로 지정한 요소는 같은 파일 내부에 다른 타입의 코드가 있더라도 접근이 불가능하다.
    
        - 그러나 자신을 확장하는 익스텐션 코드가 같은 파일에 존재하는 경우 접근할 수 있다.
        
- - -

### 같은 파일에서의 private와 fileprivate의 동작

![privateAndFileprivateExampleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/privateAndFileprivateExampleImage-1.png?raw=true)

- - -

### 읽기 전용 구현

- 구조체 또는 클래스를 사용하여 저장 프로퍼티를 구현할 때는 허용된 접근수준에서 프로퍼티 값을 가져갈 수 있다.

- 값을 변경할 수 없도록 구현하고 싶다면 또는, 서브스크립트도 읽기만 가능하도록 제한할 수 있다.

    - 위와 같이 하고 싶을 때는 설정자(Setter)만 더 낮은 접근수준을 갖도록 제한하면 된다.
    
        - 요소의 접근수준 키워드 뒤에 '접근수준'(set) 처럼 표현하면 설정자의 접근수준만 더 낮도록 지정해줄 수 있다.
        
- 설정자(Setter) 접근수준 제한은 프로퍼티, 서브스크립트, 변수 등에 적용될 수 있으며, 해당 요소의 접근수준과 같거나 혹은 보다 낮은 수준으로 제한해주어야 한다.

- - -

### 설정자(Setter)의 접근수준(Access Level) 지정

<img width="1718" alt="privateAndFileprivateExampleImag-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/privateAndFileprivateExampleImage-2.png?raw=true">
<img width="1718" alt="privateAndFileprivateExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/privateAndFileprivateExampleImage-3.png?raw=true">