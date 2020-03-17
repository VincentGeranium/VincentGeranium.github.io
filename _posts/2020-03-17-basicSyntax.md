---
layout: post
title:  "기본 문법 공부(데이터 타입 고급 - 열거형(Enumeration))"
date:   2020-03-17
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [EnumerationExampleCode-1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample.playground)

- [EnumerationExampleCode-2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample-2.playground)

- [EnumerationExampleCode-3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample-3.playground)

- [EnumerationExampleCode-4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample-4.playground)

- [EnumerationExampleCode-5](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample-5.playground)

- [EnumerationExampleCode-6](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-03-17-EnumerationExample-6.playground)

- - -

### 열거형

- 열거형은 `연관된 항목들을 묶어서 표현할 수 있는 타입.`

- 열거형은 배열이나 딕셔너리 같은 타입과 다르게 `프로그래머가 정의해준 항목 값 외에는 추가/수정 불가.`

    - 그러므로 `딱 정해진 값만 열거형 값에 속할 수 있다.`
        
- - -

### 열거형 사용 경우 예시

- 제한된 선택지를 주고 싶을 때

- 정해진 값 외에는 입력받고 싶지 않을 때

- 예상된 입력 값이 한전되어 있을 때

- - -

### 생활 주변 속 열거형 예시

- 열거형으로 묶을 수 있는 항목들은 주변 생활에서 많이 찾아볼 수 있다.

    - `무선통신 방식` : WiFi, 블루투스, LTE, 3G, 기타
    
    - `학생` : 초등학생, 중학생, 고등학생, 대학생, 대학원생, 기타
    
    - `지역` : 강원도, 경기도, 경상도, 전라도, 제주도, 충청도
    
- - -

### Swift에서의 열거형과 다른 프로그래밍 언어에서의 열거형

- `스위프트에서 열거형은 연관된 항목들의 그룹을 정의할 수 있다.`

- `스위프트의 열거형은 항목별로 값을 가질 수도, 가지지 않을 수도 있다.`

- 다른 프로그래밍 언어 예를 들어 C언어는 열거형의 각 항목 값이 정수 타입으로 기본 지정되지만, `스위프트의 열거형은 각 항목이 그 자체로 고유의 값이 될 수 있다.`

- 기존의 C언어 등에서 열거형은 주로 정수 타입 값의 별칭 형태로 사용이 될 뿐이었다.

    - 그러므로 모든 열거형의 데이터 타입은 같은 타입(주로 정수 타입)으로 취급한다.
    
    - 이는 열거형 각각이 고유의 타입으로 인식될 수 없다는 문제 때문에 여러 열거형을 사용할 때 프로그래머의 실수로 인한 버그가 생길 수도 있었다.
    
- `스위프트의 열거형은 각 열거형이 고유의 타입으로 인정`되기 때문에 실수로 버그가 일어날 가능성을 원청 봉쇄할 수 있다.

- `스위프트의 열거형은 각 항목이 원시 값(Raw Value)이라는 형태로 (정수, 실수, 문자 타입 등의) 실제 값을 가질 수도 있다.`

    - 또는 `연관 값(Associated Values)을 사용하여 다른 언어에서 공용체라고 불리는 값의 묶음도 구현할 수 있다.`
    
- - -

### 기본 열거형

- 스위프트의 열거형은 `enum`이라는 키워드로 선언할 수 있다.

![EnumerationExampleImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-1.png?raw=true)

- School이라는 이름을 갖는 열거형에는 primary, elementary, middle, high, college, university, graduate라는 항목이 있다.

- 각 항목은 그 자체가 고유의 값이다.

![EnumerationExampleImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-2.png?raw=true)

- 항목이 여러 가지라서 나열하기 귀찮거나 어렵다면 한 줄에 모두 표현해줄 수도 있다.

![EnumerationExampleImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-3.png?raw=true)

- 열거형 변수를 생성하고 값을 할당 할 수도 있다.

- - -

### 원시 값 (Raw Value)

![EnumerationExampleImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-4.png?raw=true)

- 열거형의 `각 항목은 자체로도 하나의 값`이지만 `항목의 원시 값(Raw Value)도 가질 수 있다.`

    - `즉, 특정 타입으로 지정된 값을 가질 수 있다는 뜻이다.`
    
- `특정 타입의 값을 원시 값으로 가지고 싶다면 열거형 이름 오른쪽에 타입을 명시해주면 된다.`

- `원시 값을 사용`하고 싶다면 `rawValue`라는 프로퍼티를 통해 가져올 수 있다.

![EnumerationExampleImage-5](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-5.png?raw=true)

- `일부 항목만 원시 값을 주고 싶다면 그렇게 해도 된다. 나머지는 스위프트가 알아서 처리해준다.`

- `문자열 형식의 원시 값을 지정`해줬다면 `각 항목 이름을 그대로 원시 값`으로 갖게 되고, `정수 타입`이라면 `첫 항목을 기준으로 0부터 1씩 늘어난 값을 갖게 된다.`

![EnumerationExampleImage-6](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-6.png?raw=true)

- `열거형이 원시 값을 갖는 열거형`일 때, 열거형의 원시 값 정보를 안다면 `원시 값을 통해 열거형 변수 또는 상수를 생성해줄 수도 있다.`

- `올바르지 않은 원시 값을 통해 생성하려고 한다면 nil을 반환한다. 이는 실패 가능한 이니셜라이저 기능이다.`

- - -

### 연관 값 (Associated Values)

![EnumerationExampleImage-7](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-7.png?raw=true)

- `스위프트의 열거형 각 항목이 연관 값을 가지게 되면, 기존 프로그래밍 언어의 공용체 형태를 띌 수도 있다.`

- `열거형 내의 항목(case)이 자신과 연관된 값을 가질 수 있다.`

- `연관 값`은 `각 항목 옆에 소괄호로 묶어 표현`할 수 있다.

- 다른 항목이 연관 값을 갖는다고 `모든 항목이 연관 값을 가질 필요는 없다.`

![EnumerationExampleImage-8](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-8.png?raw=true)

- 식당의 재료가 한정적이라 파스타의 맛과 피자의 도우, 토핑 등을 특정 메뉴로 한정 지르려면 위의 그림에 나오는 것 처럼 열거형으로 바꾸면 된다.

- - -

### 순환 열거형

![EnumerationExampleImage-9](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-9.png?raw=true)

- `순환 열거형은 형거형 항목(case)의 연관 값(Associated Values)이 열거형 자신의 값이고자 할 때 사용한다.`

- `순환 열거형을 명시`하고 싶다면 `indirect` 키워드를 사용하면 된다.

- `특정 항목에만 한정`하고 싶다면 `case 키워드 앞에 indirect를 붙이면 된다.`

- `열거형 전체에 적용`하고 싶다면 `enum 키워드 앞에 indirect 키워드를 붙이면 된다.`

![EnumerationExampleImage-10](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-10.png?raw=true)

- 위 그림은 `열거형 전체에 순환 열거형을 적용`, `enum 키워드 앞에 indirect 키워드를 붙였다.`

- 위 그림의 `열거형`에는 `정수를 연관 값으로 갖는 number`라는 항목이 있고 `덧셈을 위한 addition이라는 항목`, `곱셈을 위한 multiplication 항목이 있다.`

![EnumerationExampleImage-11](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/EnumerationExampleImage-11.png?raw=true)

- 위 그림은 ArithmeticExpression 열거형을 사용하여 (5 + 4) x 2 연산을 구현해보는 코드이다.

- evaluate는 ArithemticExpression 열거형의 계산을 도와주는 순환 함수(Recursive Function)이다.

- `indirect 키워드는 위의 그림과 같은 예제뿐만 아니라, 이진 탐색 트리 등의 순환 알고리즘을 구현할 때 유용하게 사용할 수 있다.`