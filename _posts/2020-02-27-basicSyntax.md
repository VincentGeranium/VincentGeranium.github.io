---
layout: post
title:  "기본 문법 공부(클래스)"
date:   2020-02-27
categories: iOS, Swift
---

이 포스트는 야곰님의 Swift 프로그래밍 2판을 보고 스스로 공부한 내용을 정리한 포스트 입니다.

- - -

### 클래스

- 스위프트의 클래스는 부모클래스가 없더라도 상속 없이 단독으로 정의가 가능하다.

- - -

### 클래스 정의

- 클래스를 정의할 때는 `class`라는 키워드를 사용한다.

```swift
class 클래스 이름 {
    프로퍼티와 메서드들
}
```

![classImage-1](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/classImage-1.png?raw=true)

- 위의 그림에 정의된 클래스는 Float 타입인 height와 weight 저장 프로퍼티가 있는 Person 클래스이다.

- - -

### 클래스 인스턴스의 생성과 초기화

- 클래스를 정의한 후, 인스턴스를 생성하고 초기화하고자 할 때는 기본적인 이니셜라이저를 사용한다.

- Person 클래스에서는 프로퍼티의 기본값이 지정되어 있으므로 전달인자(argument)를 통하여 따로 초깃값을 전달해주지 않아도 된다.

- 인스턴스가 생성되고 초기화된 후(이니셜라이즈된 후) 프로퍼티 값에 접근하고 싶다면 마침표(.)를 사용하면 된다.

- 구조체와는 다르게 클래스의 인스턴스는 참조 타입이므로 클래스의 인스턴스를 상수 let으로 선언해도 내부 프로퍼티 값을 변경할 수 있다.

![classImage-2](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/classImage-2.png?raw=true)

- 기본 이니셜라이저 외에 사용자가 직접 이니셜라이저를 정의할 수도 있다.

- - -

### 클래스 인스턴스의 소멸

- 클래스의 인스턴스는 참조 타입이므로 더는 참조할 필요가 없을 때 메모리에서 해제된다.

- 이 과정을 소멸이라고 하는데 소멸되기 직전 `deinit`라는 메서드가 호출된다.

- 클래스 내부에 deinit 메서드를 구현해주면 소멸되기 직전 deinit 메서드가 호출된다.

- 호출된 deinit 메서드는 `Deinitializer 디이니셜라이저`라고 부른다.

- deinit 메서드는 클래스당 하나만 구현할 수 있으며, 매개변수와 반환 값을 가질 수 없다.

- deinit 메서드는 매개변수를 위한 소괄호도 적어주지 않는다.

![classImage-4](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/classImage-4.png?raw=true)

![classImage-3](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/classImage-3.png?raw=true)

- 보통 deinit 메서드에서는 인스턴스가 메모리에서 해제되기 직전에 처리할 코드를 넣어준다.

- 예를 들어 인스턴스 소멸 전에 데이터를 저장한다거나 다른 객체에 인스턴스 소멸을 알려야 할 때는 특히 deinit 메서드를 구현해야 한다.

- - -