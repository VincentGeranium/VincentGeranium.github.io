---
layout: post
title:  "기본 문법 공부(스위프트 기초 - 옵셔널 추출, 강제 추출, 옵셔널 바인딩, 암시적 추출 옵셔널, 옵셔널 추출 마무리)"
date:   2020-04-13
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 예제 코드

- [Optional Unwrapping Example Code - 1](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-13-optionalUnwrappingExample-1.playground)

- [Optional Unwrapping Example Code - 2](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-13-optionalUnwrappingExample-2.playground)

- [Optional Unwrapping Example Code - 3](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-13-optionalUnwrappingExample-3.playground)

- [Optional Unwrapping Example Code - 4](https://github.com/VincentGeranium/Swift-Study/tree/master/2020-04-13-optionalUnwrappingExample-4.playground)

- - -

### 참고 자료

- [Swift.org](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

- - -

### 옵셔널 추출 (Optional Unwrapping)

- '옵셔널의 값을 옵셔널이 아닌 값으로 추출'하는 옵셔널 추출(Optional Unwrapping)

- - -

### 옵셔널 강제 추출 (Forced Unwrapping)

- 옵셔널 강제 추출(Forced Unwrapping) 방식은 옵셔널의 값을 추출하는 가장 간단하지만 '가장 위험한 방법'이다.

    - 런타임 오류가 일어날 가능성이 가장 높기 때문이다.
    
    - 또, 옵셔널을 만든 의미가 무색해지는 방법이기도 하다.
    
- 옵셔널의 값을 강제 추출(Forced Unwrapping)하려면 옵셔널 값의 뒤에 느낌표(!)를 붙여주면 값을 강제로 추출하여 반환해준다.

- 강제 추출 시 옵셔널에 값이 없다면, 즉 nil 이라면 런타임 오류가 발생한다.

<img width="1058" alt="optionalUnwrappingImage-1" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalUnwrappingImage-1.png?raw=true">
<img width="1058" alt="optionalUnwrappingImage-2" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalUnwrappingImage-2.png?raw=true">

- 런타임 오류의 가능성을 항상 내포하기 때문에 옵셔널 강제 추출 방식은 사용하는 것을 지양해야 한다.

- - -

### 옵셔널 바인딩 (Optional Binding)

- '옵셔널 강제 추출' 파트에서 사용한 if 구문을 통해 myName이 nil인지 먼저 확인하고 옵셔널 값을 강제 추출(Forced Unwrapping)하는 방법은 다른 프로그래밍 언어에서 NULL 값을 체크하는 방식과 비슷하다.

    - 앞서 설명한 것처럼 옵셔널을 사용하는 의미도 사라진다.
    
- 스위프트는 조금 더 안전하고 세련된 방법으로 옵셔널 바인딩(Optional Binding)을 제공한다.

- 옵셔널 바인딩(Optional Binding)은 옵셔널에 값이 있는지 확인할 때 사용한다.

- 옵셔널에 값이 있다면 옵셔널에서 추출한 값을 '일정 블록 안에서 사용할 수 있는 상수나 변수로 할당해서 옵셔널이 아닌 형태로 사용'할 수 있도록 한다.

- 옵셔널 바인딩(Optional Binding)은 if 또는 while 구문 등과 결합하여 사용 할 수 있다.

<img width="1058" alt="optionalUnwrappingImage-3" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalUnwrappingImage-3.png?raw=true">

- 위의 그림 속 코드에서는 if 구문을 실행하는 블록 안쪽에서만 name이라는 임시 상수를 사용 할 수 있다.

    - 즉, if 블록 밖에서는 사용할 수 없고 else 블록에서도 사용할 수 없다.
    
    - 때문에 위와 아래 각기 다른 옵셔널 바인딩 예시 코드에서 모두 별도로 name을 사용했지만 충돌이 일어나지 않았다.
    
- 상수(Constant - let)로 사용하지 않고 변수(Variable - var)로 사용하고 싶다면 if var를 통해 임시 변수로 할당할 수도 있다.

- 위의 그림 속 코드에서는 if와 else 블록만 사용했지만, else if 블록도 추가할 수 있다.

- - -

### 옵셔널 바인딩을 사용한 여러 개의 옵셔널 값의 추출

- 옵셔널 바인딩을 통해 한 번에 여러 옵셔널의 값을 추출할 수도 있다.

- 쉽표(,)를 사용해 바인딩 할 옵셔널을 나열하면 된다.

- 단, 바인딩하려는 옵셔널 중 하나라도 값이 없다면 해당 블록 내부의 명령문은 실행되지 않는다.

<img width="1058" alt="optionalUnwrappingImage-4" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalUnwrappingImage-4.png?raw=true">

- 옵셔널 바인딩은 옵셔널 체이닝과 환상의 결합을 이누다.

- - -

### 암시적 추출 옵셔널 (Implicitly Unwrapping Optionals)

- 때때로 nil을 할당하고 싶지만, 옵셔널 바인딩으로 매번 값을 추출하기 귀찮거나 로직상 nil 때문에 런타임 오류가 발생하지 않을 것 같다는 확신이 들 때 nil을 할당해줄 수 있는 옵셔널이 아닌 변수나 상수가 있다.

    - 이때 사용하는 것이 바로 암시적 추출 옵셔널(Implicitly Unwrapping Optionals)이다.
    
    - * '확신이 들 때' 라는 말을 위의 문장에서 사용했지만 이는 매우 위험한 생각이다. 실제로 프로젝트용 프로그래밍 중에 오류가 생기지 않겠다라는 확신이 드는 순간은 드물다.

- 옵셔널을 표시하고자 타입 뒤에 물음표(?)를 사용했지만, 암시적 추출 옵셔널(Implicitly Unwrapping Optionals)을 사용하려면 타입 뒤에 느낌표(!)를 사용해주면 된다.

- 암시적 추출 옵셔널(Implicitly Unwrapping Optionals)로 지정된 타입은 일반 값처럼 사용할 수 있으나, 여전히 옵셔널이기 때문에 nil도 할당해줄 수 있다.

    - 그러나 nil이 할당되어 있을 때 접근을 시도하면 런타임 오류가 발생한다.
    
<img width="1058" alt="optionalUnwrappingImage-5" src="https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/optionalUnwrappingImage-5.png?raw=true">

- - -

### 옵셔널 추출 마무리

- 옵셔널을 사용할 때는 강제 추출 또는 암시적 추출 옵셔널을 사용하기보다는 옵셔널 바인딩, nil 병합 연산자를 비롯해 옵셔널 체이닝 등의 방법을 사용하는 것이 훨씬 안전하다.

- 또한 이렇게 하는 것이 스위프트의 지향점에 부합하다.

- - -