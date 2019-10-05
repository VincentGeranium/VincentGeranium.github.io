---
layout: post
title:  "Property Summary"
date:   2019-10-04
categories: iOS, Swift
---

### Stored Property (저장 프로퍼티)

- **상수(Constant)와 변수(Variable)값을 인스턴스의 일부로 저장**

- **클래스와 구조체에서만 사용**

- 특정 타입의 인스턴스와 연결

- 저장 프로퍼티를 선언 할 때, 저장할 기본값을 줄 수 있음, 값 수정도 가능함

- var로 선언된 것은 변수 저장 프로퍼티, let으로 선언된 것은 상수 저장 프로퍼티

- - -

### Lazy Stored Property (게으른 저장 프로퍼티)

- 값이 사용되기 전까지는 값이 계산되지 않는 프로퍼티이다

- **lazy라는 키워드를 사용하여 선언**

- 게으른 저장 프로퍼티는 초기값이 인스턴스의 초기화가 될때까지 값을 모르는 외부요소에 의존하는 경우 유용

- 게으른 저장 프로퍼티는 초기값이 복잡하거나 계산비용이 많이 드는 설정을 필요로 할때 유용

- 게으른 저장 프로퍼티를 잘 사용하면 성능도 올라가고, 공간낭비도 줄일 수 있다

- **게으른 저장 프로퍼티는 항상 변수로 선언해야 한다 -> var 로 선언**

    - 그 이유는 초기값은 인스턴스 초기값이 검색되지 않을 수 있기 때문이다
    
    - let으로 선언한 프로퍼티는 인스턴스를 만들 때 빼고, 값을 변경 할 수 없다. 이렇게 let으로 선언한 프로퍼티는 초기화를 함과 동시에 값을 가져야하기 때문에, 게으른 저장 프로퍼티로 선언할 수 없다
    
        - 게으른 저장 프로퍼티는 "값이 필요할 때" 초기화를 함
        
    - 두 번째 이유는 lazy로 선언했다고 해도 lazy 프로퍼티가 초기화 되지 않은 상태에서 여러 쓰레드가 동시에 lazy 프로퍼티에 엑세스 한다면, 이 프로퍼티가 단 한번만 초기화 된다는 것을 보장할 수 없기 때문이다.
    
- - -

### Computed Property (연산 프로퍼티)

- **값을 저장하기 보다는 그때마다 특정한 연산을 통해 값을 리턴해주는 프로퍼티**

- **클래스, 구조체, 열거형애서 사용**

- 클래스, 구조체, 열거형은 연산 프로퍼티를 정의할 수 있다

    - **바로 getter 와 setter를 통해 다른 프로퍼티와 간접적으로 값을 검색하고 세팅한다**
    
- **연산 프로퍼티를 정의할 때는 내부에서 연산된 후 나오는 값을 저장할 저장소 변수가가 있어야 한다**

- **연산 프로퍼티는 반드시 var로 선언되어야 한다. 값이 고정되어 있지 않기 때문이다.**

- set에는 괄호를 통해 Declaration을 줄 수 있다

    - **set에 괄호가 없는 것을 Shorthand Setter Declaration이라고 말하고 newValue라는 키워드를 사용해야 한다**
    
- - -

### Read-Only Computed Property (읽기 전용 연산 프로퍼티)

- **get 만 있는 연산 프로퍼티를 Read-Only Computed Property라고 한다.**

- get 만 있을 때는 get을 생략 할 수 있다.

- Example Code

```swift

struct Cuboid {

    var width = 0.0
    
    var height = 0.0
    
    var depth = 0.0
    
    var volume: Double {
        return width * height * depth
    }
}
```

- volume에 특정한 값을 주는 set 연산은 못한다

- - -

### Type Property

- **인스턴스 프로퍼티(Instance Property)란, 특정 타입의 인스턴스에 속하는 프로퍼티**

    - 특정한 구조체, 클래스에 속하는 저장 프로퍼티(Stored Property)와 연산 프로퍼티(Computed Property)가 바로 인스턴스 프로퍼티(Instance Property)이다.
    
- **프로퍼티를 타입 자체와 연결이 가능한 프로퍼티를 타입 프로퍼티(Type Property)라고 한다**

- 타입 프로퍼티는 모든 타입이 사용할 수 있는 상수 프로퍼티(constant property) 또는 글로벌 변수 프로퍼티와 같이 특정 타입의 모든 인스턴스에 공통적인 값을 정의하는 데 유용하다.

- **저장 타입 프로퍼티(Stored Type Property)는 변수(var) 또는 상수(let)일 수 있다**

- **연산 타입 프로퍼티(Computed Type Property)는 Computed Instance Property와 같이 항상 변수(var) 프로퍼티로 선언된다**

- **저장 인스턴스 프로퍼티(Stored Instance Property)와 달리 저장 타입 프로퍼티(Stored Type Property)는 항상 기본값(default value)을 줘야한다**

    - 그 이유는 초기화 시에, 타입 자체에는 저장 타입 프로퍼티(stored type property)에 할당할 initializer가 없기 때문이다.
    
- 저장 타입 프로퍼티(Stored type property)는 처음 엑세스 할때는 게으르게 초기화(lazily initizlized)한다

    - 다수의 thread에 의해 동시에 엑세스 되고 있어도, 한번만 초기화되는 것이 보증되어 있어 "lazy" 키워드를 사용할 필요는 없다
    
- Swift에서 타입 프로퍼티는 타입 정의의 **일부분으로** 타입의 **외부 중괄호 안에 쓰여지며,** 각 타입 프로퍼티는 명시적으로 지원하는 타입으로 범위가 지정되게 된다.

- **static** 키워드를 사용하여 **타입 프로퍼티를 정의할 수 있다.**

- class 타입에 대한 연산 타입 프로퍼티(Computed type property)의 경우, **class** 키워드를 사용하여 서브클래스가 슈퍼클래스의 구현을 **재정의(override)**할 수 있다.

- - -

### Example Code

[저장 프로퍼티](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-03-storedPropertyExample.playground)

[게으른 저장 프로퍼티](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-03-LazyStoredPropertyExample.playground)

[연산 프로퍼티](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-03-ComputedPropertyExample.playground)

[타입 프로퍼티](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-10-04-TypePropertyExample.playground)