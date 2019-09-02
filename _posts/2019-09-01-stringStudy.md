---
layout: post
title:  "String 다루기"
date:   2019-09-01
categories: iOS, Swift
---

## String 다루기

---

## Extended Grapheme Clusters (확장적 문자소 집합)

- Grapheme : 문자소(의미를 나타내는 최소 문자 단위)

- Swift에서 하나의 Character는 `Single Extended Grapheme Clusters`를 나타냄

    - `Extended Grapheme Clusters`라는 것은 사람이 읽을 수 있는 하나의 문자를 지칭한다
    
```swift
let precomposed: Character = "\u{D55C}" // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}" //ㅎ,ㅏ,ㄴ 

print(precomposed) // 한
print(decomposed) // 한
```

- `decomposed`는 Character 타입에 3개의 `scala`가 들어간다.

    - `scala` = 최소 의미를 담은 `Character 값` 을 의미

        - ex. \u{1112}

- 즉, `Exteded Grapheme Clusters`에서는 `1 scala = 1 Character` 가 `아니고` `1 Character = 1개 혹은 여러개의 scala` 가 `되는 것이다.`

- **인덱스를 통해서 String를 다룰 수 없는 이유가 여기서 나타난다.**

    - **각각의 `Character`가 `여러개`의 `scala` 값을 `가질 수 있기 때문에` `동일한 메모리`로 `한정된 저장공간`을 `가지기 어렵다`**
    
- 그렇기 때문에 `String`을 만들 때 `Character 별로 동일한 크기의 메모리를 할당할 수 없고`, 이는 `인덱스`를 `통한 접근을 불가능`하게 만든다

---

```
Swift에서 채택한 Extended Grapheme Clusters는 다양한 언어를 직관적으로 표시할 수 있게 도와준다

하지만

Extended Grapheme Clusters는 서로 다른 크기의 Character를 만들기 때문에 String[Int]를 통한

String의 개별 Character로의 접근은 불가능하다.
```

---

## Swift의 String 접근하기

- Swift에서는 `String[Int]`를 통해 개별 문자에 접근하기 어렵다.

    - 그래서 `Swift에서 제공하는 메소드들을 사용`해야 한다.
    
- Swift에서는 `String.index 메소드`를 통해서 `개발문자 혹은 범위`로의 `접근`을 할 수 있다.

- `가장 기본`이 되는 `2가지 메소드`는 `startIndex`와 `endIndex` 이다.

---

### 개별 Character  접근하기 (startIndex,  endIndex)

```swift
let sayHello: String = "Hello"

print(sayHello.startIndex) // Index(_rawBits: 0)
print(sayHello.endIndex) // Index(_rawBits: 327680)
```

- sayHello.startIndex는 0, sayHello.endIndex는 5 를 반환

    - `Hello`는 5글자이고, 0부터 시작하면 4까지인데, `endIndex`는 `5`
        
        - 즉, endIndex는 전체 String 길이를 반환한다는 것을 알 수 있다.
        
- **위의 메소드들을 통해서 String의 Character들을 접근할 수 있다.**

```swift
let sayHello = "Hello"

print(sayHello[sayHello.startIndex]) // H -> 0번째 인덱스, 첫번째 글자
print(sayHello[sayHello.index(before: sayHello.endIndex)]) // o -> 4번째 인덱스, 마지막 글자
```

- `sayHello[메소드를 통해 접근한 특정 인덱스]`의 표현을 통해 `개별 Character에 접근`할 수 있다

    - `숫자`로 접근하면 `Error`
    
- `sayHello[sayHello.startIndex]`이 H를 출력하는것은 `직관적`.

- `sayHello[sayHello.endIndex]`의 경우 `직관적이지 않다.`

    - 그 `이유`는 `전체 문자는 0부터 4까지`인데, `sayHello.endIndex`는 `5`이기 때문이다
    
- 그래서 `sayHello[sayHello.endIndex]는 에러`이고, `마지막 문자에 접근`하기 위해서는 `endIndex 앞의 인덱스에 대한 접근이 필요`하다.

- Swift는 이와 같은 `앞쪽 혹은 뒤쪽 문자에 대한 접근`을 위해 `string.index[before:]`와 `string.index[after:] 메소드를 제공`한다.

    - `맨 마지막 글자에 접근`하기 위해서는 `endIndex 앞의 문자를 접근`해야 하므로, `sayHello[sayHello.index(before: sayHello.endIndex)]`이 `마지막 문자 o를 가리키는 인덱스`가 된다
    
    - `비슷한 원리`로 `sayHello[sayHello.index(after: sayHello.startIndex)]`를 사용하면 `H` 다음의 문자 `e`에 `접근이 가능`하다
    
---

### 개별 Character 접근하기(offsetBy)

- `startIndex와 endIndex`는 `String의 시작과 끝(혹은 그 앞뒤 인덱스)`으로의 `접근만 가능`할 뿐, `중간에 있는 문자에 대한 접근은 어렵다`.

- 그래서 Swift는 `중간에 있는 문자에 접근`하기 위한 `index(_:offsetBy:) 메소드`를 별도로 `제공`한다.

- **offsetBy 메소드는 시작 지점부터 떨어진 정수 값만큼을 더한 위치를 반환한다**

```swift
let greetingToWorld = "Hello World"

print(greetingToWorld[greetingToWorld.index(greetingToWorld.startIndex, offsetBy: 0)]) // H
print(greetingToWorld[greetingToWorld.index(greetingToWorld.startIndex, offsetBy: 6)]) // W

print(greetingToWorld[greetingToWorld.index(greetingToWorld.endIndex, offsetBy: -1)]) // d
print(greetingToWorld[greetingToWorld.index(greetingToWorld.endIndex, offsetBy: -3)]) // r
```

- 첫 번째와 두 번째 예시는 시작지점이 greetingToWorld.startIndex

    - 첫 번째 예시는 greetingToWorld.startIndex에서 0만큼 떨어진 것은 자기 자신이므로 H
    
    - 두 번째 예시는 greetingToWorld.startIndex에서 6만큼 떨어진 것은 W
        
        - 자기 자신의 인덱스에서 6을 더한 것
        
- 세 번째와 네 번째 예시는 뒤쪽에서 접근하는 방법

     - greetingToWorld.endIndex는 전체 String의 가장 마지막 값
     
     - greetingToWorld.endIndex는 전체 길이를 반환하므로 -1을 더하면 전체 String의 마지막 문자를 지칭하는 인덱스가 된다
     
     - 이와 같은 원리로 -3을 더하면 r이 나온다.

---

### 루프를 통해 전체 String에 접근하기

- 크게 3가지 방법

- 첫 번째, greetingToWorold를 사용하여 개별 문자(value)에 접근하는 방식

```swift
for i in greetingToWorld {
    print(i)
}

// H, e, l, l, o, ,W, o, r, l, d -> 띄어쓰기 포함 각각 접근

```

- 두 번째, indice를 활용하여 인덱스에 접근

```swift
for indices in greetingToWorld.indices {
    print(indices)
}
// 정수 인덱스가 아닌 Swift에서 만들어낸 인덱스에 접근

// Index(_rawBits: 0)
// Index(_rawBits: 65792)
// Index(_rawBits: 131328)
// Index(_rawBits: 196864)
// Index(_rawBits: 262400)
// Index(_rawBits: 327936)
// Index(_rawBits: 393472)
// Index(_rawBits: 459008)
// Index(_rawBits: 524544)
// Index(_rawBits: 590080)
// Index(_rawBits: 655616)
```

- 마지막, 인덱스와 개별 문자를 동시에 접근하는 방법

```swift
for (index, value) in greetingToWorld.enumerated() {
    print("index: \(index), value: \(value)")
}
// index는 정수, value는 인덱스에 위치한 문자

// index: 0, value: H
// index: 1, value: e
// index: 2, value: l
// index: 3, value: l
// index: 4, value: o
// index: 5, value:  
// index: 6, value: W
// index: 7, value: o
// index: 8, value: r
// index: 9, value: l
// index: 10, value: d
```

---

## String Insert

- String Insert는 어떤 내용을 어떤 곳에 넣을 것인지를 통해 나타난다

- 이때 사용하는 메소드는 insert(_:at:), insert(contentsOf:at:) 이다.

```swift
var str = "Hello"

str.insert("A", at: str.startIndex) // "AHello"
str.insert(contentsOf: " World", at: str.endIndex) // "AHello World"
```

---

## String Remove

- String Remove의 경우, Insert와 유사하다.

    - 문자를 삭제할 위치 및 범위를 지정해주면 된다
    
- 이 때는 remove(_:at:), (removeSubrange(_:)) 메소드를 사용한다.

```swift
var removeStr = "AHello World"

removeStr.remove(at: removeStr.startIndex) // "A"
print(removeStr) // "Hello World"

let rangeOfWorld = removeStr.index(removeStr.endIndex, offsetBy: -6)..<removeStr.endIndex
removeStr.removeSubrange(rangeOfWorld) //Hello
```

- remove(_:at:) 메소드는 직관적으로 이해할 수 있다.

- range의 경우에는 아무 range나 사용해서는 안된다.
    
    - 하나의 배열도 range가 될 수 있기 때문이다.
    
    - 여기서 말하는 range는 String.index를 사용하여 닫힌 range를 의미한다.
    
    - 즉, 위의 예시처럼 removeStr.index 혹은 removeStr.endIndex 같은 것들로 닫힌 range를 지칭하는 것이다.
    
---

## Prefix와 Suffix(접두사와 접미사)

- hasPrefix(_:) 메소드와 hasSuffix(_:) 메소드는 String의 앞쪽 혹은 뒤쪽에 찾고자 하는 문자가 있는지를 확인할 수 있도록 해주는 메소드

- 특정 문자열이 앞에서부터(혹은 뒤에서부터) 포함되어 있는지 확인할 때 좋은 메소드

```swift
var hangle = "한글"

if hangle[hangle.startIndex] == "한" {
    print("첫 번째 글자가 한 입니다.")
}

if hangle.hasPrefix("한") {
    print("첫 번째 글자가 한 입니다.")
}

if hangle.hasSuffix("한글") {
    print("뒤쪽 글자가 글 입니다.")
}
```

---

## Substring (부분 문자열)

- String에는 String.Index 타입의 범위(Range)를 인자로 받는 subscript가 구현되어 있다.

```swift
let string = "abc123"

let start = string.index(after: string.startIndex)
let end = string.index(string.endIndex, offsetBy: -2)

let subString = string[start...end] // "bc12"
```

- String.Index를 이용해 범위(Range)를 만들고 이것을 문자열의 subscript 를 이용하면 Substring(부분문자열)을 구할 수 있다

```swift
let string = "abc123"

let start = string.index(after: string.startIndex)
let end = string.index(before: string.endIndex)

let subString = string[start..<end]  // "bc12"

type(of: subString) // Substring.Type
```

- 위의 예시와 같이 범위 표현 방식에 따라 같은 값을 가리키더라도 다른 코드로 구현할 수 있다.

```swift

let realSubstring = String(substring) // "bc12"

type(of: realSubstring) // String.Type

```

- Substring 타입은 특정 문자열의 부분 문자열을 담기 위한 특수한 타입이다.

    - 하지만 문자열이 아니기 때문에 String 타입이 필요한 곳에 그냥 넘겨 줄 수가 없다
    
    - String로 바꿔줘야 한다.
    
    - 타입의 용도가 다르기 때문에 형변환(type casting)이 안되는 점은 주의해한다.
    
---

참고자료
- [Eth Developer's Lab](https://hcn1519.github.io/articles/2017-07/swift_Str)
- [Seorenn SIGSEGV](http://seorenn.blogspot.com/2018/05/swift-string-index.html)
