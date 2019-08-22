---
layout: post
title:  "UIScreen 간략 정리"
date:   2019-08-23
categories: Swift, iOS
---

### 이 포스트는 Apple의 documentation을 참고하여 작성한 포스트 입니다.

---

# UIScreen

---

- class
- Framework : UIKit

#### UIScreen 은 하드웨어 기반 디스플레이와 관련된 속성을 정의하는 객체

- 이 클래스를 사용하여 각 디바이스에 연결되어 있는 디스플레이에 대한 화면 객체를 얻을 수 있다
- 각 화면 객체는 관련 디스플레이의 bounds rectangle 과 화면의 밝기와 같은 것을 정의한다
- iOS 8 이상에서 스크린의 bounds 프로퍼티는 화면의 인터페이스 방향을 고려한다
    - 이것은 세로방향과 가로방향이 같지 않을 수 있음을 의미한다
- fixedCoordinateSpace 프로퍼티를 사용하여 앱 화면을 계산할수 있다.

---