---
layout: post
title:  "@IBDesignable과 @IBInspectable - 190519"
date:   2019-05-19
categories: iOS, Swift
---

# @IBDesignable과 @IBInspectable

---

#### 출처

이 포스트는 ZeddiOS님의 블로그 포스트 중 "iOS ) 왕초보를 위한 IBInspectable / IBDesignable 사용해보기" 를 참고하여 쓴 포스트임을 미리 밝힙니다

**링크** [ZeddiOS님의 IBInspectable / IBDesignable 사용해보기](https://zeddios.tistory.com/270)

---

#### 실습 코드

**Github 링크** [VincentGeranium의 github](https://github.com/VincentGeranium/Swift-Study/tree/master/2019-05-19-IBDesignable-And-IBInspectable)

---

Story Board에서 CustomView 형태를 그대로 보고 싶을때

@IBDesignable과 @IBInspectable 어노테이션을 이용

---

# @IBInspectable 

- inspector 에서 해당 인터페이스 요소의 속성을 변경할 수 있게 하는 것

---

# @IBDesignable

- 컴파일 타임으로, 실시간으로 변화된 모습을 스토리보드 내에서 볼 수 있게 하는 것

- 이로 인하여 계속해서 시뮬레이터를 실행하여 변하는 모습을 볼 필요가 없이 컴파일 타임마다 즉각적으로 볼 수 있다
