---
layout: post
title:  "AppDelegate.swift에 대하여"
date:   2019-05-14
categories: iOS, Swift
---

# AppDelegate

---

#### 출처

- 이 포스트는 ZeddiOS 님의 블로그 글 중 "AppDelegate.swift의 역할"을 참고하여 작성한 글임을 미리 밝힙니다

[ZeddiOS님의 블로그](https://zeddios.tistory.com/218)

---

# AppDelegate.swift의 역활

**AppDelegate.swift**라는 소스파일은 두가지 역활을 한다

---

## 1. AppDelegate 클래스를 정의

이 큰 제목에 관하여 말하기 전에 미리 알아둬야 할 용어가 있다

**app delegate**

**이 app delegate 와 AppDelegate와는 다르다**

- app delegate는 **AppDelegate클래스의 인스턴스**

- **이 app delegate는 앱의 객체**

- **app delegate는 앱의 상태에 따라 응답하는 콘텐츠가 그려지는 창(window)를 만든다**

- **즉, AppDelegate.swift 가 있으므로 AppDelegate 클래스가 만들어지고, 이 AppDelegate 클래스의 인스턴스인 app delegate가 앱 내용이 그려질 창(window)를 만드는 것이다.**

---

## 2. AppDelegate.swift는 entry point와, 앱의 입력 이벤트를 전달하는 run loop를 생성

- 이 작업은 UIApplicationMain 속성에 의해 수행, 이 속성은 파일의 맨 위에 나타나있다

- **UIApplicationMain 속성을 사용하는 것은 UIApplicationMain 함수를 호출하고 AppDelegate 클래스의 이름을 delegate 클래스에 전달하는 것과 동일하다**

- 이에 대한 응답으로, 시스템은 **응용프로그램 객체(application object)를 생성**

- **응용프로그램 객체(application object)는 app의 life을 담당한다**

- 또한, 시스템은 AppDelegate 클래스의 인스턴스를 생성하고 이를 응용프로그램 객체(application object)에 할당

- **마지막으로, 시스템은 앱을 실행**

---

## AppDelegate에 대한 부가적 설명

- AppDelegate 클래스는 새 프로젝트를 만들 때 마다 자동으로 생성.

- Xcode에서 제공하는 AppDelegate 클래스를 사용하여 앱을 초기화 하고, app-level 이벤트에 응답

- **AppDelegate 클래스는 UIApplicationDelegate 프로토콜을 채택**

- 이 **UIApplicationDelegate 프로토콜은 앱을 세팅하고, 앱 상태 변화에 응답하며, 다른 app-level 이벤트를 처리하는데 사용하는 여러가지 방법을 정의**

---

## AppDelegate 클래스에는 프로퍼티 하나가 포함되어 있다 : window

- 이 프로퍼티는 앱의 창(window)에 대한 **참조**를 저장

- 이 창(window)은 앱의 view 계층구조의 **루트**를 나타낸다, 이는 앱 콘텐츠가 모두 그려지는 곳이다

- window 프로퍼티는 **Optional 프로퍼티**, 즉 어떨때는 아무런 값도 없을 수 있다는 (nil)것을 의미

```
var window: UIWindow?
```

---

## AppDelegate 클래스는 몇몇 delegate 메소드들이 구현되어 있다

[AppDelegate](https://user-images.githubusercontent.com/42841888/57665754-2c00b200-7638-11e9-9b99-6d9b9bde0c98.png)

- **이 메소드들을 사용하면, 응용프로그램 객체(Application Object)가 app delegate와 통신 할 수 있다**

- 앱의 상태가 전환되는 동안 응용프로그램 객체는 위 메소드들 중 해당하는 delegate 메소드를 호출하여 앱이 응답 할 수 있는 기회를 제공

- 이러한 메소드들이 올바른 시간에 호출되도록 하려고 특별한 작업을 수행 할 필요는 없다. 응용프로그램 객체가 해당 작업을 알아서 처리

- 위의 Delegate 메소드들은 기본동작이 있다, 구현을 비워두거나, AppDelegate 클래스에서 지운다면 해당 메소드가 호출될 때마다 기본동작을 얻는다 또는 메소드를 호출 할 때 실행되는 사용자 지정 동작을 정의 할 수 있다.
