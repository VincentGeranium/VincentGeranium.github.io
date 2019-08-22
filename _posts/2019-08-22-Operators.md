---
layout: post
title:  "Operators(연산자)"
date:   2019-08-22
categories: Swift, iOS
---

---

#### 알고리즘을 풀던 중 헷갈렸던 연산자 부분에 대해서 정리한 포스트입니다.

---

# 나머지 연산자 (Remainder Operator)

---

나머지 연산자 (a % b)는 b를 몇 배 곱하여 a에 맞춘 다음 남는 값을 반환.

<img width="500" alt="RemainderOperatorImage" src="https://user-images.githubusercontent.com/42841888/63490228-247e5e00-c4ef-11e9-9bb0-20b36db696de.png">

위의 그림은 9 % 4 를 어떻게 계산이 되고 값을 얻는지 알 수 있다.

    a = (b x 배수) + 나머지
    
- a % b에 **% 연산자**는 위의 방정식을 계산하고 나머지를 반환.

- a값이 음수라도 같은 방법으로 값을 얻을 수 있다.

---

# Nil 결합 연산자 (Nil Coalescing Operator)

---

Nil 결합 연산자 **(a ?? b)** 는 옵셔널 a를 풀어서 nil인지 아닌지를 확인하여,

**nil 이면 b 값을, nil이 아니면 a 값을 반환한다.**

항상 a는 옵셔널 타입이어야 하며 b는 a와 타입이 일치해야 한다.

```swift
let basicCodeName = "wolf"
var partnerCodeName: String // nil


var confirmCodeName = partnerCodeName ?? basicCodeName
// partnerCodeName 은 nil, 그러므로 confirmCodeName은 wolf 값을 갖게 된다
```

```swift
partnerCodeName = "fox"
confirmCodeName = partnerCodeName ?? basicCodeName
// partnerCodeName은 nil이 아니다, 그러므로 confirmCodeName은 fox 값을 갖게 된다
```
---

# 반 열림 범위 연산자 (Half-Open Range Operator)

---

반 열림 범위 연산자 **(a..<b)** 는 a에서 b까지 수행되는 범위지만 b는 포함되지 않음.

처음 값은 포함하지만 마지막 값은 포함하지 않음.

a는 b보다 크면 안됨.

**반 열림 범위는 0을 기반으로 한 배열을 작업할 때 유용**

```swift
let friendsName = ["Jun", "Loco", "JayPark", "HaOn"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(friendsName[i])")
}

// Person 1 is called Jun
// Person 2 is called Loco
// Person 3 is called JayPark
// Person 4 is called HaOn
```
