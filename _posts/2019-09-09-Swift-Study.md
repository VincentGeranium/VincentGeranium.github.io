---
layout: post
title:  "Swift 프로그래밍 (데이터 타입 안심, 타입 별칭)"
date:   2019-09-09
categories: iOS, Swift
---

이 포스트는 야곰님의 스위프트 프로그래밍 2판을 보고 공부한 내용을 적어나간 포스트입니다.

---

### 데이터 타입 안심

- 스위프트의 특징 중 **안전성(safe)** 이 가장 뚜렷하게 나타나는 부분

- `스위프트`는 `타입에 민감, 엄격`

- `서로 다른 타입`끼리의 `데이터 교환`은 꼭 `타입캐스팅(Type-Casting, 형변환)을 거쳐야 함`.

    - 값 타입의 데이터 교환은 엄밀히 말하면 타입캐스팅이 아닌 새로운 인스턴스를 생성하여 할당하는 것이다.
    
---

### 타입 별칭 (typealias)

- 스위프트에서 `기본으로 제공`하는 `데이터 타입`, `사용자가 임의로 만든 데이터 타입`, `이미 존재하는 데이터 타입 등` `데이터 타입`에 `임의로 다른 이름(별칭)을 부여`할 수 있다.

- `타입에 별칭을 부여`한 후 `기본 타입 이름`과 `이후 추가한 별칭`을 `모두 사용 가능`하다.

```swift
typealias MyInt = Int
typealias YourInt = Int
typealias MyDouble = Double

let age: MyInt = 100 // MyInt는 Int의 별칭, 또 다른 이름.
var year: YourInt = 2080 // YourInt는 Int의 별칭, 또 다른 이름.

year = age // MyInt도 YourInt도 Int이기 때문에 같은 타입으로 취급한다.

let month: Int = 7 // 기존의 Int도 사용 가능
let percentage: MyDouble = 99.9 // MyDouble은 Double의 별칭, 또 다른 이름. // Int 외에 다른 자료형도 모두 별칭 사용 가능
```

---

### 튜플 (Tuple)

- `튜플(Tuple)`은 `타입의 이름`이 `따로 지정되어 있지 않다`.

- `튜플은 프로그래머 마음대로 만드는 타입이다`.

- `튜플`은 `타입 이름`이 `따로 없으므로` `일정 타입`의 `나열`만으로 `튜플 타입을 생성`해줄 수 있다.

- `튜풀`에 포함될 `데이터의 개수`는 `자유`롭게 정할 수 있다.

```swift
// String, Int, Double 타입의 튜플
var person: (String, Int, Double) = ("Jun", 100, 182.5)

// 인덱스를 통해서 값을 빼 올 수 있다
print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

// print 결과값 => 이름: Jun, 나이: 100, 신장: 182.5

// 인덱스를 통해 값을 할당할 수 있다
person.1 = 99
person.2 = 178.5

print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")
// 결과값 => 이름: Jun, 나이: 99, 신장: 178.5
```

- `튜플의 각 요소`를 `이름 대신 숫자로 표현`

    - `숫자로 표현`하기 `때문에 간편해 보일 수 있지만, 차후에 다른 프로그래머가 보았을 때, 코드의 의미 파악에 어려움을 갖을 수 있다.`
    
- 그래서 `튜플의 요소마다 이름`을 `붙여줄 수도 있다`.
        
```swift
// 튜플 요소 이름 지정

// String, Int, Double 타입의 튜플
var person: (name: String, age: Int, height: Double) = ("Jun", 100, 182.5)

// 요소 이름을 통해서 값을 빼 올 수 있다.
print("이름: \(person.name), 나이: \(person.age), 신장: \(person.height)")

// print 결과값 => 이름: Jun, 나이: 100, 신장: 182.5

// 요소의 이름을 통해 값을 할당할 수 있다
person.age = 99

// 인덱스를 통해서 값을 할당할 수 있다
person.2 = 178.5

// 기존처럼 인덱스를 이용하여 값을 빼 올 수도 있다
print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

// print 결과값 => 이름: Jun, 나이: 99, 신장: 178.5
```

- `튜플에는 타입 이름`에 `해당하는 키워드`가 `따로 없다` 보니 `사용에 불편함`을 겪기도 한다.

    - 매번 같은 모양의 튜플을 사용하고 싶을시, `선언해줄 때마다 긴 튜플 타입을 모두 써줘야 하는 불편함`이 생길 수 있기 때문이다.
    
- `이럴 때`는 `타입 별칭`을 `사용`하여 `조금 더 깔끔하고 안전하게 코드를 작성`할 수 있다

```swift
// 튜플 별칭 지정

typealias PersonTuple = (name: String, age: Int, height: Double)

let Jun: PersonTuple = ("Jun", 100, 178.5)
let Michael: PersonTuple = ("Michael", 150, 183.5)

print("이름: \(Jun.name), 나이: \(Jun.age), 신장: \(Jun.height)")
// print 결과값 => 이름: Jun, 나이: 100, 신장: 178.5

print("이름: \(Michael.name), 나이: \(Michael.age), 신장: \(Michael.height)")
// print 결과값 => 이름: Michael, 나이: 150, 신장: 182.5
```