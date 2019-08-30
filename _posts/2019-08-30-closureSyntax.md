---
layout: post
title:  "closure 정리"
date:   2019-08-30
categories: iOS, Swift
---

# Closure

- Closure는 익명함수로 알려진 기능

-  `func` 키워드로 선언하는 것이 아니라, 함수를 `변수에 선언하는 형태`를 취하고 있다

- Closure는 코드를 간결하고, 직관적으로 작성하는데 많은 도움을 주는 기능

---

# 일반적 함수의 사용과 Closure의 사용 방식의 차이

---

## 일반적 함수 사용

```swift
var counter = 0
func addCounter() {
    counter += 1
}

addCounter()
addCounter()

print(counter) // 결과값 2
```

- 일반적인 함수는 위와 같이  함수명(addCounter)을 설정하고, 해당 함수명으로 함수를 호출하는 형태를 취한다.

---

## Closure

```swift
var counter = 0
let addCounter = {
    counter += 1
}

addCounter()
addCounter()

print(counter) // 결과값 2
```

- Closure는 변수에 값을 선언하는 대신 변수에 `함수`를 선언한다.

- 위와 같이 `addCounter` 변수에 `함수`를 선언하였다.

- 그리고 이 변수(addCounter)는 함수처럼 호출을 할 수 있다 -> `addCounter()` 의 형태

---

## Closure 기본 형태

- Closure는 기본적으로 `Header`와 `Body`를 가진 형태로 구성되어 있다.

```swift
var closure = { Header in Body }
```

- 여기서 `Header`에서는 `인자와 리턴타입`을 명시한다.

- `Body`에서는 호출시 `실행되는 함수의 내용`을 작성.

- `in` 키워드는 `Header`와 `Body`를 나누는 키워드이다.

<img width="505" alt="closureExpression" src="https://user-images.githubusercontent.com/42841888/63998796-edd2c400-cb3c-11e9-9f1e-537f80439ee0.png">

---

## sorted(by: )를 통한 Closure 설명

- `sorted(by: )` 메소드는 Swift 내장 메소드로 배열을 `by:` `이하의 기준에 따라 정렬`하는 메소드이다.

- 그 기준은 배열에 있는 데이터 타입들 간의 `대소 비교`를 통해 이뤄진다.

    - 즉, 배열의 두 값을 가져와 그 크기를 비교하여 앞의 값이 뒤의 값보다 이전에 와야하면 `true`, 그렇지 않으면 `false`를 반환하는 것을 반복하고 그 결과에 따라 정렬한다
    
```swift
let names = ["Chris", "Jiyeon", "Jun", "Sua", "Daniella"]
let numbers = [4,5,6,3,1]

// 배열 내의 데이터 타입에 따라 필요한 인자가 다르다.
names.sorted(by: (String, String) ->  Bool)
numbers.sorted(by: (Int, Int) -> Bool)
```

- `by`에서 필요한 값은 `Bool을 반환`하는 `함수의 형태` -> `일반적인 함수` 혹은 `Closure` 가 들어가게 된다

- 아래와 같은 형태들이  `sorted(by: )`의 인자로 들어가게 된다

```swift
let names = ["Chris", "Jiyeon", "Jun", "Sua", "Daniella"]
let numbers = [2,6,4,7,1]

// a1이 a2보다 클 때, 앞에 와야한다를 의미
// "Sua"가 "Jun" 보다 크고 이 때 true이므로 "Sua"가 "Jun"보다 배열의 앞쪽에 위치한다.
// 결과적으로 배열 전체가 내림차순으로 정렬된다

// 일반적인 함수의 형태
func reverse(_ a1: String, _ a2: String) -> Bool {
    return a1 > a2
}

// 일반적인 함수를 들어가게 함
var nameReverse = names.sorted(by: reverse) // 결과값 ["Sua", "Jun", "Jiyeon", "Daniella", "Chris"]

var numberReverse = numbers.sorted { (_ a1: Int, _ a2: Int) -> Bool in
    return a1 > a2
} // 결과값 [7, 6, 4, 2, 1]
```

---

## Closure 축약

- Closure의 `짧지만 직관적인 코드` 작성에 크게 기여하는 것이 `축약형`

- `어떤 경우` 축약을 하는지 `모른다면` 어떻게 `Closure가 작동하는지 모르는 상황에 직면`

### 1. Type Inferring

- Closure는 `어떤 타입의 데이터가 인자로 들어오고`, `return 값이 어떤 것인지 미리 알고 있다면` 이를 `생략`할 수 있다

```swift

names.sorted { (a1: String, a2: String) -> Bool in
    return a1 > a2
}

// 데이터 타입 생략
names.sorted { (a1, a2) -> Bool in
    return a1 > a2
}
```

- `sorted(by:)` 메소드의 `파라미터 함수`는 항상 `배열의 데이터 타입을 가진 인자 두개를 지닌다` 그리고 `Bool 타입`을 `리턴`한다.

- `즉, 어떤 데이터 타입이 필요한지 이미  알려져 있어서 Closure는 이를 추론 할 수 있다.`

    - 그러므로 모두 `생략` 가능하다.

```swift
var plus: (Int, Int) -> Int = { (a: Int, b: Int) in return a + b}

// 데이터 타입 생략
var plus: (Int, Int) -> Int = { (a, b) in return a + b }
```

- 위의 `plus`는 받은 두 값을 더한 값을 반환하는 변수

    - 이 때, 여기서는 변수를 선언할 때 타입을 `(Int, Int) -> Int`로 `명시`를 했기 때문에, `Closure`에서 `이미 어떤 데이터 타입이 인자로 오고 어떤 데이터 타입을 리턴`하는지 알고 있다
    
    - `그러므로 Closure 내부에서 이를 생략할 수 있다`
    
### 2. Single Expression Closure 의 "return" 키워드 생략

- Single Expression Closure는 `return` 키워드를 `생략할 수 있다.`

- 아래에서 Single Expression = `a1 > a2`, `n1 + n2` 

```swift
names.sorted { (a1, a2) -> Bool in a1 > a2 }
var plus: (Int, Int) -> Int = {(n1, n2) in n1 + n2 }
```

### 3. Short-hand argument name

- `Closure 내부`로 `들어오는 인자들`은 `항상 이름을 정의하지 않아도`, 순서대로 `$0, $1`의 이름으로 사용할 수 있다.

```swift
names.sorted(by: {$0 < $1} )
var plus: (Int, Int) -> Int = { $0 + $1 }
```

### 4. Operator Methods를 통한 축약

- `Operator(연산자)를 이용한 축약`은 `두 값`을 `연산`하는 것이 `결과`로 나오는 `특별한 경우`이기 때문에 사용할 수 있는 축약이다.

```swift
names.sorted(by: <)
var plus: (Int, Int) -> Int = (+)
```

- `sorted(by:)` 메소드는 `항상 두 값의 크기 비교`를 통해 `Bool을 반환` 하므로 `연산자(<)`만 `쓰는 것으로도` 그 `의미`를 `알 수 있다.`

- `plus`의 경우에도 `항상 두 값을 더한 값`을 `반환` 하므로 `연산자(+)`만으로도 `연산을 알 수 있다.`

- 때문에 위와 같은 축약이 가능하다.

---

## 함수로 Closure 전달하기

- `Closure`는 `변수`에 `저장`되기 때문에 `변수`를 `함수`에  `넘길 수 있는` 것처럼, `Closure`도 `함수로 넘길 수 있다`
    
    - `그 형태는` 일반적인 `변수를 넘기는 것과 동일`

    - `func 함수명(label 변수명: 변수타입)` 이 조건에 맞게만 써주면 된다.
    
```swift
var hi: () -> Void = { print("Hi!") }
var bye: () -> Void = { print("bye bye~") }

func runClosure(name aClosure: () -> Void) {
    aClosure()
}

runClosure(name: hi) // Hi!
runClosure(name: bye) // bye bye~
```

### Trailing Closure를 활용한 Syntax

- `Trailing Closure`는 `함수의 호출시 Closure가` 지나치게 `길어질 경우` 이를 `함수와 분리`해서 쓸   수 있는 Syntax Sugur 이다.

```swift
runClosure() {
    // aClosure() 가 호출된 시점에서 실행
    print("trailing 1")
}

// 인자가 Closure 밖에 없다면 ()를 생략할 수 있다
runClosure {
    print("trailing 2")
}
```

- 인자가 한 개가 아닌 경우 다음과 같이 사용할 수 있다.

```swift
// 인자가 한 개가 아닌 경우
func runClosure2(index: Int, name aClosure: () -> Void) {
    aClosure()
}

runClosure2(index: 2) {
    // index는 2로 넘기고, aClosure()가 호출된 시점에서 Hello! 출력
    print("Hello!")
}
```

### Map Method

- Trailing closure 형태로 사용하는 대표적인 메소드 중 하나 `map(_:)`

- `map(_:)`은 `collection 데이터 타입 안의 모든 객체(혹은 일부)를 수정`할 때 `사용`하는 메소드

    - 일종의 루프, 일반적인 루프라기 보다는 값을 새롭게 `mapping`하는데 목적이 강하다
    
```swift
var variableNumber = [1,5,6,2,8]

variableNumber = variableNumber.map({ (value) -> Int in
    var newVal = value + 1
    return newVal
})
```

- 위의 예시는 `variableNumber` 배열의 값들을 기존 값 + 1의 값들로 새롭게 `mapping`

- 위의 예시처럼 기존과 동일한 리턴 타입을 가질 수도 있지만 그렇지 않아도 된다

```swift
let digitName = [0:"Zero", 1:"One", 2:"Two", 3:"Three", 4:"Four", 5:"Five", 6:"Six", 7:"Seven", 8:"Eight", 9:"Nine"]

let oddOrEvenArr = digitName.map { (key, value) -> String in
    var str = ""
    
    if (key % 2) == 0 {
        str = "짝수"
    } else {
        str = "홀수"
    }
    return str
}

print("🔵: \(oddOrEvenArr)")
// 🔵: ["홀수", "홀수", "홀수", "짝수", "짝수", "짝수", "짝수", "홀수", "짝수", "홀수"]



let oddOrEvenDic = digitName.map { (key, value) -> [Int: String] in
    var str = ""
    if (key % 2) == 0 {
        str = "짝수"
    } else {
        str = "홀수"
    }
    return [key: str]
}

print("🔵: \(oddOrEvenDic)")
🔵: [[1: "홀수"], [3: "홀수"], [8: "짝수"], [0: "짝수"], [4: "짝수"], [5: "홀수"], [9: "홀수"], [2: "짝수"], [6: "짝수"], [7: "홀수"]]
```

- 위의 예시는 각각 digitName을 새롭게 mapping 하여 만든 배열과 딕셔너리이다.