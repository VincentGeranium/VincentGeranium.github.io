---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 옵셔널, 옵셔널의 사용)"
date:   2020-04-10
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Optional Example Code](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-10-optionalExample-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

- - -

### 옵셔널(Optionals)

- 옵셔널(Optionals)은 스위프트의 특징 중 하나인 안전성(Safe)을 문법으로 담보하는 기능이다.

- 옵셔널은 '선택적인', 즉 값이 '있을 수도, 없을 수도 있음'을 나타내는 표현이다.

    - 이는 '변수나 상수 등에 꼭 값이 있다는 것을 보장할 수 없다. 즉, 변수 또는 상수의 값이 nil일 수도 있다'는 것을 의미한다.
    
    - 라이브러리의 API 문서를 작성 혹은 읽어보면 문서에 It can be NULL 또는 It can NOT be NULL 등의 부연설명이 있다.
    
    - 그리고 전달인자(Argument)로 NULL이 전달되어도 되는지 문서를 보기 전에는 알 수가 없다.
    
    - 그러나 스위프트에서는 옵셔널 하나만으로도 이 의미를 충분히 전달할 수 있다.
    
    - 옵셔널과 옵셔널이 아닌 값을 철저히 다른 타입으로 인식하기 때문에 컴파일할 때 바로 오류를 걸러낼 수 있다.
    
- - -

### 옵셔널 사용

- n옵셔널 변수 또는 상수가 아니면 nil을 할당할 수 없다.

    - 예를 들어 Int 타입에 0을 할당했다면 값이 없다는 의미가 아니다. 0도 하나의 값이다.
    
    - 또한 " " 로 '빈 문자열'을 만들었다면 이것도 '빈 문자열'이라는 값이지, 값이 없는 것은 아니다.
    
- 변수 또는 상수에 '정말 값이 없을 때만 nil'로 표현한다.

    - 함수형 프로그래밍 패러다임에 자주 등장하는 모나드(Monad) 개념과 일맥상통한다.
    
- 그래서 옵셔널의 사용은 많은 의미를 축약하여 표현하는 것과 같다.

- 옵셔널을 읽을 때 '해당 변수 또는 상수에는 값이 없을 수 있다. 즉, 변수 또는 상수가 nil일 수도 있으므로 사용에 주의하라'는 뜻으로 직관적으로 받아들일 수 있다.

- 값이 없는 옵셔널 변수 또는 상수에 (강제로) 접근하려면 런타임 오류가 발생한다. 그렇게 되면 OS가 프로그램이 강제 종료시킬 확률이 매우 높다.

```swift
// 오류가 발생하는 nil 할당
var myName: String = "Jun"
myName = nil // Error !!
```

- nil은 옵셔널로 선언된 곳에서만 사용될 수 있다.

- 옵셔널 변수 또는 상수 등은 데이터 타입 뒤에 물음표(?)를 붙여 표현해준다.

```swift
// 옵셔널 변수의 선언 및 nil 할당
var myName: String? = "Jun"
print(myName) // Jun

myName = nil
print(myName) // nil
```

- 위의 코드에서 var myName: Optional<String> 처럼 옵셔널을 조금 더 명확하게 써줄 수도 있다.

- 그러나 물음표를 붙여주는 것이 조금 더 편하고 읽기도 쉽기 때문에 굳이 긴 표현을 사용하지는 않는다.

- - -

### 옵셔널의 사용 상황과 사용 이유, 굳이 변수에 nil이 있음을 가정해야 하는 이유

- 위 타이틀에 답할 수 있는 예로 스스로 만든 함수에 전달되는 전달인자의 값이 잘못된 값일 경우 제대로 처리하지 못했음을 nil을 반환하여 표현하는 것을 들 수 있다.

- 기능상 심각한 오류라면 별도로 처리해야겠지만, 간단히 nil을 반환해서 오류가 있음을 알릴 수도 있다.

- 또는, 매개변수를 굳이 넘기지 않아도 된다는 뜻으로 매개변수의 타입을 옵셔널로 정의할 수도 있다.

- 스위프트 프로그래밍을 하면서 매개변수가 옵셔널일 때는 '매개변수에는 값이 없어도 되는구나'라는 것을 API 문서를 보지 않고도 알아야 한다.

- - -

### 원시 값을 통한 열거형 초기화

```swift
let primary = School(rawValue: "유치원") // Primary
let graduate = School(rawValue: "석박사") // nil

let one = Numbers(rawValue: 1) // One
let three = Numbers(rawValue: 3) // nil
```

- 위의 코드에서는 상수 뒤에 데이터 타입을 명시해주지 않고 타입 추론 기능을 사용했다.

    - 그 이유는 nil을 할당하는 경우가 생기기 때문이다.
    
    - 컴파일러는 아마도 primary 및 graduate 상수의 데이터 타입을 School?이라고 추론했을 것이다.
    
    - 또, one와 three 상수의 데이터 타입은 Numbers?라고 추론했을 것이다.
    
    - 이때 원시 값이 열거형의 case에 해당하지 않으면 열거형 인스턴스 생성에 실패하여 nil을 반환하는 경우가 생긴다.
    
    - '옵셔널의 사용 상황과 사용 이유, 굳이 변수에 nil이 있음을 가정해야 하는 이유' 파트에서 설명한 함수의 처리 실패 유형에 해당하는 것이다.
    
- - -

### 옵셔널 열거형의 정의

```swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
    case none
    case some(Wrapped)
    public init(_ some: Wrapped)
    /// 중략...
}
```

- 위의 옵셔널 정의 코드를 보면 알 수 있듯이 옵셔널은 열거형으로 구현되어 있다.

- 위의 코드에서 옵셔널은 제네릭이 적용된 열거형이다.

- ExpressibleByNilLiteral 프로토콜을 따른다는 것도 확인할 수 있다.

- 위의 코드에서 보고 알아야 할 것은 옵셔널이 값을 갖는 케이스와 그렇지 못한 케이스 두 가지로 정의되어 있다는 것이다.

    - 즉, nil 일 때는 none 케이스가 될 것이고, 값이 있는 경우는 some 케이스가 되는데, 연관 값으로는 Wrapped가 있다.
    
    - 따라서 옵셔널에 값이 있으면 some의 연관 값인 Wrapped에 값이 할당된다.
    
        - 즉, 값이 옵셔널이라는 열거형의 방패막에 보호되어 래핑되어 있는 모습이라는 것이다.
        
- - -

### Switch를 통한 옵셔널 값의 확인

<img width="1058" alt="optionalExampleImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalExampleImage-1.png?raw=true">
        
- 위의 코드를 보면 알 수 있듯이 옵셔널 자체가 열거형이기 때문에 옵셔널 변수는 switch 구문을 통해 값이 있고 없음을 확인 할 수 있다.

<img width="1058" alt="optionalExampleImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalExampleImage-2.png?raw=true">

- 위의 코드처럼 여러 케이스의 조건을 통해 검사하고자 한다면 더욱 유용하게 쓰일 수도 있다.

    - 그럴 땐 where 절과 병합해서 쓰면 더욱 좋다.
    
- - -    