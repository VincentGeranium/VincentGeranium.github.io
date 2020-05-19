---
layout: post
title:  "기본 문법 공부(타입 캐스팅(Type Casting) - Any, AnyObject의 타입 캐스팅(Type Casting for Any and AnyObject))"
date:   2020-05-19s
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -
- - -

### 예제 코드

- [Type Casting Example Code - 7](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-05-19-TypeCastingExampleCode-7.playground)

- - -
- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)

- - -
- - -

### Any, AnyObject의 타입 캐스팅(Type Casting for Any and AnyObject)

- 스위프트에는 특정 타입을 지정하지 않고 여러 타입의 값을 할당할 수 있는 Any와 AnyObject라는 특별한 타입이 있다.

    - Any는 함수 타입을 포함한 모든 타입을 뜻하거, AnyObject는 클래스 타입만을 뜻한다.
    
        - Any와 AnyObjcet를 사용하면 예기치 못한 오류가 발생할 확률이 높아지므로 되도록이면 사용을 지양하는 것이 좋다.
        
- 스위프트 표준 라이브러리에서는 Any나 AnyObject를 찾아보기 어렵지만 다른 프로그래머나 기업에서 만들어 제공하는 프레임워크의 API를 보면 Any또는 AnyObject의 사용을 심심치 않게 볼 수 있다.

    - API를 통해 어떤 타입의 데이터라도 전달할 수 있다는 의미로 해석해볼 수 있다.
    
    - 그런데 문제는 반환되는 타입도 Any나 AnyObject라면 전달받은 데이터가 어떤 타입인지 확인하고 사용해야 한다.
    
    - 왜냐하면 스위프트는 암시적 타입 변환을 허용하지 않으며, 타입에 굉장히 엄격하기 때문이다.
    
<img width="1058" alt="TypeCastingExampleImg-12" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-12.png?raw=true" title="TypeCastingExampleImg-12">

- 위 코드에는 AnyObject를 타입으로 명시한 item 매개변수(Parameter)가 있는 checkType(of:) 함수에 Coffee, Latte, Americano 타입의 인스턴스를 전달인자(Argument)로 호출했다.

    - 그 결과 checkType(of:) 함수 안에서 is 연산자를 사용하여 해당 인스턴스가 어떤 타입의 인스턴스인지만 확인해볼 수 있다.
    
<img width="1058" alt="TypeCastingExampleImg-13" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-13.png?raw=true" title="TypeCastingExampleImg-13">

- 위 코드의 방법을 사용하면 item이 어떤 타입인지 판단하는 동시에 실질적으로 해당 타입의 인스턴스로 사용할 수 있도록 캐스팅할 수 있다.

<img width="1058" alt="TypeCastingExampleImg-14" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/TypeCastingExampleImg-14.png?raw=true" title="TypeCastingExampleImg-14">

- 위의 두 코드인 "AnyObject의 타입 확인" 코드와 "AnyObject의 타입캐스팅" 코드에서 AnyObject는 클래스 인스턴스만 취할 수 있었던 반면에, Any는 모든 타입의 인스턴스를 취할 수 있다.

    - Any는 함수, 구조체, 클래스, 열거형 등 모든 타입의 인스턴스를 의미할 수 있다.

- 위 코드 "Any의 타입캐스팅"에서 Any를 타입으로 명시한 item 매개변수가 있는 checkAnyType(of:) 함수에 다양한 타입의 인스턴스를 전달인자(Argument)로 호출했다.

    - 그 결과 checkAnyType(of:) 함수 안에서 switch 조건 구문과 as 연산자, let 값 바인딩 등을 사용하여 item의 타입을 확인하고 타입에 맞는 동작을 할 수 있다.
    
    - 전달되는 전달인자에는 Int, Double, String, Tuple, ClassType, Function 등 다양한 타입이 전달될 수 있었으며 적절히 처리된 것을 볼 수 있다.
    
    - switch의 case에 해당하지 않은 타입은 default에서 타입 이름을 콘솔로 출력해볼 수도 있다.

- - -
- - -