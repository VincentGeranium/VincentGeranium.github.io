---
layout: post
title:  "코코아 와 코코아터치 간단 요약"
date:   2019-06-04
categories: Swift, iOS
---

### 참고 자료

이 포스트는 himoon님의 블로그 포스트와 edwith 부스트코스 iOS 프로그래밍을 듣고 참고하여 작성한 포스트 임을 미리 밝힙니다.

[himoon 블로그](https://himoon.tistory.com/76)

[edwith iOS 부스트코스](https://www.edwith.org/boostcourse-ios/lecture/17994/)

---

# Cocoa Touch Framework

- iOS 애플리케이션 개발환경 토대

- iOS 애플리케이션 개발 환경

- 애플리케이션의 다양한 기능 구현에 필요한 **여러 프레임워크를 포함하는 최상위 레벨의 프레임워크**

- **참고** : 코코아 프레임워크는 macOS 애플리케이션 제작에 사용하는 프레임워크

- **"코코아"** 라는 단어는 **Objcetive-C 런타임 기반으로함**

- **"코코아"** 라는 단어는 **NSObject를 상속받는 모든 클래스 또는 객체를 가리킬 때 사용**

- **"코코아" 또는 "코코아 터치"** 는 **iOS 또는 macOS의 전반적인 기능을 활용해 애플리케이션을 제작 할 때 사용하는 프레임워크**

- **"코코아 터치"** 는 핵심 프레임워크인 **UIKit과 Foundation을 포함**

![cocoa](https://user-images.githubusercontent.com/42841888/58844615-fab55800-86b2-11e9-8a28-d48f4a54c120.png)

---

# Foundation Framework

Foundation 프레임워크는 **컬렉션, 스트링, 메모리 관리, 파일 시스템, 아카이빙 등을 다루는 클래스를 제공**

---

# AppKit Framework

AppKit Framework는 **뷰, 윈도우, 도큐먼트 등 사용자 인터페이스를 만드는 클래스가 들어있다**

---

# 코코아 와 코코아터치 프레임워크의 차이점

**데스크톱과 노트북에서는 AppKit 프레임워크**를 사용할 수 있지만,

**아이폰같은 모바일 기기를 위해서는 UIKit**을 사용해야 한다

**이를 코코아 터치(Foundation + UIKit)프레임워크**라고 부른다

**코코아 = Foundation + AppKit**

**코코아 터치 = Foundation + UIKit**


