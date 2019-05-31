---
layout: post
title:  "타입캐스팅 is, as 개념 정리"
date:   2019-05-30
categories: iOS, Swift
---

# Type Casting, Downcasting

---

### 참고 자료

이 포스트는 ZeddiOS 님의 **Swift ) Type Casting**을 참고하여 작성한 포스트임을 미리 밝힙니다

[ZeddiOS님의 블로그](https://zeddios.tistory.com/265)

---

# 타입 캐스팅의 목적

1) 타입 캐스팅은 인스턴스의 타입을 확인

2) 인스턴스의 타입을 슈퍼클래스 또는 서브클래스 타입처럼 다루기 위해

---

# is And as

**is**와 **as** 라는 연산자로 타입 캐스팅

**is**와 **as** 는 **1) 값의 타입을 확인하거나,** **2) 값을 다른 타입으로 변환** 하는 간단하고 표현적인 방법을 제공

**as와 as?, as!의 차이점**
1) 실행되는 시간의 차이
- as는 컴파일 타임에 실행
- as?와 as!는 런타임에 실행


2) as는 업캐스팅과 패턴매칭(switch)에서만 사용할 수 있다.

---

# 타입 캐스팅을 이용한 클래스의 계층 정의

클래스 및 하위 클래스의 계층 구조와 함께, **타입 캐스팅을 사용하여 특정 클래스 인스턴스의 타입을 확인**

**해당 인스턴스를 동일한 계층구조 내의 다른 클래스로 캐스트 할 수 있다**

---

## 타입 캐스팅을 사용하여 특정 클래스 인스턴스의 타입을 확인

**is** 키워드를 통해 **특정 클래스의 인스턴스의 타입 확인** (**Struct도 가능**)

[is_typeCasting](https://user-images.githubusercontent.com/42841888/58674377-83b65180-838a-11e9-8f35-c915999fb06c.png)

**jun 이라는 인스턴스가 Person의 인스턴스인가? 하고 확인하는 것** -> 인스턴스 자체를 확인 -> **is 사용**

[is_typeCasting_property](https://user-images.githubusercontent.com/42841888/58674539-42727180-838b-11e9-801d-0bc750dc9543.png)

**jun이라는 인스턴스의 타입이 String인가? 하고 확인하는 것** -> 인스턴스의 프로퍼티를 확인 -> **is 사용** 

[is_ArrayTypeCheck](https://user-images.githubusercontent.com/42841888/58675266-81ee8d00-838e-11e9-9ce4-89cfd48a1085.png)

**배열을 돌면서 해당 인스턴스가 Movie인지, Song인지 "is"로 타입을 확인**

---

# 다운캐스팅

특정 클래스 타입의 상수 또는 병수는 하위 클래스의 인스턴스를 참조 할 수 있다

**이 경우에는 타입캐스트 연산자 (as? 또는 as!)를 사용하여 서브 클래스 타입으로 "다운캐스팅"을 시도 할 수 있다**

---

## 다운캐스팅의 타입캐스팅 연산자의 두 가지 형태, 그 목적과 이유

다운캐스팅은 실패 할 가능성이 있다, 때문에 타입 캐스트 연산자는 두가지 형태로 제공되는데

**1) 조건부 형식인 ?은 다운캐스팅 하려는 타입의 Optional 값을 반환한다**

**2) 강제 형식인 !은 강제 언래핑을 하여 값을 반환한다**

여기서 주의 할 점이 있다, 강제 형식은 다운캐스팅이 꼭 성공할 것이라는 확신이 들때만 강제 형식인 !을 사용해야 한다

잘못된 클래스의 타입으로 다운캐스트 하려고 하면, **런타임 에러**를 발생시킨다

[as_typeCasting](https://user-images.githubusercontent.com/42841888/58676541-96815400-8393-11e9-9204-64db0136efbf.png)

if let 구문을 활용하여 **as? 라는 조건부 형식 다운캐스팅을 진행**

storedMovieAndSong는 MovieOrSong 타입의 배열, 그 안에 들어있는 인스턴스는 MovieOrSong의 서브클래스들인 movie와 song

MovieOrSong = 슈퍼클래스

movie와 song 클래스는 MovieOrSong의 서브클래스 -> 다운캐스팅이 가능 -> **as**로 다운캐스팅

---

### 예제 파일 

[github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-05-31-typeCastingExample.playground)
