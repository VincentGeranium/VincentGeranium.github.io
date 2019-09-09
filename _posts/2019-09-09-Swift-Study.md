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

- 스위프트는 타입에 민감, 엄격

- `서로 다른 타입`끼리의 `데이터 교환`은 꼭 `타입캐스팅(Type-Casting, 형변환)을 거쳐야 함`.

    - 값 타입의 데이터 교환은 엄밀히 말하면 타입캐스팅이 아닌 새로운 인스턴스를 생성하여 할당하는 것이다.
    
---

### 타입 별칭 (typealias)

- 스위프트에서 기본으로 제공하는 데이터 타입, 사용자가 임의로 만든 데이터 타입, 이미 존재하는 데이터 타입 등 데이터 타입에 임의로 다른 이름(별칭)을 부여할 수 있다.

- 타입에 별칭을 부여한 후 기본 타입 이름과 이후 추가한 별칭을 모두 사용 가능하다.

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