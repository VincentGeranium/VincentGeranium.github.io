---
layout: post
title:  "Type Property에 대해여"
date:   2019-05-12
categories: iOS, Swift
---

# Type Property

---

#### 이 포스트는 저의 공부 목적으로 작성한 글 입니다

#### 이 포스트는 ZeddiOS 님의 블로그 글 중 Swift ) Properties - Type Properties 를 참고하여 쓴 포스트임을 미리 밝힙니다

**출처:** [ZeddiOS](https://zeddios.tistory.com/251)

---

#### 인스턴스 프로퍼티(Instance Property)

- **특정 타입의 인스턴스에 속하는 프로퍼티**
    - 예를들어 말하면, 특정 구초제, 클래스에 속한 저장 프로퍼티 또는 연산 프로퍼티
    
---

#### 타입 프로퍼티 (Type Property)

- **프로퍼티를 타입 자체와 연결할 수도 있다** 이러한 프로퍼티를 **Type Property**라고 한다.
- 타입 프로퍼티는 모든 타입이 사용할 수 있는 상수 프로퍼티(constants property) 또는 글로벌 변수 프로퍼티와 같이 특정 타입의 모든 인스턴스에 공통적인 값을 정의하는데 유용

---

#### 연산 타입 프로퍼티 (Computed type Property)

- 연산 인스턴스 프로퍼티(Computed instance property)와 같이 항상 **변수(var) 프로퍼티**로 선언

---
#### 저장 타입 프로퍼티 (Stored type Property)

- 변수 또는 상수일 수 있다
- 저장 인스턴스 프로퍼티(Stored instance property)와 달리 **저장 타입 프로퍼티(Stored type property)에는 항상 기본값(default value)를 줘야한다**
    - 그 이유는 초기화 시에, 타입 자체에는 저장 타입 프로퍼티에 값을 할당할 **initializer가 없기 때문이다**
- 저장 타입 프로퍼티는 처음 엑세스 할때는 게으르게 초기화(lazily initialized) 된다
    - 다수의 thread에 의해 동시에 엑세스 되고 있어도, 한번만 초기화되는 것이 보증되어 있어 lazy라는 키워드를 사용할 필요 없다
    
---

#### 저장 타입 프로퍼티 설명에 대한 정리

1. 프로퍼티를 **타입 자체에 연결 가능** => 그것이 바로 **타입 프로퍼티**

2. **타입프로퍼티**의 두 종류가 있다 => 1) **저장 타입 프로퍼티(Stored type Property)** 2) **연산 타입 프로퍼티 (Computed type Property)**

3. 저장 타입 프로퍼티(Stored type Property)는 상수/변수 둘 다 가능 => let/var 로 선언이 가능, 무조건 기본값(default value)를 줘야 한다.

4. 연산 타입 프로퍼티(Computed type Property)는 무조건 변수(variable)로 선언 되어야 한다

---

#### 부가적 설명

- **Swift에서 타입 프로퍼터는 타입 정의의 일부로 타입의 외부 중괄호 안에 쓰여지며, 각 타입 프로퍼티는 명시적으로 지원하는 타입으로 범위가 지정되게 된다**

- **"static"** 키워드를 사용하여 타입 프로퍼티를 정의 할 수 있다

- 클래스 타입에 대한 연산 타입 프로퍼티(Computed type property)의경우, "class" 키워드를 사용하여 서브클래스가 슈퍼클래스의 구현을 재정의(override) 할 수 있다

---

#### 예제 코드를 통한 설명

```
struct UnknownStructure {

    static var storedTypeProperty = "unknownValue"

    static var computedTypeProperty: Int {
        
        return 7
        
    }
    
}
```

UnknownStructure 라는 구조체를 선언, 그 안에는 static 키워드를 사용한 것들이 있다

static 키워드라 없었으면 그냥 저장 인스턴스 프로퍼티(Stored instance property) 와 연산 인스턴스 프로퍼티(Computed instance property)로 알 수 있지만, static 키워드가 붙어있으니,

저장 타입 프로퍼티(Stored type property)와 연산 타입 프로퍼티(Computed type property)라는 것을 알 수 있다.

위의 예시에서 보면 **static var storedTypeProperty = "unknownValue"** 로 저장 인스턴스 프로퍼티와는 다르게 **기본값(default value)** 를 준것을 볼 수 있다.

위의 예시에서 보면 **static var computedTypeProperty: Int { return 7 }** 로 연산 타입 프로퍼티(Computed type property) 가 정의되어 있는데 위에 연산 타입 프로퍼티를 설명한 부분을 보면 **연산 타입 프로퍼티는 무조건 변수(var)** 로 선언되어 있어야 한다는 설명과 같이 var 로 선언 되어 있다.

---

#### 예제 코드를 통한 설명 2

```
enum UnknownEnumeration {
    
    static var storedTypeProperty = "unknownValue"
    
    static var computedTypeProperty: Int {
    
        return 77
    
    }
}
```

**저장 인스턴스 프로퍼티(Stored property)는 상수와 변수의 값을 인스턴스의 일부로 저장, 클래스와 구조체에서만 사용된다** 라고 알고있다.

그러나

**저장 타입 프로퍼티(Stored Type Property)는 enum (열거형)에서 사용이 가능하다**

---

#### 예제 코드를 통한 설명 3

이 예제를 보기전에 미리 머리 속에 넣어두고 봐야 할 것이 있는데

**"클래스 타입에 대한 연산 타입 프로퍼티(Computed type property)의 경우 "class"키워드를 사용하여 서브클래스가 슈퍼클래스의 구현을 재정의(override) 할 수 있다" 는 점을 기억하고 봐야한다**

```
class UnknownClass {
    
    static var storedTypeProperty = "unknowValue"
    
    static var computedTypeProperty: Int {
    
        return 30
    
    }
    
    class var canOverrideComputedTypeProperty: Int {
    
        return 4
        
    }
    
    static var anotherComputedTypeProperty: Int {
    
        return 1234
        
    }
    
}
```

이 클래스에서 중점적으로 봐야 할 점은

**class var canOverrideComputedTypeProperty: Int { return 4 }**

이 코드인데 **static 키워드**가 붙지 않고 **class**라는 키워드가 붙어있다

위에서 한 설명 중

**클래스 타입에 대한 연산 타입 프로퍼티(Computed Type Property)의 경우, class 키워드를 사용하여 서브클래스가 슈퍼클래스의 구현을 재정의(override)할 수 있다** 라고 명시해 놓았었다

위의 예시 코드를 보면 canOverrideComputedTypeProperty는 class 키워드가 붙어있으니

**연산 타입 프로퍼티**이고 이 **class 키워드가** 붙어있는 것을 봐서 **이 연산 타입 프로퍼티는 재정의 할 수 있다는 뜻이다**

```
class TheSubClass: UnknowClass {

    override static var canOverrideComputedTypeProperty: Int {
    
        return 42430
        
    }

}
```

이렇게 UnknowClass를 상속받은 TheSubClass 서브 클래스에서 슈퍼클래스인 UnknownClass에서

정의했던 canOverrideComputedTypeProperty 연산 타입 프로퍼티를 재정의(override) 할 수 있다

**여기서 재정의시 잊으면 안되는 점은 override 키워드와 static키워드를 꼭 써줘야 한다는 점이다**

그리고 만약에 class를 안붙인 그냥 연산 프로퍼티를 서브클래스에서 재정의하면 에러를 낸다

#### 에러 예시 코드

```
class TheSubClass: UnknowClass {

    override static var anotherComputedTypeProperty: Int {
    
        return 1
        
    } // error! cannot override static var

}
```

---

#### 타입 프로퍼티의 값 접근과 값 수정

```
struct ExampleLengthRange {

    var firstExampleValue: Int
    let firstExampleLength: Int

}

var rangeOfItems = ExampleLengthRange(firstExampleValue: 0, length: 5)

rangeOfItems.firstExampleValue = 7
rangeOfItems.firstExampleLength = 15 //error
```

위의 예시코드 처럼 구조체,열거형 또는 클래스의 인스턴스를 만들고 그 인스턴스를 통해서 프로퍼티들에 접근 할 수 있었다

**그러나**

**타입 프로퍼티는 타입 "자체"의 이름을 치고 .(dot)을 통해 프로퍼티에 접근한다**

**타입 자체의 이름을 통해 프로퍼티에 접근하는 것 빼고, 인스턴스 프로퍼티와 사용법은 동일하다**

아래의 코드를 보면서 한번 더 이해해보자

```
print(UnknownStructure.storedTypeProperty) // "unknownValue"

UnknownStructure.storedTypeProperty = "another Value"

print(UnknownStructure.storedTypeProperty) // "another Value"

print(UnknownEnumeration.computedTypeProperty) // 77

UnknownEnumeration.computedTypeProperty = 15

print(UnknownEnumeration.computedTypeProperty) // 15

```
