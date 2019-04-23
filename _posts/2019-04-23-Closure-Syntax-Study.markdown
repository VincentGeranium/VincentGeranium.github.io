--
layout: post
title:  "Closure 함축 문법  - 190423"
date:   2019-04-23
categories: iOS, Swift
---

# Closure Syntax Study

---

클로저의 표현 문법들을 공부하려 한다

이번 글은 바로 아래 코드를 예시로 하여 모든것을 일괄적으로 설명하고 알아보려한다

```
func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
    return method(a, b)
}
```

---

### 후행 클로저

클로저가 함수의 마지막 전달인자라면 마지막 매개변수 이름을 생략한 후 함수 소괄호 외부에 클로저를 구현할 수 있다

```
func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
    return method(a, b)
}
```

위에 코드를 보면 이 함수의 마지막 매개변수는 클로저를 받고 있다

```
method: (Int, Int) -> Int
```

method 라는 매개변수가 그 인자값으로 클로저를 받고 있는 것을 볼 수 있다

즉, 이 method 매개변수 이름을 생략한 후 함수 소괄호 와부에 클로저를 구현 할 수 있다는 말이다

```
var result
result = calculate(a: 10, b: 10) { (left: Int, right: Int) -> Int in
    return left + right
}

print(result) // 20
```

위의 코드를 보면 마지막 매개변수였던 클로저를 밖을 빼서 중괄호를 열어주고 그 안에 클로저가 받았던 인자값 2개를 써준다 

두가지는 Int 타입으로 받으니 매개변수 이름을 left와 right로 하고 그 타입을 Int로 지정해 주고

이 클로저의 반환타입이 Int 타입이므로 -> 다음에 Int를 명시해 준 다음에

in 다음에는 실행 구문을 써주면 된다

이 실행 구문에는 left와 right를 더해주는 실행 구문을 넣어주었다

그러면 위의 코드처럼 후행 클로저가 완성이 된다

---

### 반환타입 생략

위의 calculate 함수의 method 매개변수는 Int 타입을 반환할 것이라는 사실을 컴파일러도 알기 때문에 굳이 클로저에서 반환타입을 명시해 주지 않아도 된다 대신 in 키워드는 생략할 수 없다

```
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) in
    return left + right
})

print(result) // 20
```

위의 예시에서 in 뒤에 실행 구문 내에 리턴값이 left와 right 즉 Int와 Int 값을 더해줘서 Int 값을 반환하니 

컴파일러는 반환 타입이 Int 라는 것을 알게 되므로 클로저 구문의 반환 타입을 생략해 줄 수 있

---

### 반환타입 생략과 후행 클로저

아래의 예시를 보면

```
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) in
    return left + right
})

print(result) // 20
```

일단 먼저 반환타입을 생략 할 수 있어서 반환타입을 생략해 주었다

그 이후에 자세히 살펴보니 이 함수의 마지막 매개변수가 클로저를 받고 있어서 후행 클로저를 함께 해줄수 있다

```
result = calculate(a: 10, b: 10) { ( left: Int, right: Int) in
    return left + right
}
```

---

### 단축 인자이름

클로저의 매개변수 이름이 굳이 불필요하다면 단축 인자이름을 활용할 수 있다, 단축 인자이름은 클로저의 매개변수의 순서대로 $0, $1... 처럼 표현한다
in 도 생략이 가능하다

```
func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
    return method(a, b)
}
```

```
result = calculate(a: 10, b: 10, method: {
    return $0 + $1
})

print(result) // 20
```

위의 반환타입 생략과 후행 클로저의 예시에서 left 와 right가 굳이 필요한지 생각해보면 굳이 필요하지 않다

왜냐하면 이미 매개변수의 타입도 컴파일러가 알고 있기 때문이다

그렇기 때문에  리턴에 나온 $0은 Int 타입의 첫번째 매개변수 $1은 Int 타입의 두번째 매개변수

이렇게 표현을 해 줄 수 있는 것이다.

---

### 단축 인자이름과 후행 클로저

```
result = calculate(a: 10, b: 10, method: {
    return $0 + $1
})
```

위의 코드는 클로저의 매개변수 이름을 생략하고 단축 한 것이다.

이것 역시 후행 클로저와 함께 사용할 수 있다

```
result = calculate(a:10, b:10) {
    return $0 + $1
}
```

---

### 암시적 반환 표현

암시적 반환 표현은 클로저가 반환하는 값이 있다면 클로저의 마지막 줄의 결과값은 암시적으로 반환 값으로 취급한다

다시말해, 클로저가 반환 값을 가지고 있는 경우 마지막에 나오는 값은 당연히 리턴값이 되겠지 하고 컴파일러가 인지하여 굳이 return 키워드를 안해도 반환값이 반환된다

```
result = calculate(a: 10, b: 10) {
    $0 + $ 1
}
```



