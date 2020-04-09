---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 자동 클로저, 클로저 파트 마무리)"
date:   2020-04-09
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드.

- [Auto Closure Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-09-AutoClosureExample-1.playground)

- - -

### 참고 자료.

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- - -

### 자동 클로저(Auto Closure).

- 함수의 전달인자(Argument)로 전달하는 표현을 자동으로 변환해주는 클로저를 '자동 클로저(Auto Closure)'라고 한다.

    - 자동 클로저는 전달인자를 갖지 않는다.
    
- 자동 클로저는 호출되었을 때 자신이 감싸고 있는 코드의 결괏값을 반환한다.

- 자동 클로저는 함수로 전달하는 클로저를 (소괄호와 중괄호를 겹쳐 써야 하는) 어려운 클로저 문법을 사용하지 않고도 클로저로 사용할 수 있도록 문법적 편의를 제공한다.

- 스위프트 표준 라이브러리에는 자동 클로저를 호출하는 함수가 구현되어 있어 이를 사용하는 일이 종종있다.

- 하지만 직접 자동 클로저를 호출하는 함수를 구현하는 일은 흔치 않을 것이다.

    - 예를 들어 스위프트 표준 라이브러리에 구현되어 있는 assert(condition:message:file:line:) 함수는 condition과 message 매개변수가 자동 클로저이다.
    
    - condition 매개변수는 디버그용 빌드에서만 실행되고, message 매개변수는 condition 매개변수가 false일 때만 실행된다.
    
-  자동 클로저는 클로저가 호출되기 전 까지 클로저 내부의 코드가 동작하지 않는다.

    - 따라서 연산을 지연시킬 수 있다.
    
    - 이 과정은 연산에 자원을 많이 소모한다거나 부작용이 우려될 때 유용하게 사용할 수 있다.
    
        - 그 이유는 코드의 실행을 제어하기 좋기 때문이다.
        
- - -

### 클로저를 이용한 연산 지연.

<img width="1058" alt="autoClosureImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/autoClosureImage-1.png?raw=true">

- 위의 코드를 통하여 클로저가 연산을 어떻게 지연시킬 수 있는지 확인 할 수 있다.

- 위의 코드에서 customerProvider 상수에 저장해둔 클로저는 하나의 명령문 묶음으로 볼 수 있다.

    - Array의 removeFirst() 메서드는 자신의 첫 번째 요소를 제거하면서 그 요소를 반환해주는 메서드이다.
    
- 그래서 customerProvider()를 선언했지만 바로 아래서 호출한 print(customerInLine.count)에서는 클로저 내부의 연산이 반영되지 않으며 클로저가 실제로 실행되기 전까지는 removeFirst() 메서드의 연산을 실행하지도 않는다.

- 그 뒤에 실제로 클로저를 실행하게 되면 그때서야 연산을 실행하게 된다.

- 클로저가 영영 호출되지 않는다면 내부의 코드도 실행되지 않기 때문에 해당 연산을 실행되지 않는다.

- - -

### 함수의 전달인자로 전달하는 클로저.

<img width="1058" alt="autoClosureImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/autoClosureImage-2.png?raw=true">

- 위의 코드는 함수의 전달인자로 직접 클로저를 작성하여 전달해주었다.

- 코드의 serveCustomer(_:) 함수는 클로저를 매개변수로 전달받고 있다.

- - -

#### NOTE. 암시적 반환 표현.

- '함수의 전달인자로 전달하는 클로저'의 코드에서 '클로저를 이용한 연산 지연' 코드와는 다르게 클로저 내부에서 return 키워드를 사용하지 않아도 되는 이유는 암시적 반환 표현 때문이다.

- 물론, '클로저를 이용한 연산 지연' 코드에서도 return 키워드를 생략해줘도 된다.

- 반대로 '함수의 전달인자로 전달하는 클로저'의 코드에서도 return 키워드를 명확하게 반환 값임을 명시해줄 수도 있다.

- - -

### 자동 클로저의 사용.

<img width="1058" alt="autoClosureImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/autoClosureImage-3.png?raw=true">

- 위의 코드는 기존의 serveCustomer(_:) 함수와 동일한 역활을 하지만 매개변수에 @autoclosure 속성을 주었기 때문에 자동 클로저 기능을 사용한다.

- 자동 클러저 속성을 부여한 매개변수는 클로저 대신에 customerInLine.removeFirst() 코드의 실행 결과인 String 타입의 문자열을 전달인자로 받게 된다.

- String 타입의 값이 자동 클로저 매개변수에 전달되면 String 값을 매개변수가 없는 String 값을 반환하는 클로저로 변환해준다.

- String 타입의 값을 전달 받는 이유는 자동 클로저의 반환 타입이 String이기 때문이다.

- 자동 클로저는 전달인자를 갖지 않기 때문에 반환 타입의 값이 자동 클로저의 매개변수로 전달되면 이를 클로저로 바꿔줄 수 있는 것이다.

- 이렇게 String 값으로 전달된 전달인자가 자동으로 클로저로 변환되기 때문에 자동 클로저라고 부른다.

- 자동 클로저를 사용하면 기존의 사용 방법처럼 클로저를 전달인자로 넘겨줄 수 없다.

- - -

### 자동 클로저의 탈출.

<img width="1058" alt="autoClosureImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/autoClosureImage-4.png?raw=true">

- 기본적으로 @autoclosure 속성은 @noescape 속성을 포함한다.

    - 즉, @autoclosure 속성을 사용하면 @noescape 속성도 부여됨을 암시하는 것이다.
    
- 만약 자동 클로저를 탈출하는 클로저로 사용하고 싶다면 @autoclosure 속성 뒤에 @escaping 속성을 덧붙여서 위의 코드처럼 사용하면 된다.

- 위의 코드를 살펴보면 탈출 가능한 자동 클로저를 매개변수로 받아서 반환 값으로 반환하는 returnProvider(_:) 함수가 있다.

    - 이 함수의 전달인자로 전달한 후 클로저로 변환된 코드들이 그대로 클로저의 형태로 반환되는 것을 알 수 있다.
    
    - 즉, 함수를 탈출하는 클로저가 되는 것이다. 그래서 위의 코드와 같이 @autoclosure @escaping 속성을 사용해야 한다.
    
- - -

### 클로저 파트의 마무리.

- 클로저는 스위프트의 막강한 기능에 매번 함께하는 파트너가 될 것이다.

- 클로저는 생략할 수 있는 부분이 많다. 그렇기 때문에 경우의 수만 따져보더라도 정말 다양한 표현의 클로저가 만들어질 수 있다.

- 타입 유추만 사용할 수도 있고, 암시적 반환 표현만 사용할 수 있으며, 단축 인자 이름만 사용할 수도 있고, 이를 모두 사용할 수도, 사용하지 않을 수도 있다.

- 그렇기 때문에 다양한 클로저 표현 방법을 알아두고, 잘 활용할 줄 아는 지혜가 필요하다. 물론 다른 사람의 코드를 이해하려면 이를 모두 알고 있어야 함은 물론이다.

- 클로저의 축약 표현들이 득이 될 수도, 독이 될 수도 있을 것이다.