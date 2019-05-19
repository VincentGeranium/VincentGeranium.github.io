---
layout: post
title:  "UIWindow란? - 190519"
date:   2019-05-19
categories: iOS, Swift
---

# What is the UIWindow ??

---

#### 출처

이 포스트는 Alpaca 님의 글을 참고하여 쓴 포스트임을 미리 밝힙니다

[Alpaca님의 UIWindow에 대한 글](https://medium.com/@Alpaca_iOSStudy/uiwindow-5e7a9d72c582)

---

# UIWindow의 역활

- 앱의 시각적 콘텐츠를 담는다

- 뷰들과 다른 어플리케이션 객체들에게 터치 이벤트를 전달한다

- 오리엔테이션 변화를 쉽게하기 위해 앱의 뷰 컨트롤러들과 협력한다

---

# UIWindow

- window 객체는 뷰들을 담는 컨테이너라고 생각하면 된다

- 스크린에 표시되는 뷰의 계층구조에서 최상위 뷰의 역활을 할 고정적인 객체의 역활을 한다

- 앱의 생명 주기 동안 특별한 경우를 제외하고 단 하나의 window 객체만을 생성하고 사용

- 표시한 뷰가 바뀌어야 하는 경우 가장 앞에있는 rootViewController의 교체를 통해 뷰를 바꾸는 방법을 사용한다

- Xcode 프로젝트가 생성되면 자동으로 AppDelegate에 window 객체를 생성

- window 객체를 새로이 생성 또는 상속받는 일은 잘 없다

---

# Window 객체를 새로 만들어지는 특별한 경우

- 스토리보드를 쓰지 않는 경우 메인 window를 직접 생성해야 한다

- 외부 디스플레이를 지원하는 앱의 경우 새로운 window를 만들어 보여줄 수 있다

- 보통의 경우 새로운 window는 시스템에 의해 만들어지며 특정 이벤트의 대한 반응으로 만들어진다 (ex: 전화가 오는 경우)

---

# 메인 window를 만드는 두가지 방법

- 프로그래밍 방법

- 인터페이스 빌더 방법

메인 window 객체는 위 두가지 방법으로 생성과 설정이 가능하다

AppDelegate 객체가 메인 window 객체를 잡고 있어야 한다.

그리고 이 객체는 백그라운드나 포그라운드에 상관없이 앱이 실행될 때는 항상 생성해야 한다.
