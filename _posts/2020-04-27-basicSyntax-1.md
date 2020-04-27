---
layout: post
title:  "기본 문법 공부(연산자(Basic Operator) - 연산자 우선순위(Precedence)와 결합방향(Associativity))"
date:   2020-04-27
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Operator Precedence Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-27-OperatorPrecedenceExampleCode-1.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/AdvancedOperators.html)

- - -

### 연산자 우선순위와 결합방향

- 스위프트에서는 연산자 우선순위(Precedence)를 지정해 놓았기 때문에 코딩하다가 헷갈리는 경우 확인하면 된다.

- 우선순위가 높은 연산자는 자신에 비해 우선순위가 낮은 연산자보다 먼저 실행된다.

- 프로그래머가 임의로 정의하는 사용자정의 연산자 또는 이 규칙에 따라 실행 순서가 결정된다.

- 연산자가 연산하는 결합방향(Associativity)도 지정되어 있다.

    - 예를 들어 1 + 2 + 3 + 4 라는 수식이 있다면, 연산자 +는 모두 같은 우선도를 가지며 +의 결합방향은 왼쪽이기 때문에 (((1 + 2) + 3) + 4) 처럼 왼쪽부터 그룹이 묶이는 것이다.
    
    - 그래서 1 + 2가 가장 먼저 연산이 되고 연산된 결과가 다시 3과 연산이 되고 그 결과가 다시 4와 연산이 되는 것이다.
    
    - 만약 결합방향이 오른쪽이라면 (1 + (2 + (3 + 4))) 처럼 묶여서 연산이 된다.
    
- 기본 연산자들의 우선도와 결합방향을 알아보려면 스위프트 표준 라이브러리의 연산자 정의를 참고하면 된다.

```swift
// 스위프트 표준 라이브러리에 정의된 연산자 정의의 일부

// 중략...

infix operator == : ComparisonPrecedence
infix operator ~= : ComparisonPrecedence
infix operator &= : AssignmentPrecedence
infix operator % : MultiplicationPrecedence
infix operator > : ComparisonPrecedence

// 중략...
```

- 위의 스위프트 표준 라이브러리에 정의된 연산자 정의의 일부를 보면 연산자 우선도와 결합방향을 알 수 없다.

- 연산자 뒤에 콜론을 붙이고 이어서 써준 연산자 우선순위 그룹(Precedence Group)을 지정해준 것이기 때문이다.

- 스위프트 표준 라이브러리에는 다양한 우선순위 그룹(Precedence Group)이 존재한다.

```swift
// 스위프트 표준 연산자 우선순위 그룹

precedencegroup BitwiseShiftPrecedence {
    higherThan: MultiplicationPrecedence
}

precedencegroup FunctionArrowPrecedence {
    associativity: right
    higherThan: AssignmentPrecedence
}

precedencegroup TernaryPrecedence {
    associativity: right
    higherThan: FunctionArrowPrecedence
}

precedencegroup DefaultPrecedence {
    higherThan: TernaryPrecedence
}

precedencegroup LogicalDisjunctionPrecedence {
    associativity: left
    higherThan: TernaryPrecedence
}

precedencegroup LogicalConjunctionPrecedence {
    associativity: left
    higherThan: LogicalDisjunctionPrecedence
}

precedencegroup ComparisonPrecedence {
    higherThan: LogicalConjunctionPrecedence
}

precedencegroup NilCoalescingPrecedence {
    associativity: right
    higherThan: ComparisonPrecedence
}

precedencegroup AdditionPrecedence {
    associativity: left
    higherThan: RangeFormationPrecedence
}

precedencegroup CastingPrecedence {
    higherThan: NilCoalescingPrecedence

precedencegroup AssignmentPrecedence {
    associativity: right
    assignment: true
}

precedencegroup RangeFormatPrecedence {
    higherThan: CastingPrecedence
}
```

- 위의 코드처럼 연산자 우선순위 그룹은 higherThan, lowerThan, associativity 등으로 우선순위 및 결합방향 등을 지정한 것을 볼 수 있다.

- 연산자 우선순위 그룹의 정의를 보면 알 수 있듯이 스위프트 연산자의 우선순위는 절대치가 아닌 상대적인 수치임을 알 수 있다.

- 스위프트 표준 라이브러리의 연산자 우선순위 그룹 우선순위별 정렬(우선순위 높은 순)

    - 아래에 기술된 정렬 순서는 프위프트 표준 라이브러리에 존재하는 기본 연산자 우선순위 그룹의 관계체계이다.
    
        - 1) 연산자 우선순위 그룹 이름 : DefaultPrecedence , 결합 방향 : none , 할당 방향 사용 : false
    
        - 2) 연산자 우선순위 그룹 이름 : BitwiseShiftPrecendence , 결합 방향 : none , 할당 방향 사용 : false
    
        - 3) 연산자 우선순위 그룹 이름 : Multiplication , 결합 방향 : left , 할당 방향 사용 : false
    
        - 4) 연산자 우선순위 그룹 이름 : AdditionPrecedence , 결합 방향 : left , 할당 방향 사용 : false
    
        - 5) 연산자 우선순위 그룹 이름 : RangeFormationPrecedence , 결합 방향 : none , 할당 방향 사용 : false
    
        - 6) 연산자 우선순위 그룹 이름 : CastingPrecedence , 결합 방향 : none , 할당 방향 사용 : false
    
        - 7) 연산자 우선순위 그룹 이름 : NilCoalescingPrecedence , 결합 방향 : right , 할당 방향 사용 : false
    
        - 8) 연산자 우선순위 그룹 이름 : ComparisonPrecedence , 결합 방향 : none , 할당 방향 사용 : false
    
        - 9) 연산자 우선순위 그룹 이름 : LogicalConjunctionPrecedence , 결합 방향 : left , 할당 방향 사용 : false
    
        - 10) 연산자 우선순위 그룹 이름 : LogicalDisjunctionPrecedence , 결합 방향 : left , 할당 방향 사용 : false
    
        - 11) 연산자 우선순위 그룹 이름 : TernaryPrecedence , 결합 방향 : right , 할당 방향 사용 : false
    
        - 12) 연산자 우선순위 그룹 이름 : AssignmentPrecedence , 결합 방향 : right , 할당 방향 사용 : true
    
        - 13) 연산자 우선순위 그룹 이름 : FunctionArrowPrecedence , 결합 방향 : right , 할당 방향 사용 : false
    
- 연산자 우선순위가 높을수록 같은 라인의 연산자 중 먼저 처리된다.

<img width="1058" alt="operatorPrecedenceImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/operatorPrecedenceImage-1.png?raw=true">

- 위의 코드에는 Int 타입의 피연산자를 연산하기 위해 <<, +, * 연산을 사용했다.

- Int 타입의 << 연산은 BitwiseShiftPrecedence 연산자 우선순위 그룹을 우선순위로 가지며, + 연산은 AdditionPrecedence 연산자 우선순위 그룹을 우선순위로 가진다.

    - 따라서 << 연산이 + 연산보다 더 먼저 실행되는 것을 확인할 수 있다.
    
- * 연산은 MultiplicationPrecedence 연산자 우선순위 그룹을 우선순위로 가지므로 + 연산보다 먼저 실행된다.