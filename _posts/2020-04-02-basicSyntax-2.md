---
layout: post
title:  "기본 문법 공부(함수형 프로그래밍과 스위프트 - 기본 클로저)"
date:   2020-04-02
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Closure Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-02-ClosureExample.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)

- [Nested Function Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/01/basicSyntax-1.html)

- [Closure Summary](https://vincentgeranium.github.io/ios,/swift/2020/04/02/basicSyntax-1.html)

- - -

### 기본 클로저

- 스위프트 표준 라이브러리에는 배열의 값을 정렬하기 위해 구현한 'sorted(by:)' 메서드가 있다.

    - sorted(by:) 메서드는 클로저를 통해 어떻게 정렬할 것인가에 대한 정보를 받아 처리하고 결괏값을 배열로 돌려준다.

    - 단순히 정렬만 하기 때문에 입력받은 배열의 타입과 크기가 동일하다.
    
    - 기존의 배열은 변경하지 않고 정렬된 배열을 새로 생성하여 반환해준다.
    
```swift
// 스위프트 라이브러리의 sorted(by:)메서드 정의
public func sorted(by areInIncreasingOrder: (Element, Element) -> Bool) -> [Element]
```

- - -

### Sorted(by:) 메서드를 이용하여 설명하는 클로저(Closure) - 1

<img width="500" alt="ClosureExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ClosureExampleImage-1.png?raw=true">

- 위의 이름 배열을 이용, String 타입의 배열에 이름을 넣어 영문 알파벳을 내림차순으로 정렬할 것이다.

- sorted(by:) 메서드는 (배열의 타입과 같은 두 개의 매개변수를 가지며 Bool 타입을 반환하는) 클로저를 전달인자로 받을 수 있다.

    - 반환하는 Bool 값은 첫 번째 전달인자 값이 새로 생성되는 배열에서 두 번째 전달인자 값보다 먼저 배치되어야 하는지에 대한 결괏값이다.
    
        - true를 반환하면 첫 번째 전달인자가 두 번째 전달인자보다 앞에 온다.
        
<img width="1058" alt="ClosureExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ClosureExampleImage-2.png?raw=true">

- 위의 그림에 나오는 함수는 매개변수로 String 타입 두 개를 가지며, Bool 타입을 반환하는 함수이다.

- 위의 그림에서 보면 구현된 함수를 'sorted(by:)'메서드의 전달인자로 전달하여 'reversed'라는 이름의 배열로 반환받는다.

- 전달받는 두 전달인자는 정렬에 참고할 값이고, 반환될 값은 첫 번째 전달인자가 앞으로 배치될지 뒤로 배치될지에 대한 Bool 타입 값이다.

- 함수는 클로저의 한 형태이다.

- 만약 first 문자열이 second 문자열보다 크다면 backwards(first:second:) 함수의 반환값은 true가 될 것이다.

    - 즉, 값이 더 큰 first 문자열이 second 문자열보다 앞쪽에 정렬되어야 한다는 뜻이다.

    - '문자열이 크다' 라는 뜻은 '알파벳이 더 뒤쪽이다'라는 뜻이다. 
    
        - 예를 들어 'B'는 'A'보다 큽니다. 혹은 'vincent'는 'ron'보다 큽니다.

- - -

### Sorted(by:) 메서드를 이용하여 설명하는 클로저(Closure) - 2

- 위의 함수에서 보면 first > second 라는 반환 값을 받기 위해 너무 많은 표현을 사용했다.

    - 함수 이름부터 매개변수 표현까지 부가적인 표현도 많다.

- 이를 클로저 표현을 사용해서 조금 더 간결하게 표현 할 수 있다.

- 클로저 표현은 통상 아래 형식을 따른다.

```swift
{ ('매개변수들') -> '반환타입' in
    '실행 코드'
}
```

- 클로저도 함수와 마찬가지로 입출력 매개변수(Parameter)를 사용할 수 있다.

- 매개변수 이름을 지정한다면 가변 매개변수 또한 사용이 가능하다.

- 다만 클로저는 매개변수 기본값을 사용할 수 없다.

- - -

### Sorted(by:) 메서드를 이용하여 설명하는 클로저(Closure) - 3

<img width="758" alt="ClosureExampleImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/ClosureExampleImage-3.png?raw=true">

- 위의 그림은 backwards(first:second:) 함수를 클로저 표현으로 대체한것이다.

- sorted(by:) 메서드로 전달하는 클로저의 매개변수 개수와 타입, 그리고 반환 타입 모두 backwards(first:second:) 함수와 같다.

    - 위의 그림을 보면 처음보다 코드가 훨씬 간결해지고 직관적으로 바뀌었다.

- 위와 같이 프로그래밍하면 sorted(by:) 메서드로 전달되는 backwards(first:second:) 함수가 어디에 있는지, 어떻게 구현되어 있는지 찾아다니지 않아도 된다.

- 물론, 반복해서 같은 기능을 사용하려면 함수로 구현해두는 것도 나쁘지 않다.