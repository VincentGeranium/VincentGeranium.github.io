---
layout: post
title:  "NSLayoutConstraint 제약조건 지정 방법"
date:   2019-09-10
categories: iOS, Swift
---

이 포스트는 edwith의 iOS 프로그래밍 강의를 듣고 정리한 내용입니다.

---

# NSLayoutConstaint 제약조건 지정

- 코드로 오토레이아웃을 구현하는 다른 방법인 NSLayoutConstraint 인스턴스 생성을 사용하여 제약조건을 지정하는 방법

    - 오토레이아웃 방정식
    
        - view1.attr1 = view2.attr2 * multiplier + constant
        
        - item.attribute = toItem.attribute * multiplier + constant
        
![NSLayoutConstaint](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/NSLayoutConstaint.png?raw=true)

- button과 textField에 기본간격 (8 point)에 제약을 주기 위해 NSLayoutConstraint 인스턴스를 생성하는 코드

```swift
NSLayoutConstraint(item: button,
                attribute: .right,
                relatedBy: .equal,
                toItem: textField,
                attribute: .left,
                multiplier: 1.0,
                constant: 8.0)
```

![NSLayoutConstraintExample](https://github.com/VincentGeranium/VincentGeranium.github.io/blob/master/assets/img/NSLayoutConstraintExample.png?raw=true)