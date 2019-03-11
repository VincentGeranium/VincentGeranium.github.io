---
layout: post
title:  "Swift-자료형-2"
date:   2019-03-11
categories: Swift
---

# Int 자료형 구조체

- **Int 자료형은 사실 SingedInteger를 구현한 구조체의 일종**
- **Int 자료형은 SignedInteger라는 객체를 뼈대로 하여 만들어졌다**

- Int 구조체 구현

```
/// A 64-bit signed integer value
/// type.
public struct Int : SignedInteger, cmparable, Equatable {
    /// Create an instance initalized to zero.
    public init()
    
    /// Create an instance initalized to 'value'.
    public init(_ value: Int)
    
    /// Creates an integer from its big-endian representation, changing the
    /// byte order if necessary.
    public init(bigEndian value: Int)
    
    /// Creates an integer from its little-endian representation, changing the
    /// byte order if necessary
    public init(littleEndian value: Int)
    
    /// Create an instance initialized to 'value'.
    public init(integerLiteral value: Int)
    
    ///Returns the big-endian representation of the integer, changing the
    /// byte order if necessary
    public var bigEndian: Int{ get }
    
    /// Returns the little-endian representation of the integer, changing the
    /// byte order if necessary
    public var littleEndian: Int{ get }
    
    /// Returns the current integer with the byte order swapped.
    public var byteSwapped: Int { get }
    public static var max: Int { get }
    public static var min: Int { get }
    
    ...(중략)
    
}
```

- **Int 내부에는 여러가지 메소드나 속성 변수들이 다량 정의되어 있다**

```
public static var max: Int { get }
public static var min: Int { get }
```
- 이 두 가지 속성은 각각 Int 자료형이 가질 수 있는 최대값(=max)과 최소값(=min)을 의미한다
- Int 타입에 저장할 수 있는 값의 범위, **즉 최대값과 최소값, 그 값을 max와 min 속성을 통해서 가져올 수 있다는 뜻이다**

```
Int.max -> 9223372036854775807
Int.min -> -9223372036854775808

Int64.max -> 9223372036854775807
Int64.min -> -9223372036854775808

Int32.max -> 2147483647
Int32.min -> -2147483648

Int16.max -> 32768
Int16.min -> -32768

Int8.max -> 127
Int8.min -> -128
```

- 64bit의 실행 환경에서 Int는 Int64와 같은 처리 결과를 가진다
- 32bit의 실행 환경이라면 Int는 Int32와 같은 처리 결과를 가진다
- **Int 자료형은 Int8, Int16, Int32, Int64까지의 서브 자료형을 가지고 있다**
    - **실행 환경의 플랫폼에 따라 유연하게 처리되는 특성을 가지고 있다**
- 양수부터 음수까지의 정수를 저장하고자 할 때는 Int 타입을 사용한다

# UInt

- **UInt는 Unsigned Integer를 줄인 단어로 부호가 없는 정수를 의미한다**
- Int처럼 정수값을 저장하는 데 사용되는 자료형이지만 Int가 양수부터 음수까지를 모두 저장할 수 있는 반면 UInt는 양수만 저장할 수 있다는 차이가 있다
- **UInt는 0을 포함하여 1,2,3,...등 우리가 일반적으로 자연수라고 부르는 범위의 정수를 저장할 수 있

#### Int를 써도 되는데 왜 굳이 UInt를 사용할까??
- **UInt는 마이너스 범위의 정수를 저장할 수 없는 대신, 플러스 범위의 정수에 대해서는 Int보다 두 배 큰 범위까지 저장할 수 있다**
- 8bit의 CPU를 예로 들어 설명
    - UInt는 Int와 동일하게 값을 256개 저장할 수 있지만 마이너스 범위까지 값을 할당할 필요가 없으므로 플러스 범위의 128개를 더 사용할 수 있어서 ~ 255까지 저장할 수 있다
    - 양의 정수 범위만 다루는 데이터에는 UInt가 훨씬 효율적이다
        - Ex) 나이, 물건의 개수, 참여인원의 수, 반복 횟수 등
- **UInt에도 Int처럼 8비트, 16비트, 32비트, 64비트로 구분된 서브 자료형이 있다**
    - **각각 UInt8, UInt16, UInt32, UInt64라는 이름으로 정의되어 있다**

#### UInt 타입에 따른 값의 범위
- UInt8, 저장할 수 있는 값의 범위 : 0 ~ 255 , 크기: 8bit
- UInt16, 저장할 수 있는 값의 범위 : 0 ~ 65,535 크기 : 16bit
- UInt32, 저장할 수 있는 값의 범위 : 0 ~ 4,294,967,295, 크기: 32bit
- UInt64, 저장할 수 있는 값의 범위 : 0 ~ 18,446,744,073,709,551,615 , 크기: 64bit
- UInt는 0부터 플러스 범위의 정수를 저장하기 때문에 저장할 수 있는 최소값은 서브 자료형의 종류와 상관 없이 모두 0이다

#### UInt 구조체

```
/// A 64-bit unsigned integer value
/// type.

public struct UInt : UnsignedInteger, Comparable, Equatable {
    
    /// Create an instance initialized to zero.
    public init()
    
    /// Create an instance initialized to 'value'.
    public init(_ value: UInt)
    
    /// Create an integer from its big-endian representation, changing the
    /// byte order if necessary
    public init(bigEndian value: UInt)
    
    /// Creates an integer from its little-endian representation, changing the
    /// byte order if necessary.
    public init(littleEndian value: UInt)
    
    /// Create an instance initialized to 'value'.
    public init(integerLiteral value: UInt)
    
    /// Returns the big-endian representation of the integer, changing the
    /// byte order ig necessary.
    public var bigEndian: UInt{ get }
    
    /// Returns the little-endian representation of the integer, changing the
    /// byte order if necessary.
    public var littleEndian: UInt { get }
    
    /// Returns the current integer with the byte order swapped.
    public var byteSwapped: UInt { get }
    public static var max: UInt { get }
    public static var min: UInt { get }
    ...(중략)
}
```

# Double & Float

- **Double 타입과 Float 타입 둘 다 실수값을 저장할 수 있는 자료형이라는 공통점이 있다**
    - **Double 타입은 64bit 부동소수점 자료형**
    - **Float 타입은 32bit 부동소수점 자료형**
- Double 타입은 특별히 매우 정확해야 하는 부동소수점 값이나 또는 매우 넓은 범위의 실수값을 저장할 때 사용된다
    - 그 이외의 부동소수점 값에는 Float 타입이 사용된다
- 일반적으로 Float 타입은 소수점 아래 7 ~ 8 자리까지의 값을 정확하게 저장
- 일반적으로 Double 타입은 소수점 아래 15 ~ 16 자리의 값을 정확하게 저장
    - Float 타입보다 훨씬 더 세밀한 값을 저장하는 데에 유리하다
- 메모리에서 차지하는 크기도 Double 타입이 Float 타입보다 크다
- Swift에서 Float 타입의 서브 자료형으로 사용되는 Float32와 Float64 이 둘은 실제로 존재하는 객체가 아니라 Typealias에 의해 정의된 타입들이다

```
/// A 32-bit floating point type
typealias Float32 = Float

/// A64-bit floating point type
typealias Float64 =  Double
```
- **32bit 실수는 Float로 처리하고, 64bit 실수는 Double로 처리한다는 의미로 해석할 수 있다**

# Bool

- **Bool은 true/false 두 가지 종류의 값만 가질 수 있는 자료형**
    - **주로 논리값을 저장하기 위해 사용**
- 참/거짓, 성공/실패, 스위치의 on/off등 두 가지 상태만 존재하는 데이터에 사용되며, 조건문의 결과를 표현하는 데에도 많이 사용된다
- 조건문은 조건식의 참/거짓 판단 결과에 따라 조건절의 실행 여부가 결정되는 구문이다

```
// Bool 타입 저장 변수
var close = true

// Bool 타입의 저장 상수
let success = true
let fail = false
```

# String

- "ABC","가나다" 처럼 문자열을 저장할 때 사용된다
- 스위프트 언어에서 제공되는 기본 자료형
- **String 타입 데이터의 값을 표현할 때 큰따옴표를 사용한다**

```
// String 타입 저장 변수
var projectname = "iOS study"

// String 타입 저장 상수
let language = "swift"
```

- 스위프트에서 Objecetive-C에서 사용되는 NSString을 사용할 수도 있다
    - import Foundation이라는 구문을 사용하여 파운데이션 프레임워크만 반입하면 사용 가능
    - NSString와 String 사이의 타입 변환 과정은 오류가 발생할 가능성이 전혀 없는 완전 변환

# Character

- String은 여러 글자로 이루어진 문자열을 저장할 수 있는 일종의 집단 자료형이다
- **Character는 한 개의 문자를 저장할 수 있는 단일 자료형이다**
    - **String 타입에 저장된 문자열을 하나씩 분해하면 Characte 타입이 된다**
- Character 타입의 데이터 값을 표현할 때도 String 타입과 마찬가지로 큰따옴표를 사용한다

```
// Character 타입 저장 변수
var character: Character = "C"

// Character 타입 저장 상수
let character: Character = "B"
```
