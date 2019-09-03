---
layout: post
title:  "프로그래머스 알고리즘(문자열 내 마음대로 정렬하기)"
date:   2019-09-03
categories: iOS, Swift
---

```swift
func solution(_ strings:[String], _ n:Int) -> [String] {
    let resultArray = strings.sorted {
        let first = $0[$0.index($0.startIndex, offsetBy: n)]
        let second = $1[$1.index($1.startIndex, offsetBy: n)]
        print("first : \(first)")
        print("second : \(second)")
        
        if first == second {
            return $0 < $1
        } else if first < second {
            return first < second
        } else {
            return false
        }
    }
    
    return resultArray
}
```

---

### 알고리즘을 풀면서 새롭게 알게된 점

- 문자간에 비교연산이 가능

각각 서로 다른 두 문자가 있다고 가정하고, 이 두 문자를 비교하여 같은지 혹은 다른지 불리언 값을 반환하는 비교 연산자(==, !=)를 사용하여 비교연산이 가능하다는 것은 알고 있었다.

그러나 두 문자를 값이 큰지 작은지를 비교하는 연산자(>, <)를 사용하여 문자의 크기를 비교? 할 수 있다는 것을 새롭게 알 수 있었다.

이렇게 연산자(>, <)를 이용하여 비교를 하게 되면 불리언 값을 돌려준다.

```swift

let stringA = "A"
let stringB = "B"

// compare
stringA > stringB // false
stringA < stringB // true

```

---

### sorted(by:)

- 맨 위에 알고리즘을 푼 코드를 보면 sorted(by:)를 이용하였다, sorted(by:) 안에 구현된 코드 중 if 문에 대해 해석을 해보려 한다

```swift

let first = $0[$0.index($0.startIndex, offsetBy: n)]

let second = $1[$1.index($1.startIndex, offsetBy: n)]
        
        if first == second {
            return $0 < $1
        } else if first < second {
            return first < second
        } else {
            return false
        }
        
```

- $0[$0.index($0.startIndex, offsetBy: n)] 이 코드는 배열 내에 있는 아이템의 n번째 character 접근하는 코드

- if 문을 보면 아이템의 n번째 character을 비교하는것이 아니고 그 문자열 자체. 즉, 아이템의 n번째 character이 아닌 string를 비교하여 같으면 $0 < $1 을 리턴하는데 이것을 조금 더 자세히 들여다 보자

    - 문자열 자체를 비교하는 이유는 알고리즘의 제한조건에 "인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다." 라고 나와있어 비교하려는 character가 같으므로 문자열 자체를 비교하여 사전순으로 정렬한다.

    - sorted(by:) 메소드는 Swift 내장 메소드로 배열을 by: 이하의 기준에 따라 정렬하는 메소드이다
    
    - 그 기준은 배열에 있는 데이터 타입들 간의 대소비교를 통해 이루어진다
    
        - 즉, 배열의 두 값을 가져와 그 크기를 비교하여 앞의 값이 뒤의 값보다 이전에 와야하면 true, 그렇지 않으면 false를 반환하는 것을 반복하고 그 결과에 따라 정렬한다

![algorithm_sorted](/assets/img/algorithm_sorted.png)