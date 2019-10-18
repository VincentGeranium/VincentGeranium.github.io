---
layout: post
title:  "Gesture Recognizer Summary"
date:   2019-10-18
categories: iOS, Swift
---

이 포스트는 edwith의 부스트코스 iOS 프로그래밍을 공부하고 정리한 내용입니다

[edwith iOS 프로그래밍 - Gesture Recognizer](https://www.edwith.org/boostcourse-ios/lecture/17992/)

- - -

### Gesture Recognizer

- 제스처 인식기는 여러 제스처 관련 이벤트를 인식할 수 있다

- 특정 제스처 이벤트가 일어날 때 마다 각 타깃에 맞는 액션 메시지를 보내어 제스처 관련 이벤트를 처리할 수 있다

- - -

### UIGestureRecognizer Class

- UIGestureRecognizer 클래스는 특정 제스처 인식기에 대한 동작을 정의한다

- 또한 델리게이트 객체를 활용하여 일부 동작을 더욱 세밀하게 사용자화 할 수 있다

- - -

### UIGestureRecognizer의 하위 클래스

- 아래의 7가지 UIGestureRecognizer 하위 클래스를 통해 여러 제스처를 인식할 수 있다

    - 1) UITapGestureRecognizer
        
        - 싱글탭 또는 멀티탭 제스쳐
        
    - 2) UIPinchGestureRecognizer
    
        - 핀치(Pinch) 제스처
        
    - 3) UIRotationGestureRecognizer
    
        - 회전 제스쳐
        
    - 4) UISwipeGestureRecognizer
    
        - 스와이프(swipe) 제스쳐
        
    - 5) UIPanGestureRecognizer
    
        - 드래그(Drag) 제스쳐
        
    - 6) UIScreenEdgePanGestureRecognizer
    
        - 화면 가장자리 드래그 제스쳐
        
    - 7) UILongPressGestureRecognizer
    
        - 롱프레스(long-press) 제스쳐
        
- 제스쳐 인식기를 사용하기 위해서 타깃-액션 연결을 설정한 후 UIView의 메서드인 addGestureRecognizer(_:) 메서드를 통해 뷰에 연결한다

    - 제스쳐가 인식되면 해당 제스쳐 인벤트에 연결된 타깃에 액션 메시지가 전달된다
    
    - 호출되는 메서드는 아래의 메서드 구현 형식 중 하나와 같아야 한다
    
```swift

@IBAction func myActionMethod()
@IBAction func myActionMethod(_ sender: UIGestureRecognizer)

```

- 윈도우는 뷰에 터치 이벤트를 전달하기 전에 뷰에 추가된 제스쳐 인식기에 터치 이벤트를 전달한다

- 제스쳐 인식기가 터치 이벤트를 인식했을 경우 뷰는 터치 이벤트를 받지 못하고, 제스쳐 인식기가 터치 이벤트를 인식하지 못했을 경우 터치 이벤트를 뷰가 받게 된다

- 일반적인 제스처 인식기의 동작의 흐름은 cancelsTouchesInView, delaysTouchesBegan, delaysTouchedEnded 프로퍼티의 값에 영향을 받는다