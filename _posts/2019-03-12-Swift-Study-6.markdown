---
layout: post
title:  "Swift - Fast campus iOS School"
date:   2019-03-12
categories: Swift
---

#### 이 글은 FAST CAMPUS의 iOS School "이봉원" 강사님의 강의를 듣고 정리한 내용입니다

# iOS School - Lecture 1

- **주석(Comment)**
    - // : 한 줄 주석
    - /// : 한 줄 주석 + Quick Help Markup
    - /* */ : 멀티 라인 주석

- 주석을 쓰는 이유
    - 1. 빠르게 특정 부분의 코드를 비활성황
    - 2. 협업 또는 인계 시 이해를 돕기 위해
    - 3. 자기 자신의 이해를 위해
    - 4. 문서화
    - **주석 없이도 쉽게 이해할 수 있을 만한 코드를 짜는 것이 베스트이자 선행 과제**

- **Quick Help Markup??**

![Error img](assets/img/quick.png)

- **Semicolon (;)**
    - 각 라인의 마지막에 붙는 세미콜론은 옵션
    - 한 라인에 여러 구문(다중 명령)을 사용하고 싶을 경우는 세미콜론 필수
    - 예시
    
    ```
    print(1); print(2); print(3);
    
    print(1);
    
    print(2);
    
    print(3);
    ```

# Constants and Variables

- **상수와 변수는 현재 어떤 데이터에 대한 상태값, 속성 정보 등을 담고 있는 컨테이너**
    - **상수(Constants) : 한 번 설정되면 값 변경 불가**
    - **변수(Variables) : 설정한 값을 변경 가능**

```
let yourBirthDay = 430 // 상수
var myBirthDay = 424 // 변수
```

# Declare multiple constants or variables

# 다중선언

```
var x = 0.0, y = 0.0, z = 0.0
x = 1
y = 2
z = 3
```

# Type Annotation

- **변수 선언 시 사용될 자료의 타입을 명확하게 지정하는 것**

```
let year: Int = 2019
    
var language: String
language = "Korean"
```

# Type Inference
- **변수 및 상수 선언 시 초기화로 사용되는 값의 타입을 통해 변수의 타입을 추론하여 적용하는 것**

```
let name: String = "Jun" // String type // Type Annotation

let age: Int = 77 // Int type // Type Annotation
    
var weight = 73.2 // Double type // Type Inference

var spelling = ["J", "u", "n"] // String type // Type Inference
```

# Literals and Types

- **상수** 
    - 고정된 값(메모리 주소)을 가지는 심볼/식별자
- **리터럴**
    - 소스코드에서 고정된 값으로 표현되는 문자(데이터) 그 자체
    - 정수/실수/문자/문자열/블리언 리터럴 등

# Numeric Literals

```
var signedInteger = 123 //123 //Int type
signedInteger = +123 //123 //Int type
signedInteger = -123 //-123 //Int type

let decimalInteger = 17 //17 //Int type
let binaryInteger = 0b10001 //17 //Int type

let octalInteger = 0o21 //17 //Int type
let hexadecimalInteger = 0x11 //17 // Int type

var bigNumber = 1_000_000_000 //1000000000 // Int type
bigNumber = 000_001_000_000_000 //1000000000 // Int type
```

- 위의 예시에서 언더바( _ )의 용도는 큰 숫자를 가독성이 좋게 나타내기 위해서 사용
- 언더바 앞에 숫자 0은 무시한다

# Integer types
- 8-bit: Int8, UInt8
- 16-bit: Int16, UInt16
- 32-bit: Int32, UInt32
- 64-bit: Int64, UInt64
- Platform dependent: Int, UInt (64-bit on modern devices)
    - 플랫폼에 따라 Int와 UInt가 다르다, 현대 기기들은 64 bit 사용한다

- UInt에 음수를 넣으면 overflow 오류가 뜬다
    - UInt는 양수 범위만 표현한다
- Int8에 127을 초과하는 숫자를 넣으면 overflow 오류가 뜬다
    - Int8의 범위는 -128 ~ 127 이다
