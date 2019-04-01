---
layout: post
title:  "Swift - 알고리즘 공부 [문자열 다루기 기본]"
date:   2019-04-01
categories: Swift
---

# Coding Test Practice

## Algorithm  
  
### 이 포스트는 프로그래머스의 알고리즘 연습 문제를 풀고 정리하여 올리는 포스트 입니다

---

- 문제 : 문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, answer을 완성하세요.
    - 예를 들어 param이 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다.  

---

### 나의 풀이

```
func answer(_ param: String) -> Bool {
    guard param.count == 4 || param.count == 6
        else {
        return false
    }
    
    return Int(String(param)) != nil ? true : false
    
}
```

---

### 결과

- answer("1234")
    - true -> String 타입인 1234 이므로 숫자로만 구성돼어 있어서 true
- answer("asd1")
    - false ->  String 타입인 "asd1", 문자열이 숫자로만 구성돼어 있지 않으므로 false
- answer("1234567")
    - false -> String 타입인 "1234567"이 모두 숫자로만 구성돼어 있지만 길이가 6을 넘으므로 false
- answer("123")
    - false -> String 타입인 "123"이 모두 숫자로만 구성돼어 있지만 길이가 4미만 즉, 3 이므로 false
  
---

### 배운점

- guard 문의 활용법과 쓰임새를 알게 되었다.
- 삼항연산자를 사용하면 간결하고 쉬운 코드를 만들 수 있다는 것을 알게 되었다.
- 논리연산자에 대해 깊이 고민해보고 사용해보는 시간이 되었다.
- optional 공부가 부족하다는 것을 알게되었다.

