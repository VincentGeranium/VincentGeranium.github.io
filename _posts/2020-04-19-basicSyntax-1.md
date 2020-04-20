---
layout: post
title:  "기본 문법 공부(옵셔널 체이닝과 빠른종료 - 빠른종료(Early Exit), guard)"
date:   2020-04-19
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Guard Syntax Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-19-guardSyntaxExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html#ID525)

- [옵셔널 체이닝과 빠른종료 - 옵셔널 체이닝](https://vincentgeranium.github.io/ios,/swift/2020/04/14/basicSyntax-1.html)

- [스위프트 기초 - 옵셔널 추출, 강제 추출, 옵셔널 바인딩, 암시적 추출 옵셔널, 옵셔널 추출 마무리](https://vincentgeranium.github.io/ios,/swift/2020/04/13/basicSyntax-1.html)

- - -

### 빠른종료 (Early Exit)

- `'빠른종료(Early Exit)'의 핵심 키워드는 'guard'이다.`

- `guard 구문은 if 구문과 유사`하게 `Bool 타입의 값으로 동작하는 기능`이다.

- if 구문과는 다르게 `guard 구문은 항상 else 구문이 뒤에 따라와야 한다.`

- `만약 guard 뒤에 따라오는 Bool 값이 false라면 else의 블록 내부 코드를 실행하게 되는데, 이때 else 구문의 블록 내부에는 꼭 자신보다 상위의 코드 블록을 종료하는 코드가 들어가게 된다.`

    - 그래서 `특정 조건에 부합하지 않는다는 판단이 되면 재빠르게 코드 블록의 실행을 종료할 수 있다.`
    
    - 이렇게 `현재의 코드 블록을 종료할 때는 return, break, continue, throw 등의 제어문 전환 명령을 사용한다. 또는 fatalError()와 같은 비반환 함수나 메서드를 호출할 수도 있다.`
    
```swift
guard Bool 타입 값 else {
    예외사항 실행문
    제어문 전환 명령어
}
```

- `guard 구문을 사용`하면 if 코드를 훨씬 `간결하고 읽기 좋게 구성할 수 있다.`

- `if 구문을 사용하면 예외사항을 else 블록으로 처리해야 하지만 예외사항만을 처리하고 싶다면 guard 구문을 사용하는 것이 훨씬 간편하다.`

<img width="1058" alt="guardSyntaxExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/guardSyntaxExampleImage-1.png?raw=true">

- 위의 코드는 `같은 기능을 수행하는 if 구문과 guard 구문의 비교`이다.
    
<img width="1058" alt="guardSyntaxExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/guardSyntaxExampleImage-2.png?raw=true">

- `Bool 타입의 값으로 guard 구문을 동작시킬 수 있지만 옵셔널 바인딩의 역활도 할 수 있다.`

- `guard 뒤에 따라오는 옵셔널 바인딩 표현에서 옵셔널의 값이 있는 상태라면 guard 구문에서 옵셔널 바인딩된 상수를 guard 구문이 실행된 아래 코드부터 함수 내부의 지역상수처럼 사용할 수 있다.`

- `위의 코드에서 guard를 통해 옵셔널 바인딩 된 상수는 greet(_:) 함수 내에서 지역상수처럼 사용된 것을 볼 수 있다.`

<img width="1058" alt="optionalChainingImage-12" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalChainingImage-12.png?raw=true">

- 위의 코드는 [옵셔널 체이닝](https://vincentgeranium.github.io/ios,/swift/2020/04/14/basicSyntax-1.html)에서 작성했던 코드이다.

- 위의 코드에서 작성했던 `Address 구조체의 fullAddress() 메서드를 guard 구문을 이용하여 조금 수정해보자.`

<img width="1058" alt="guardSyntaxExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/guardSyntaxExampleImage-3.png?raw=true">

- `위의 코드를 보면 기존에 사용했던 if let 바인딩보다는 조금 더 깔끔하고 명료하게 사용한 것을 볼 수 있다.`

<img width="1058" alt="guardSyntaxExampleImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/guardSyntaxExampleImage-4.png?raw=true">

- `조금 더 구체적인 조건을 추가하고 싶다면 쉼표(,)로 추가조건을 나열해주면 된다.`

    - `추가된 조건은 Bool 타입 값이어야 한다.`
    
    - `또, 쉼표로 추가된 조건은 AND 논리연산과 같은 결과를 준다. 즉, 쉼표를 &&로 치환해도 같은 결과를 얻을 수 있다는 뜻이다.`
    
<img width="1058" alt="guardSyntaxExampleImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/guardSyntaxExampleImage-5.png?raw=true">

- `guard 구문의 한계는 자신을 감싸는 코드 블록, 즉 return, break, continue, throw 등의 제어문 전환 명령어를 쓸 수 없는 상황이라면 사용이 불가능하다는 점이다.`

- `함수나 메서드, 반복문 등 특정 블록 내부에 위치하지 않는다면 사용이 제한된다.`